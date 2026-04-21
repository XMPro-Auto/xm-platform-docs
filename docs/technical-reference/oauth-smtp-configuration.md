# OAuth SMTP Configuration for Microsoft 365

> [!IMPORTANT]
> **Microsoft is deprecating Basic Authentication for SMTP:**
>
> - **March 1, 2026**: Microsoft begins rejecting Basic Auth for SMTP submissions
> - **April 30, 2026**: 100% rejection of Basic Auth SMTP submissions
>
> If you use Microsoft 365 or Office 365 for SMTP, you must configure OAuth 2.0 authentication before March 2026.

> [!NOTE]
> **Supported Versions:** OAuth SMTP configuration is supported in XMPro 4.6 and later.

## Overview

XMPro supports OAuth 2.0 authentication for SMTP using the client credentials grant flow. This is Microsoft's recommended replacement for Basic Authentication and provides enhanced security through token-based authentication.

This guide covers Azure AD app registration, platform-specific configuration for each deployment method, testing and verification, troubleshooting common issues, and migration from Basic Auth.

**When to use OAuth SMTP:**

- **Required**: When using Microsoft 365 or Office 365 SMTP after March 2026
- **Recommended**: For any email service that supports OAuth 2.0 authentication
- **Not Required**: For SMTP servers that continue supporting Basic Authentication

## Prerequisites

Before configuring OAuth SMTP in XMPro, you need:

1. **Azure Active Directory access** with permissions to:
   - Create app registrations
   - Grant admin consent for API permissions

2. **Microsoft 365 mailbox** configured for sending email

3. **XMPro deployment method**:
   - Azure Terraform
   - Windows Server installer

## Azure AD App Registration

### Step 1: Create App Registration

