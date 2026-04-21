# 1. Preparation

Before attempting any of the supported XMPro deployment options (e.g. Cloud, On-Premise), these are the server prerequisites:

* [Hardware Requirements](install.md#hardware-requirements)
* [Software Requirements](install.md#software-requirements)
* [Signing Certificate](install.md#signing-certificate)
* [HTTPS/SSL Certificate](install.md#httpsssl-certificate)
* [SMTP Account](install.md#smtp-account)
* [Twilio Account (Optional)](install.md#twilio-account-optional)

> [!NOTE]
> [**Browser Requirements**](../getting-started/browser-requirements.md)
>
> * Supported Browsers
> * Supported Operating Systems
> * Third-Party Cookies

![Fig 1: The sequence of the 'Prepare to Install XMPro' step within the overall process](../images/installation-preparation.png)

## Hardware and Software Requirements

### Hardware Requirements

For each environment, refer to the [Sizing Guideline](../resources/sizing-guideline.md) guideline to compute resources needed for small, medium, and large deployments:

* Azure
* AWS
* On-Prem

### Software Requirements

This section describes the software that must be installed on the server before installing XMPro (refer [Deploy XMPro](deployment/index.md) section), as well as the software required for the post-installation step of installing a Stream Host.

#### Web Application Servers and SQL Database Server

The following software must be installed on the web application server per product:

<table><thead><tr><th width="466">Software Requirements</th><th width="92">Azure 1</th><th width="74">AWS</th><th>On-Prem</th></tr></thead><tbody><tr><td><strong>Windows Installers</strong></td><td></td><td></td><td></td></tr><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet-framework/net481">Microsoft .NET Framework 4.8.1 Runtime</a></td><td>No</td><td>No</td><td>Yes</td></tr><tr><td><strong>Subscription Manager (SM) Web Application Server</strong></td><td></td><td></td><td></td></tr><tr><td>Windows Server 2022</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet-framework/net48">Microsoft .NET Framework 4.8 Runtime</a></td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td>Microsoft Internet Information Services (IIS) 10</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://www.iis.net/downloads/microsoft/url-rewrite">IIS URL Rewrite 2.1</a></td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><strong>Application Designer (AD) Web Application Server</strong></td><td></td><td></td><td></td></tr><tr><td>Windows Server 2022</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet/8.0">Microsoft ASP.NET Core Runtime 8 (Hosting Bundle)</a></td><td>No</td><td>No</td><td>Yes</td></tr><tr><td>Microsoft Internet Information Services (IIS) 10</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://www.iis.net/downloads/microsoft/url-rewrite">IIS URL Rewrite 2.1</a></td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><strong>Data Stream Designer (DS)</strong> <strong>Web Application Server</strong></td><td></td><td></td><td></td></tr><tr><td>Windows Server 2022</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet/8.0">Microsoft ASP.NET Core Runtime 8 (Hosting Bundle)</a></td><td>No</td><td>No</td><td>Yes</td></tr><tr><td>Microsoft Internet Information Services (IIS) 10</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><a href="https://www.iis.net/downloads/microsoft/url-rewrite">IIS URL Rewrite 2.1</a></td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td><strong>SQL Database Server (Combined SM, AD, DS)</strong></td><td></td><td></td><td></td></tr><tr><td>Windows Server 2019 or 2022</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr><td>Microsoft SQL Server 2019 or 2022</td><td>Yes</td><td>Yes</td><td>Yes</td></tr></tbody></table>

> [!NOTE]
> **Footnotes**
>
> **1** As per the ARM template for your Azure instance.

#### Stream Host Server

The following software must be installed on the Stream Host server:

<table data-full-width="false"><thead><tr><th width="266">Software Requirements</th><th width="122">Windows</th><th width="141">Azure Web Job</th><th width="111">Ubuntu </th><th>Docker</th></tr></thead><tbody><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-aspnetcore-8.0.3-windows-x64-installer">ASP.NET Core Runtime 8.0.3</a></td><td>No <strong>1</strong></td><td>Yes <strong>2</strong></td><td>Yes <strong>3</strong></td><td>No</td></tr><tr><td><a href="https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-8.0.3-windows-x64-installer">.NET Runtime 8.0.3</a></td><td>No <strong>1</strong></td><td>Yes <strong>2</strong></td><td>Yes <strong>3</strong></td><td>No</td></tr></tbody></table>

> [!NOTE]
> **Footnotes**
>
> **1** Not a prerequisite from v4.4.1+.\
> **2** As per the ARM template for your Azure instance.\
> **3** See the Ubuntu documentation for installing [ASP.NET Core Runtime](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu) and [.NET Runtime](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu) on Ubuntu.

## Certificate and Communication Steps

### Signing Certificate

Subscription Manager manages Identity and access for the whole XMPro Platform. To do this, it regularly issues authentication tokens to the users as they log into the system. The server must sign these tokens to ensure their validity, hence a signing certificate is required.

A PKCS 12 archived certificate .pfx file is required. The minimum length of the accepted private key is 2048. Follow the instructions below to generate a Signing certificate:

* Download and install [OpenSSL for Windows](http://www.slproweb.com/products/Win32OpenSSL.html)
* Open a command prompt as administrator and navigate to the OpenSSL install directory. The default location is `C:\Program Files\OpenSSL-Win64`
* Run the following commands

```
cd C:\Program Files\OpenSSL-Win64
cd bin
openssl genrsa -out sign.pem 2048
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout sign.key -out sign.crt -subj "/CN={YourMachine}" -days 3650
openssl pkcs12 -export -out sign.pfx -inkey sign.key -in sign.crt -certfile sign.crt
```

* Follow the prompts on the screen and complete the certificate request
* Make a note of the _Common Name ("/CN='')_ and _Password_ you choose
* Create a file called _sign.password.txt_ and add the password to the file

> [!NOTE]
> The resulting _sign.pfx_ and _sign.password.txt_ files will be required during the installation.

### HTTPS/SSL Certificate

The XMPro Platform enforces secure communication using HTTPS/SSL. This means the server it is deployed to must have HTTPS configured. Depending on the deployment option you choose, you may have the following options:

* Order a certificate from a certificate authority (CA)
* Create a certificate in AWS (AWS deployment only)
* Create a self-signed certificate (On-Premise only)

> [!NOTE]
> The DNS or hostname that users are expected to use to browse to the XMPro Platform must correspond to the SSL Certificate Common Name.

#### Creating Self-Signed Certificate through PowerShell

If you need to create a self-signed certificate, open Windows PowerShell as administrator and follow the instructions below:

1. Create SSL certificate with proper extensions, replacing "yourdomain.com" with your actual domain:

```powershell
# Create SSL certificate with proper extensions
$cert = New-SelfSignedCertificate `
    -Subject "CN=yourdomain.com" `
    -DnsName @("yourdomain.com", "www.yourdomain.com", "localhost") `
    -KeyLength 4096 `
    -KeyAlgorithm RSA `
    -HashAlgorithm SHA256 `
    -KeyExportPolicy Exportable `
    -KeyUsage DigitalSignature, KeyEncipherment `
    -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") `
    -NotAfter (Get-Date).AddYears(1)
```

1. Export to PFX with a strong password:

```powershell
# Export to PFX
$password = ConvertTo-SecureString -String "YourStrongPassword" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath "c:\ssl-cert.pfx" -Password $password
```

1. Clean up the certificate from the local store (optional):

```powershell
# Clean up
Remove-Item -Path "Cert:\LocalMachine\My\$($cert.Thumbprint)"
```

> [!NOTE]
> The directory you specify in step 2's `-FilePath` parameter must already exist.

1. Create a txt file with the name _cert.password.txt_ and add the certificate password to this file.

> [!WARNING]
> **Troubleshooting Self-Signed Certificate Issues**
>
> If the Subscription Manager installer reports certificate validation errors with PowerShell-generated certificates:
>
> 1. **Enhanced Security Parameters**: The updated certificate command includes improved security settings (4096-bit RSA, SHA256 hash, proper key usage) that resolve most compatibility issues with the SM installer.
> 2. **Extended Key Usage**: The certificate includes both Server Authentication (`1.3.6.1.5.5.7.3.1`) and Client Authentication (`1.3.6.1.5.5.7.3.2`) extensions as shown in the command above.
> 3. **Certificate Validation**: Verify the certificate was created correctly by running:
>
>    ```powershell
>    Get-ChildItem -Path cert:\LocalMachine\My | Where-Object {$_.Subject -like "*yourdomain.com*"}
>    ```
>
> 4. **File Permissions**: Ensure the exported `.pfx` file and `.password.txt` file have appropriate read permissions.
> 5. **Certificate Store**: If you didn't run the cleanup command in step 3, the certificate will remain in the LocalMachine\My store, which is normal and expected.

#### Creating Self-Signed Certificate through IIS

The self-signed certificate can also be generated through IIS, following the instructions below:

1. Open IIS Manager and click "Server Certificates"

![Fig 2: Creating a Self-Signed Certificate through IIS](../images/iis-manager.png)

1. Click "Create Self-Signed Certificate"

![Fig 3: Click "Create Self-Signed Certificate"](../images/installation-preparation-server-cert2.png)

1. Enter "cert" for the Certificate name, select "Personal" for the certificate store, and click OK

![Fig 4: Enter a friendly name](../images/installation-preparation-server-cert3.png)

1. Confirm the certificate is generated and listed on 'Server Certificates'
2. Right click on the certificate and Export, taking note of the location and password entered for later use

### SMTP Account

XMPro components use emails to notify users of certain events, for instance, a new User signed up, or your account is ready. Please set up an SMTP account and have the necessary server details, as these are required for the notifications to work.

1. **TLS/SSL Security**
   * TLS encryption is required for secure email transmission
   * Use port 587 (STARTTLS) for modern secure email delivery
   * Enable SSL must be set to "true" in configuration
2. **Account Configuration** You will need the following details from your email provider:

<table><thead><tr><th width="120">Setting</th><th width="265">Value</th><th>Description</th></tr></thead><tbody><tr><td>Smtp Server</td><td>Your provider's SMTP server address</td><td>The fully qualified domain name of your SMTP server (e.g. smtp.office365.com)</td></tr><tr><td>User Name</td><td>Your SMTP account username</td><td>Often the same as your email address (e.g. noreply@mydomain.com)</td></tr><tr><td>Password</td><td>Your SMTP account password</td><td>Secure authentication credentials</td></tr><tr><td>Port</td><td>587</td><td>Required for TLS (STARTTLS) encryption</td></tr><tr><td>Enable SSL</td><td>true</td><td>Must be enabled for secure transmission</td></tr></tbody></table>

### Twilio Account (Optional)

App Designer uses SMS, among other means, to notify users of certain events e.g. a recommendation alert was triggered or resolved, etc. An SMS provider is required to send SMS notifications.

Please set up an account at Twilio using these [instructions](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account) and have the necessary details handy, i.e. Account ID, Authorization Token, and the Phone Number.
