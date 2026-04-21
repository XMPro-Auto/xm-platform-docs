# Troubleshooting

This guide helps you resolve common issues when installing XMPro on Windows Server 2022.

> [!TIP]
> **Quick fixes that solve most issues:**
>
> - Restart IIS: `iisreset /restart`
> - Restart SQL Server: `Restart-Service MSSQLSERVER`
> - Check Windows Firewall is not blocking ports 443, 5202, 5203, 1433
> - Verify you're running PowerShell as Administrator
> - **View Application Logs:** Check [XMPro Log Events documentation](../../../technical-reference/xmpro-log-events/index.md) for log file locations and troubleshooting guidance

## Installation Issues

### Installer Script Execution Blocked

**Error:**

```text
.\install-xmpro-application.ps1 : File cannot be loaded because running scripts is disabled on this system.
```

**Solution:**

```powershell
# Run PowerShell as Administrator, then:
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process -Force

# Then run installer:
.\install-xmpro-application.ps1
```

### Prerequisites Not Met

**Error:**

```text
Validation failed: IIS is not installed
```

**Solution:**
Check the [Prerequisites](index.md#prerequisites) and install missing components:

- IIS with required features
- .NET Framework 4.8
- .NET 8 Hosting Bundle
- SQL Server
- Certificates

**Quick check:**

```powershell
# Verify IIS
Get-Service W3SVC

# Verify .NET 8
dotnet --list-runtimes

# Verify SQL Server
Get-Service MSSQLSERVER
```

### Configuration File Missing

**Error:**

```text
Global-variables.json not found
```

**Solution:**

If running application installer for the first time:

```powershell
# Create configuration directory
New-Item -Path "C:\XMPro" -ItemType Directory -Force

# Run installer (will create configuration)
.\install-xmpro-application.ps1
```

If configuration was accidentally deleted:

- The installer will recreate it during first run
- You'll need to re-enter all configuration values

### Installation Failure Recovery

**If installation fails on any server:**

1. **Resolve the underlying issue** - See relevant troubleshooting sections below for your specific error
2. **Re-run the installer:**

   ```powershell
   .\install-xmpro-application.ps1
   ```

The installer will:

- Completely reinstall IIS applications
- Preserve database data (migration is idempotent)
- Use existing configuration from C:\XMPro

## Database Issues

### Cannot Connect to SQL Server

**Error:**

```text
A network-related or instance-specific error occurred while establishing a connection to SQL Server
```

**Common causes and solutions:**

**1. SQL Server service not running:**

```powershell
# Check service status
Get-Service MSSQLSERVER

# Start service if stopped
Start-Service MSSQLSERVER
```

**2. TCP/IP protocol disabled:**

```powershell
# Enable TCP/IP using SQL Server Configuration Manager
# Or PowerShell:
$wmi = New-Object Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer
$tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
$tcp.IsEnabled = $true
$tcp.Alter()

# Restart SQL Server
Restart-Service MSSQLSERVER
```

**3. Firewall blocking SQL Server:**

```powershell
# Allow SQL Server through firewall
New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433 -Action Allow
```

**4. Wrong credentials:**

```powershell
# Test SQL Server connection
sqlcmd -S hostname -U sa -P YourPassword

# If this fails, verify:
# - Username is correct (default: sa)
# - Password is correct
# - Mixed Mode Authentication is enabled
```

### SQL Server Certificate Trust Error

**Symptoms:**

- Application fails to start or connect to database
- Event Viewer shows SQL connection errors
- Error message mentioning "certificate chain" or "trust relationship"

**Error Example:**

```text
A connection was successfully established with the server, but then an error occurred during the login process.
(provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

**Root Cause:**
The web server does not trust the SQL Server's SSL/TLS certificate.

**Solutions:**

#### Production Environment (Recommended)

Configure the Windows Server to trust the SQL Server certificate by following Microsoft's official documentation:

**See:** [SQL Server Certificate Procedures - Export and Import Certificates](https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/certificate-procedures?view=sql-server-ver17)

After importing the certificate, restart IIS:

```powershell
iisreset
```

#### Non-Production Environment (Quick Fix)

Rerun the installer and answer `Y` (Yes) when prompted "Trust SQL Server Certificate?":

```cmd
powershell.exe -ExecutionPolicy Bypass -Command "$env:SCRIPT_URL='https://download.app.xmpro.com/5.0.0-alpha/install-xmpro-application.ps1'; iex (irm $env:SCRIPT_URL)"
```

When prompted, select:

- **Trust SQL Server Certificate**: `Y` (Yes)
- Keep all other settings the same as your original installation

> [!WARNING]
> Setting "Trust SQL Server Certificate" to `Y` disables certificate validation and should only be used in non-production environments.

**Reference:** [TrustServerCertificate Documentation](https://learn.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.trustservercertificate)

### Database Migration Fails

**Error:**

```text
Database migration failed for SM database
```

**Solutions:**

**Check database connection:**

```powershell
# Test connection with credentials from installer
sqlcmd -S your-hostname -U sa -P YourPassword -Q "SELECT @@VERSION"
```

**Check disk space:**

```powershell
# Verify enough disk space for databases
Get-PSDrive C | Select-Object Used,Free
```

**Check SQL Server error logs:**

```powershell
# View SQL Server error log
Get-Content "C:\Program Files\Microsoft SQL Server\MSSQL16.MSSQLSERVER\MSSQL\Log\ERRORLOG"
```

**Manual database creation test:**

```powershell
sqlcmd -S hostname -U sa -P YourPassword
# At prompt, type:
CREATE DATABASE TestDB
GO
DROP DATABASE TestDB
GO
# If this fails, SQL Server has permission or configuration issues
```

### Database Creation Timeout

**Error:**

```text
Unhandled exception. Microsoft.Data.SqlClient.SqlException (0x80131904): Execution Timeout Expired. The timeout period elapsed prior to completion of the operation or the server is not responding.
CREATE DATABASE operation failed. Internal service error.
Operation cancelled by user.
Error Number:-2,State:0,Class:11
SM/AD/DS database migration failed: database migration failed with exit code -532462766
Installation failed: database migration failed with exit code -532462766
```

**What's happening:**

- SQL Server is creating the database in the background
- The migration tool times out before the database creation completes
- The database will eventually be created successfully, but the installer exits with an error

**Root Cause:**
Database provisioning takes longer than the migration tool's timeout period.

**Solutions:**

#### Option 1: Rerun the Installer

Simply rerun the installation script. The database has been created in the background and the installer will detect it exists and continue with the migration:

```cmd
powershell.exe -ExecutionPolicy Bypass -Command "$env:SCRIPT_URL='https://download.app.xmpro.com/5.0.0-alpha/install-xmpro-application.ps1'; iex (irm $env:SCRIPT_URL)"
```

> [!NOTE]
> You may encounter this timeout for each database (SM, AD, DS) during first-time installation. Simply rerun the installer each time until all databases are created and migrated successfully.

#### Option 2: Manually Create Databases Before Installation

Create the databases manually using your SQL admin account (e.g., `xmadmin`) before running the installer:

```sql
-- Connect to Azure SQL Database using your admin account
-- Example using Azure Data Studio or SQL Server Management Studio

-- Create databases
CREATE DATABASE SM;
CREATE DATABASE AD;
CREATE DATABASE DS;
```

Then run the installer normally. It will detect the databases exist and proceed with the migration.

### Database Already Exists Warning

**Message:**

```text
We've noticed that the SM database 'SM' already exists (45 tables found)
Please ensure that you've performed a backup before proceeding
```

**What this means:**

- Installer detected existing XMPro database
- Database migration will modify/upgrade existing data

**Solutions:**

#### Option 1: Backup and continue (recommended for upgrades)

```powershell
# Backup existing database first
sqlcmd -S hostname -U sa -P YourPassword -Q "BACKUP DATABASE SM TO DISK='C:\Backup\SM.bak'"

# Then press Enter in installer to continue
```

#### Option 2: Use different database name

- Cancel installer (Ctrl+C)
- Re-run with custom database name:

  ```text
  SM Database Name: SM_New
  ```

### Data Stream Designer Database Errors

**Problem:** "Violation of PRIMARY KEY constraint" errors during Data Stream Designer startup

**Solution:**

1. Restart IIS using `iisreset /restart`

2. If errors persist, check SQL database for corruption or manually resolve conflicts

3. Verify DS database integrity:

```powershell
# Check for duplicate keys or data issues
sqlcmd -S hostname -U sa -P YourPassword -d DS -Q "DBCC CHECKDB (DS)"
```

1. If database corruption is detected, restore from backup or re-run database migration:

```powershell
# Re-run DS database migration
.\install-xmpro-application.ps1 -Products @('DS')
```

## IIS Configuration Issues

### IIS Application Pool Not Starting

**Error:** Application pool stops immediately after starting

**Check event logs:**

```powershell
# View Application event log
Get-EventLog -LogName Application -Newest 50 | Where-Object {$_.Source -like "*IIS*"}
```

**Common causes:**

**1. .NET runtime not installed:**

```powershell
# Verify .NET 8 Hosting Bundle
dotnet --list-runtimes | Select-String "Microsoft.AspNetCore.App 8"

# If missing, download and install:
# https://dotnet.microsoft.com/en-us/download/dotnet/8.0
```

**2. Application pool identity permissions:**

```powershell
# Reset application pool identity
Import-Module WebAdministration
Set-ItemProperty IIS:\AppPools\XMPro-SM -Name processModel.identityType -Value ApplicationPoolIdentity
Restart-WebAppPool -Name "XMPro-SM"
```

**3. Port conflict:**

```powershell
# Check if port is already in use
netstat -ano | findstr ":443"
netstat -ano | findstr ":5202"
netstat -ano | findstr ":5203"

# If port is in use, you can:
# - Stop the conflicting application
# - Change XMPro application port in IIS Manager
```

### Cannot Access XMPro Application

**Problem:** Browser shows "This site can't be reached" or connection timeout

**Solutions:**

**1. Check Windows Firewall:**

```powershell
# Allow inbound connections on XMPro ports
New-NetFirewallRule -DisplayName "XMPro SM" -Direction Inbound -Protocol TCP -LocalPort 443 -Action Allow
New-NetFirewallRule -DisplayName "XMPro AD" -Direction Inbound -Protocol TCP -LocalPort 5202 -Action Allow
New-NetFirewallRule -DisplayName "XMPro DS" -Direction Inbound -Protocol TCP -LocalPort 5203 -Action Allow
```

**2. Verify IIS bindings:**

```powershell
# Check IIS site bindings
Import-Module WebAdministration
Get-WebBinding -Name "XMPro-SM"
Get-WebBinding -Name "XMPro-AD"
Get-WebBinding -Name "XMPro-DS"
```

**3. Test from localhost first:**

```powershell
# Test connection from server itself
Invoke-WebRequest -Uri "https://localhost/" -UseBasicParsing
Invoke-WebRequest -Uri "https://localhost:5202/" -UseBasicParsing
Invoke-WebRequest -Uri "https://localhost:5203/" -UseBasicParsing
```

**4. Check application is running:**

```powershell
# Verify application pools are started
Get-IISAppPool | Where-Object {$_.Name -like "XMPro*"} | Select-Object Name, State
```

### HTTP Error 500.19 - Configuration Error

**Error:**

```text
HTTP Error 500.19 - Internal Server Error
Cannot read configuration file
```

**Solutions:**

**1. IIS URL Rewrite module not installed:**

```powershell
# Download and install:
# https://www.iis.net/downloads/microsoft/url-rewrite

# Verify installation:
Get-WebConfiguration -Filter "system.webServer/rewrite/rules"
```

**2. web.config file corrupted:**

```powershell
# Check web.config exists and is readable
Test-Path "C:\inetpub\wwwroot\XMPro-SM\web.config"

# View web.config for XML errors
Get-Content "C:\inetpub\wwwroot\XMPro-SM\web.config"
```

**3. File permissions:**

```powershell
# Grant IIS_IUSRS read access to application directory
$acl = Get-Acl "C:\inetpub\wwwroot\XMPro-SM"
$rule = New-Object System.Security.AccessControl.FileSystemAccessRule("IIS_IUSRS","ReadAndExecute","ContainerInherit,ObjectInherit","None","Allow")
$acl.SetAccessRule($rule)
Set-Acl "C:\inetpub\wwwroot\XMPro-SM" $acl
```

### HTTP Error 404.15 - Request URL Too Long

**Error:** Request URL too long error when accessing XMPro applications

**Solution:**

You need to make two changes to fix this issue:

1. Increase the httpRuntime maxQueryStringLength and maxUrlLength in the system.web section
2. Add requestFiltering settings in the system.webServer section

**Steps:**

1. Navigate to `C:\inetpub\wwwroot\XMPro-SM` and open `web.config` in a text editor

2. Update the httpRuntime line in the system.web section:

```xml
<!-- Find this line -->
<httpRuntime targetFramework="4.8" maxUrlLength="1024" />

<!-- Change it to this -->
<httpRuntime targetFramework="4.8" maxUrlLength="8192" maxQueryStringLength="8192" />
```

1. Repeat for AD and DS web.config files:
   - `C:\inetpub\wwwroot\XMPro-AD\web.config`
   - `C:\inetpub\wwwroot\XMPro-DS\web.config`

2. Restart IIS:

```powershell
iisreset /restart
```

### HTTP Error 400 - Bad Request (Request Too Long)

**Error:** HTTP 400 error due to large request headers

**Solution:**

This issue requires registry changes to increase HTTP.sys limits:

1. Open Registry Editor by pressing Win+R, typing "regedit" and pressing Enter

2. Navigate to: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters`

3. Look for these two registry keys:
   - `MaxFieldLength`
   - `MaxRequestBytes`

4. If they don't exist, create them as DWORD (32-bit) values:
   - Right-click in the right pane and select "New" → "DWORD (32-bit) Value"

5. Name the first value `MaxFieldLength`:
   - Double-click it to edit
   - Select "Decimal" as the base
   - Enter a value of 65536 (or higher if needed)
   - Click OK

6. Right-click again and add a second DWORD value:
   - Name it `MaxRequestBytes`
   - Double-click to edit
   - Select "Decimal" as the base
   - Enter a value of 65536 (or higher if needed)
   - Click OK

7. After adding or modifying these values, restart HTTP service and IIS:

```cmd
net stop http /y
net start http
iisreset
```

> [!WARNING]
> Stopping the HTTP service will temporarily interrupt all IIS websites and services on the server.

## Certificate Issues

### Browser Shows Certificate Warning

**Warning:** "Your connection is not private" or "NET::ERR_CERT_AUTHORITY_INVALID"

**Cause:** Self-signed certificate not trusted by browser

**Solutions:**

**Option 1: Trust the certificate (for testing):**

1. In browser, click "Advanced"
2. Click "Proceed to hostname (unsafe)"
3. Certificate will be trusted for this session

**Option 2: Install root certificate in browser:**

```powershell
# Export root certificate
Export-Certificate -Cert (Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Subject -like "*XMPro Root CA*"}) -FilePath "C:\XMPro\XMProRootCA.cer"

# Manually import to browser:
# - Open certificate file
# - Install to "Trusted Root Certification Authorities"
```

**Option 3: Use production certificate (recommended):**

- Obtain certificate from trusted Certificate Authority
- Import to Windows Certificate Store
- Update IIS bindings to use new certificate

### Certificate Private Key Not Accessible

**Error:**

```text
Cannot access private key for certificate
```

**Solution:**

```powershell
# Grant IIS application pool permission to certificate private key

# Find certificate thumbprint
Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Subject -like "*hostname*"}

# Grant permission using certificate MMC:
# 1. Run: certlm.msc
# 2. Navigate to Personal > Certificates
# 3. Right-click certificate > All Tasks > Manage Private Keys
# 4. Add "IIS AppPool\XMPro-SM" with Read permission
# 5. Repeat for AD and DS application pools
```

### JWT Token Signing Certificate Error

**Error:**

```text
Failed to load signing certificate for JWT tokens
```

**Solution:**

```powershell
# Verify JWT certificate exists
Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Subject -like "*JWT*"}
```

**If certificate is missing, create a new signing certificate:**

```powershell
# Configuration
$certPath = "C:\XMPro\Certificates\sign.crt"
$pfxPath = "C:\XMPro\Certificates\sign.pfx"
$certPassword = "xmpro123"  # Change this to a secure password

# Create directory if needed
New-Item -Path "C:\XMPro\Certificates" -ItemType Directory -Force | Out-Null

# Create self-signed certificate
$cert = New-SelfSignedCertificate -Subject "CN=sm" `
    -KeyLength 4096 -KeyAlgorithm RSA -HashAlgorithm SHA256 `
    -NotAfter (Get-Date).AddYears(1) `
    -CertStoreLocation "Cert:\LocalMachine\My" `
    -KeyUsage DigitalSignature -KeyExportPolicy Exportable -KeySpec KeyExchange

# Export certificate files
$securePassword = ConvertTo-SecureString -String $certPassword -Force -AsPlainText
Export-Certificate -Cert $cert -FilePath $certPath -Type CERT | Out-Null
Export-PfxCertificate -Cert $cert -FilePath $pfxPath -Password $securePassword | Out-Null

# Remove from store (we only need the files)
Remove-Item -Path "Cert:\LocalMachine\My\$($cert.Thumbprint)" -Force

Write-Host "Signing certificate created at: $pfxPath"
Write-Host "Password: $certPassword"
```

**Update configuration to use the new certificate:**

```powershell
# Update appsettings.json with correct certificate path
$config = Get-Content "C:\inetpub\wwwroot\XMPro-SM\appsettings.json" | ConvertFrom-Json
$config.JwtSettings.CertificatePath
# Should point to: C:\XMPro\Certificates\sign.pfx
```

## SMTP Configuration Issues

### Email Not Sending

**Problem:** Password reset emails, notifications not being sent

**Check SMTP configuration:**

**1. Verify SMTP settings in configuration:**

```powershell
# Check Global-variables.json
Get-Content "C:\XMPro\Global-variables.json" | ConvertFrom-Json | Select-Object -ExpandProperty database | Select-Object -ExpandProperty smtp
```

**2. Test SMTP connection:**

```powershell
# Test SMTP server connectivity
Test-NetConnection -ComputerName smtp.example.com -Port 587

# Send test email
Send-MailMessage -From "test@example.com" -To "test@example.com" `
  -Subject "Test" -Body "Test" `
  -SmtpServer "smtp.example.com" -Port 587 `
  -UseSsl -Credential (Get-Credential)
```

**3. Check IIS environment variables:**

```powershell
# Verify EMAIL_* environment variables set for SM application
Get-WebConfigurationProperty -PSPath "IIS:\Sites\XMPro-SM" -Filter "system.webServer/aspNetCore" -Name "environmentVariables"
```

**4. Common SMTP issues:**

| Issue | Solution |
| --- | --- |
| **Port blocked** | Check firewall allows outbound on port 587 or 465 |
| **Authentication failed** | Verify username/password, may need app-specific password (Gmail) |
| **TLS/SSL error** | Ensure `enableSsl: true` for port 587, check TLS version support |
| **Relay denied** | SMTP server must allow relay from Windows Server IP |

**5. Re-configure SMTP:**

```powershell
# Edit Global-variables.json and re-run installer
.\install-xmpro-application.ps1 -SkipDatabaseMigration
```

## Stream Host Service Issues

### Stream Host Service Won't Start

**Error:** StreamHost-{hostname} service fails to start

**Check service status:**

```powershell
# Get Stream Host service name
$serviceName = Get-Service | Where-Object {$_.Name -like "StreamHost*"} | Select-Object -ExpandProperty Name

# Check service status
Get-Service $serviceName

# View service error
Get-EventLog -LogName Application -Source $serviceName -Newest 10
```

**Common causes:**

**1. CollectionId or Secret missing:**

```powershell
# Verify Global-settings.json contains collection info
Get-Content "C:\XMPro\Global-settings.json" | ConvertFrom-Json | Select-Object CollectionId, CollectionSecret

# If missing, DS database migration failed
# Re-run installer with DS selected
```

**2. Cannot connect to DS:**

```powershell
# Test DS connectivity
Invoke-WebRequest -Uri "https://hostname:5203/version" -UseBasicParsing

# Check Stream Host config file
Get-Content "C:\Program Files\XMPro\StreamHost\appsettings.json"
# Verify DataStreamDesignerUrl is correct
```

**3. Permission issues:**

```powershell
# Stream Host service runs as NetworkService by default
# Grant NetworkService access to installation directory
$acl = Get-Acl "C:\Program Files\XMPro\StreamHost"
$rule = New-Object System.Security.AccessControl.FileSystemAccessRule("NT AUTHORITY\NetworkService","FullControl","ContainerInherit,ObjectInherit","None","Allow")
$acl.SetAccessRule($rule)
Set-Acl "C:\Program Files\XMPro\StreamHost" $acl
```

**4. Reinstall Stream Host:**

```powershell
# Uninstall service
$serviceName = Get-Service | Where-Object {$_.Name -like "StreamHost*"} | Select-Object -ExpandProperty Name
Stop-Service $serviceName
sc.exe delete $serviceName

# Re-run installer
.\install-xmpro-application.ps1 -Products @('SH')
```

## Authentication and Login Issues

### Cannot Login with Admin Credentials

**Problem:** Login fails with correct username/password

**Solutions:**

**1. Verify credentials:**

- Username format: `admin@xmpro.onxmpro.com` (super admin) or `firstname.lastname@companyname.onxmpro.com` (company admin)
- Password: Must meet complexity requirements (8+ chars, uppercase, lowercase, number, special char)

**2. Check SM application is running:**

```powershell
# Verify SM application pool
Get-IISAppPool -Name "XMPro-SM" | Select-Object Name, State

# Restart if stopped
Start-WebAppPool -Name "XMPro-SM"
```

**3. Check SM database:**

```powershell
# Verify SM database exists and has data
sqlcmd -S hostname -U sa -P YourPassword -Q "SELECT TOP 5 * FROM SM.dbo.Users"
```

**4. Reset admin password (if forgotten):**

```powershell
# Contact XMPro Support for password reset procedure
# Or re-run database migration (will reset passwords)
.\install-xmpro-application.ps1 -SkipPrompts
# Select SM for migration
```

### 401 Unauthorized After Login

**Problem:** Login succeeds but redirects show 401 Unauthorized

**Cause:** OIDC (OpenID Connect) hostname case sensitivity issue

**Solution:**

```powershell
# Check hostname case
[System.Net.Dns]::GetHostName()

# Hostname must be lowercase in all configurations
# Edit Global-variables.json if needed and re-run installer
```

## Performance and Stability Issues

### High CPU Usage

**Check which process:**

```powershell
# Identify top CPU consumers
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 Name, CPU, Id
```

**Common causes:**

- **w3wp.exe**: IIS worker process (normal during data processing)
- **sqlservr.exe**: SQL Server (check for slow queries)
- **StreamHost service**: Processing data streams (normal during active streams)

**Solutions:**

- Increase server CPU resources
- Optimize data stream configurations
- Add additional Stream Host services for load distribution

### Memory Issues

**Check memory usage:**

```powershell
# View available memory
Get-CimInstance Win32_OperatingSystem | Select-Object TotalVisibleMemorySize, FreePhysicalMemory

# Check application pool memory
Get-Process w3wp | Select-Object Id, ProcessName, WorkingSet, PrivateMemorySize
```

**Solutions:**

- Increase server RAM
- Configure application pool recycling
- Monitor for memory leaks in data streams

## Getting More Help

### Collect Information for Support

When contacting XMPro Support, provide:

```powershell
# 1. System information
Get-ComputerInfo | Select-Object WindowsVersion, OsHardwareAbstractionLayer

# 2. Installed .NET versions
dotnet --list-runtimes

# 3. IIS application pools status
Get-IISAppPool | Where-Object {$_.Name -like "XMPro*"} | Format-Table Name, State

# 4. Service status
Get-Service | Where-Object {$_.Name -like "*XMPro*" -or $_.Name -like "StreamHost*"} | Format-Table Name, Status

# 5. Recent errors
Get-EventLog -LogName Application -EntryType Error -Newest 20 | Format-Table TimeGenerated, Source, Message

# 6. Installation logs
Get-Content "C:\XMPro\Prerequisites\XMPro-Prerequisites-Install.log" -Tail 50
Get-Content "$env:TEMP\XMPro-Application-Install.log" -Tail 50
```

### XMPro Support Resources

- **Support Portal**: [https://xmpro.na1.teamsupport.com/](https://xmpro.na1.teamsupport.com/)
- **Documentation**: [https://documentation.xmpro.com/](https://documentation.xmpro.com/)
- **Community Forum**: [https://community.xmpro.com/](https://community.xmpro.com/)

### Additional Resources

- [Installation Guide](index.md) - Main deployment documentation
- [Multi-Server Deployment](multi-server-deployment.md) - Distributed deployments
- [Airgapped Deployment](airgapped-deployment.md) - Offline installation
- [Installer README](https://github.com/XMPro/xmpro-development/tree/main/install) - Complete technical reference

---

> [!NOTE]
> For issues specific to the optional prerequisites script (`install-xmpro-prerequisites.ps1`), note that this tool is **not supported by XMPro**. For prerequisites issues, refer to the [Prerequisites](index.md#prerequisites) section in the installation guide.
