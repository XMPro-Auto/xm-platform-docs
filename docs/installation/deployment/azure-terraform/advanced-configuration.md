# Advanced Configuration

This page covers optional features that are automatically configured in your XMPro deployment. Most users don't need to change these settings.

## Health Monitoring (Automatically Configured)

Health monitoring is automatically enabled for all XMPro services. No configuration needed!

### What's Included

✅ **Real-time health checks** - Services monitor each other automatically  
✅ **Health dashboard** - Visual status at `/health-ui` on App Designer and Data Stream Designer  
✅ **Application Insights** - Full monitoring and alerting in Azure Portal

### Viewing Health Status

**Option 1: Health Dashboard (Recommended)**

Access the built-in health dashboard UI:

- App Designer: `https://ad-yourcompany.azurewebsites.net/health-ui`
- Data Stream Designer: `https://ds-yourcompany.azurewebsites.net/health-ui`

This provides a visual dashboard showing the real-time status of all components.

**Option 2: Application Insights**

For detailed monitoring and historical data:

1. Go to Azure Portal
2. Open your resource group
3. Click on Application Insights
4. View the Application Map to see all services and dependencies

**Option 3: Direct API Endpoints**

For programmatic access or troubleshooting:

- App Designer: `https://ad-yourcompany.azurewebsites.net/health`
- Data Stream Designer: `https://ds-yourcompany.azurewebsites.net/health`
- Subscription Manager: `https://sm-yourcompany.azurewebsites.net/version`

## Logging (Automatically Configured)

All logging is automatically set up. No configuration needed!

### What's Included

✅ **Application Insights** - Logs and metrics for App Designer (AD) and Data Stream Designer (DS)  
✅ **File-based logging** - Subscription Manager (SM) logs to files via Serilog  
✅ **Log Analytics** - Query and analyze Application Insights data

### Viewing Logs

**For AD and DS (Application Insights):**

1. Go to your resource group in Azure Portal
2. Click on Application Insights
3. Click "Logs" to search logs
4. Click "Failures" to see errors

**For SM (File Logs):**

1. Go to your SM App Service in Azure Portal
2. Navigate to Advanced Tools (Kudu)
3. Browse to `C:\home\LogFiles\Application\`
4. View the `sm-log-*.txt` files

> [!TIP]
> Need help with specific log types? See:
>
> - [Data Stream Logs](../../../how-tos/data-streams/check-data-stream-logs.md)
> - [Connector Logs](../../../how-tos/apps/check-connector-logs.md)

## SMTP Email Configuration

XMPro supports email notifications for password resets, user invitations, and system alerts. Configure SMTP in your `terraform.tfvars` file.

### Basic SMTP Configuration

Add these variables to enable email notifications:

```hcl
# Enable email notifications (required - defaults to false)
enable_email_notification = true

# SMTP server settings
email_server     = "smtp.gmail.com"  # or smtp.office365.com
email_server_ssl = true
email_server_port = 587

# Email credentials
email_username     = "notifications@yourcompany.com"
email_password     = "your-smtp-password"
email_from_address = "notifications@yourcompany.com"
```

> [!NOTE]
> SMTP is required for password resets and user invitations. Without SMTP configured, users cannot reset forgotten passwords or receive invitation emails.

### OAuth SMTP Configuration (Microsoft 365)

> [!IMPORTANT]
> **Microsoft 365 Users:** Microsoft is deprecating Basic Authentication for SMTP by **March 2026**. You must configure OAuth 2.0 authentication to continue using Microsoft 365 SMTP.

For Microsoft 365 or Office 365 SMTP, use OAuth 2.0 authentication:

```hcl
# Enable email notifications (required - defaults to false)
enable_email_notification = true

# Enable OAuth SMTP
enable_email_oauth = true

# OAuth token endpoint (replace {tenant-id} with your Azure AD tenant ID)
email_oauth_token_endpoint = "https://login.microsoftonline.com/{tenant-id}/oauth2/v2.0/token"

# Azure AD application credentials
email_oauth_token_client_id     = "your-application-client-id"
email_oauth_token_client_secret = "your-client-secret-value"

# OAuth scope (use this exact value for Microsoft 365)
email_oauth_token_scope = "https://outlook.office365.com/.default"

# Basic SMTP settings (still required with OAuth)
email_server       = "smtp.office365.com"
email_server_ssl   = true
email_server_port  = 587
email_username     = "notifications@yourcompany.com"
email_from_address = "notifications@yourcompany.com"
# Note: email_password is not used when OAuth is enabled
```

> [!NOTE]
> **Prerequisites for OAuth SMTP:** Before configuring OAuth, you must create an Azure AD app registration with SMTP.SendAsApp and Mail.Send permissions.
>
> See the complete [OAuth SMTP Configuration Guide](../../../technical-reference/oauth-smtp-configuration.md) for step-by-step Azure AD setup instructions.

### Additional SMTP Settings

For more advanced SMTP configuration options, see the <a href="https://github.com/XMPro/terraform-xmpro-azure#smtp-configuration" target="_blank">Terraform module SMTP documentation</a>.

## Production Considerations

For production deployments, you may want to:

- **Set up alerts** in Application Insights for errors or performance issues
- **Configure backups** for your SQL databases
- **Review security settings** in Azure Portal
- **Set up custom domains** (see <a href="https://github.com/XMPro/terraform-xmpro-azure#dns-and-domain-configuration" target="_blank">GitHub documentation</a>)

> [!NOTE]
> For all other advanced configurations like SMTP, custom domains, and production settings, see the <a href="https://github.com/XMPro/terraform-xmpro-azure" target="_blank">complete module documentation</a>.