1. Sign in to the [Azure Portal](https://portal.azure.com)

2. Navigate to **Azure Active Directory** > **App registrations**

3. Click **New registration**:
   - **Name**: `XMPro SMTP OAuth` (or your preferred name)
   - **Supported account types**: **Accounts in this organizational directory only (Single tenant)**
   - **Redirect URI**: Leave blank
   - Click **Register**

4. **Note the following values** (you'll need them for XMPro configuration):
   - **Application (client) ID** - Located on the Overview page
   - **Directory (tenant) ID** - Located on the Overview page

### Step 2: Create Client Secret

1. In your app registration, go to **Certificates & secrets**

2. Click **New client secret**:
   - **Description**: `XMPro SMTP Secret` (or your preferred description)
   - **Expires**: Choose an appropriate expiration (Recommended: 12 or 24 months)
   - Click **Add**

3. **Copy the secret value immediately** - You won't be able to see it again!
   - Store this securely - you'll need it for XMPro configuration

> [!WARNING]
> **Secret Expiration**: Client secrets expire after the chosen period. Set a calendar reminder to rotate the secret before it expires to avoid SMTP failures.

### Step 3: Configure API Permissions

1. In your app registration, go to **API permissions**

2. Click **Add a permission** > **APIs my organization uses**

3. Search for and select **Office 365 Exchange Online**

4. Select **Application permissions** (not Delegated permissions)

5. Add these two permissions:
   - **SMTP.SendAsApp** - Send mail using SMTP AUTH protocol
   - **Mail.Send** - Send mail as any user

6. Click **Add permissions**

7. **Grant admin consent**:
   - Click **Grant admin consent for [Your Organization]**
   - Confirm when prompted
   - Wait for the status to show "Granted for [Your Organization]"

> [!NOTE]
> **Admin Consent Required**: Application permissions require admin consent. If you don't see the "Grant admin consent" button, contact your Azure AD administrator.

### Step 4: Enable SMTP AUTH in Exchange Online

> [!IMPORTANT]
> **SMTP AUTH is disabled by default** in Microsoft 365 for security. Even with OAuth 2.0, administrators must explicitly enable it.

Microsoft 365 tenants have SMTP authentication disabled by default. You must enable SMTP AUTH either globally or for specific mailboxes before OAuth SMTP will work.

#### Option 1: Enable SMTP AUTH Globally (Recommended for XMPro)

Use this option if XMPro will send emails from multiple mailboxes or if you want a simpler configuration.

1. **Install Exchange Online PowerShell** (if not already installed):

   ```powershell
   Install-Module -Name ExchangeOnlineManagement -Scope CurrentUser
   ```

2. **Connect to Exchange Online**:

   ```powershell
   Connect-ExchangeOnline
   ```

   You'll be prompted to authenticate with your admin credentials.

3. **Enable SMTP AUTH globally**:

   ```powershell
   Set-TransportConfig -SmtpClientAuthenticationDisabled $false
   ```

4. **Verify the setting**:

   ```powershell
   Get-TransportConfig | Format-List SmtpClientAuthenticationDisabled
   ```

   Should return: `SmtpClientAuthenticationDisabled : False`

#### Option 2: Enable SMTP AUTH for Specific Mailbox

Use this option for a more restrictive security posture, enabling SMTP AUTH only for the mailbox XMPro will use.

1. **Connect to Exchange Online** (same as above)

2. **Enable SMTP AUTH for specific mailbox**:

   ```powershell
   Set-CASMailbox -Identity your-email@yourdomain.com -SmtpClientAuthenticationDisabled $false
   ```

   Replace `your-email@yourdomain.com` with the mailbox XMPro will use to send emails.

3. **Verify the setting**:

   ```powershell
   Get-CASMailbox -Identity your-email@yourdomain.com | Format-List SmtpClientAuthenticationDisabled
   ```

   Should return: `SmtpClientAuthenticationDisabled : False`

For detailed instructions, see [Microsoft's official guide on enabling SMTP AUTH](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission).

> [!NOTE]
> **Security Defaults:** If your organization has "Security Defaults" enabled in Azure AD, SMTP AUTH is disabled and cannot be enabled. You must disable Security Defaults first. See [Microsoft Security Defaults documentation](https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults) for more information.

#### Common Error Without This Step

If you skip this step, you'll see this error when attempting to send email:

```text
535 5.7.139 Authentication unsuccessful, SmtpClientAuthentication is disabled for the Tenant
```

**Solution:** Complete this step to enable SMTP AUTH as shown above.

### Step 5: Calculate Token Endpoint URL

Using your Directory (tenant) ID from Step 1, construct the token endpoint URL that XMPro will use to request OAuth tokens.

Your OAuth token endpoint URL follows this format:

```text
https://login.microsoftonline.com/{tenant-id}/oauth2/v2.0/token
```

Replace `{tenant-id}` with your **Directory (tenant) ID** from Step 1.

**Example:**

```text
https://login.microsoftonline.com/12345678-1234-1234-1234-123456789012/oauth2/v2.0/token
```

## XMPro Configuration by Deployment Method

After completing the Azure AD app registration above, configure your XMPro deployment with the OAuth SMTP settings. Choose the section that matches your deployment method.

### Azure Terraform Deployment

Add these variables to your `terraform.tfvars` file:

```hcl
# Enable email notifications (required - defaults to false)
enable_email_notification = true

# Enable OAuth SMTP authentication
enable_email_oauth = true

# OAuth token endpoint (replace {tenant-id} with your Directory tenant ID)
email_oauth_token_endpoint = "https://login.microsoftonline.com/{tenant-id}/oauth2/v2.0/token"

# Azure AD application credentials
email_oauth_token_client_id     = "your-application-client-id"
email_oauth_token_client_secret = "your-client-secret-value"

# OAuth scope (use this exact value for Microsoft 365)
email_oauth_token_scope = "https://outlook.office365.com/.default"

# Basic SMTP settings (still required with OAuth)
email_server          = "smtp.office365.com"
email_server_ssl      = true
email_server_port     = 587
email_username        = "notifications@yourdomain.com"
email_from_address    = "notifications@yourdomain.com"
# Note: email_password is not used when OAuth is enabled
```

> [!NOTE]
> The OAuth configuration applies to both SM and AD automatically in Terraform deployments.

For detailed Terraform configuration, see the <a href="https://github.com/XMPro/terraform-xmpro-azure" target="_blank">Terraform module documentation</a>.

### Windows Server Deployment

#### During Installation

The Windows installer (v4.6+) supports OAuth SMTP configuration during installation:

1. When prompted **"Enable SMTP configuration? (y/n)"**, answer `y`

2. Provide standard SMTP settings:
   - **SMTP Server**: `smtp.office365.com`
   - **SMTP Port**: `587`
   - **Enable SSL**: `y`
   - **SMTP Username**: `notifications@yourdomain.com`
   - **From Email Address**: `notifications@yourdomain.com`

3. When prompted **"Enable OAuth SMTP authentication? (y/n)"**, answer `y`

4. Provide OAuth settings:
   - **OAuth Token Endpoint**: Your token endpoint URL from Azure
   - **OAuth Client ID**: Your Application (client) ID
   - **OAuth Client Secret**: Your client secret value
   - **OAuth Scope**: `https://outlook.office365.com/.default` (default)

#### After Installation (Manual Configuration)

If you need to add or update OAuth SMTP after installation:

1. **Stop XMPro services** (SM and/or AD)

2. **Edit configuration file**:
   - `C:\XMPro\Global-variables.json`

3. **Add or update the `smtp` section** in the file:

```json
{
  "smtp": {
    "enabled": true,
    "server": "smtp.office365.com",
    "port": "587",
    "enableSsl": true,
    "username": "notifications@yourdomain.com",
    "fromAddress": "notifications@yourdomain.com",
    "password": "your-smtp-password",
    "oauth": {
      "enabled": true,
      "tokenEndpoint": "https://login.microsoftonline.com/{tenant-id}/oauth2/v2.0/token",
      "clientId": "your-application-client-id",
      "clientSecret": "your-client-secret-value",
      "scope": "https://outlook.office365.com/.default",
      "tokenMethod": "POST",
      "grantType": "client_credentials"
    }
  }
}
```

1. **Start XMPro services**

> [!TIP]
> Configuration files are located in `C:\XMPro\` by default. The installer preserves these files across reinstalls.

## Testing OAuth SMTP Configuration

After configuring OAuth SMTP in your XMPro deployment, verify the configuration is working correctly by triggering an email and checking application logs for successful OAuth token acquisition and delivery.

### Quick Check

Use the **Forgot Password** flow on the Subscription Manager login page to trigger a test email. If the email is received, OAuth SMTP is configured correctly.

### App Designer (AD)

1. Sign in to XMPro App Designer

2. Create a simple [notification](../concepts/recommendation/notification.md) (or use an existing one)

3. Trigger the notification

4. Verify:
   - Email is received
   - No errors in application logs

### Check Logs

Application logs will show OAuth token acquisition:

**Success:**

```text
[Information] Successfully acquired OAuth token for SMTP authentication
[Information] Email sent successfully to: user@example.com
```

**Failure:**

```text
[Error] Failed to acquire OAuth token: Invalid client secret
[Error] SMTP authentication failed
```

## Troubleshooting

If you encounter issues with OAuth SMTP authentication, this section provides solutions to common problems and guidance on enabling detailed logging for diagnosis. Most issues stem from incorrect Azure AD configuration, expired secrets, or missing Exchange Online permissions. Start by checking the specific error message in your XMPro application logs, then refer to the corresponding solution below.

### Common Issues and Solutions

#### "Insufficient privileges to complete the operation"

**Cause**: API permissions not granted or admin consent not provided

**Solution**:

1. Go to your Azure AD app registration
2. Navigate to **API permissions**
3. Verify **SMTP.SendAsApp** and **Mail.Send** are listed
4. Ensure status shows "Granted for [Your Organization]"
5. If not granted, click **Grant admin consent**

#### "Invalid client secret"

**Cause**: Client secret expired or incorrectly copied

**Solution**:

1. Go to **Certificates & secrets** in your app registration
2. Check if the secret has expired
3. Create a new client secret if expired
4. Update XMPro configuration with the new secret value
5. Restart XMPro services

#### "AADSTS700016: Application with identifier not found"

**Cause**: Incorrect tenant ID in token endpoint URL

**Solution**:

1. Verify the tenant ID in your token endpoint URL
2. Check it matches the **Directory (tenant) ID** in Azure AD
3. Update the endpoint URL in XMPro configuration
4. Restart XMPro services

#### "AADSTS65001: The user or administrator has not consented"

**Cause**: Admin consent not granted for application permissions

**Solution**:

1. Have an Azure AD administrator grant admin consent
2. Navigate to **API permissions** > **Grant admin consent**
3. Wait a few minutes for the change to propagate

#### Emails not sending with OAuth enabled

**Possible causes**:

1. **Email notifications not enabled (Terraform)**: `enable_email_notification` defaults to `false`. Even with all SMTP and OAuth settings configured, emails will not be sent unless `enable_email_notification = true` is set in your `terraform.tfvars`
2. **Email username doesn't match mailbox**: Ensure the email username corresponds to a valid Microsoft 365 mailbox
3. **Mailbox permissions**: The Azure AD app needs permission to send from that mailbox
4. **SMTP AUTH disabled**: Ensure SMTP AUTH is enabled for the mailbox in Exchange Online

**Solution**:

1. Verify the email username in XMPro configuration matches a valid mailbox
2. Test SMTP connectivity using a tool like Telnet or PowerShell
3. Check Exchange Online settings for the mailbox

### Enable Detailed Logging

For Windows Server deployments, enable detailed logging:

1. Edit `C:\XMPro\Global-variables.json`
2. Add or update: `"LOG_LEVEL": "Debug"`
3. Restart the service
4. Check logs in Event Viewer or application log files

For Terraform deployments, set the log level environment variable:

- `log_level = "Debug"` in terraform.tfvars

## Security Best Practices

### Client Secret Management

1. **Use secure storage**:
   - Azure Key Vault (for Azure deployments)
   - Windows Credential Manager (for Windows Server)

2. **Set expiration reminders**:
   - Create calendar alerts for secret expiration
   - Plan to rotate secrets at least 30 days before expiration

3. **Limit access**:
   - Restrict who can view/modify client secrets
   - Use separate app registrations for dev/test/prod environments

### Application Permissions

1. **Principle of least privilege**:
   - Only grant the required permissions (SMTP.SendAsApp, Mail.Send)
   - Don't add additional permissions unless necessary

2. **Regular audits**:
   - Periodically review app permissions
   - Remove unused app registrations

### Monitoring

1. **Set up alerts**:
   - Monitor for SMTP authentication failures
   - Alert on approaching secret expiration

2. **Review logs regularly**:
   - Check for unusual email patterns
   - Monitor OAuth token acquisition errors

## Migration from Basic Auth

If you're currently using Basic Authentication, follow these steps to migrate:

### Before You Begin

1. **Complete Azure AD app registration** (Steps 1-4 above)
2. **Test OAuth configuration** in a non-production environment first
3. **Document current SMTP settings** for rollback if needed

### Migration Steps

1. **Update XMPro configuration** with OAuth settings (keep existing SMTP settings)

2. **Enable OAuth**:
   - Set `ENABLE_EMAIL_OAUTH=true` (or equivalent for your deployment method)

3. **Restart XMPro services**

4. **Test email functionality**:
   - Send test emails from SM
   - Verify notifications work in AD
   - Check logs for OAuth token acquisition

5. **Monitor for 24-48 hours**:
   - Watch for any email failures
   - Review logs for authentication errors

6. **Optional: Remove password** from configuration (for security):
   - Password is not used when OAuth is enabled
   - Can be removed from config files/variables

### Rollback Plan

If issues occur after enabling OAuth:

1. **Set** `ENABLE_EMAIL_OAUTH=false`
2. **Restart XMPro services**
3. **Verify email works with Basic Auth** again
4. **Investigate** the OAuth issue before re-attempting

> [!NOTE]
> Keep Basic Auth configured initially as a fallback. Remove it only after OAuth is proven stable.

## Additional Resources

- [Microsoft Learn: Authenticate SMTP using OAuth](https://learn.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth)
- [Exchange Online SMTP AUTH deprecation](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online)
- [Azure AD app registrations](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)

## Need Help?

If you encounter issues not covered in this guide:

1. **Check XMPro logs** for specific error messages
2. **Review Azure AD app configuration** for missing permissions
3. **Contact XMPro Support** with:
   - XMPro version
   - Deployment method (Terraform, Windows Server)
   - Error messages from logs
   - Steps already attempted
