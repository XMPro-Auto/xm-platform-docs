
# Prerequisites

In order to proceed with the deployment, you are required to meet the hardware and software requirements listed below:

## 1. Hardware Requirements

1. **XMPro Web Server**
   1. Ensure your server meets the minimum [XMPro Platform hardware requirements](../../install.md#hardware-requirements)
   2. Ensure your server meets the minimum [Windows Server 2022 hardware requirements](https://learn.microsoft.com/en-us/windows-server/get-started/hardware-requirements?tabs=cpu&pivots=windows-server-2022)

2. **Database Server**
   1. _NOTE: These instructions are based on SQL Server running on a different server however SQL Server can be run on the same XMPro Web Server._
   2. Ensure your server meets the minimum [SQL Server 2022 hardware requirements](https://learn.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2022?view=sql-server-ver16)

## 2. SQL Server Install

1. Install SQL Server 2022 (Standard) with Mixed Mode authentication (not Windows authentication)
2. Install SQL Server Management Studio
3. Create a dedicated SQL user account with the following permissions:
   1. Connect to your SQL Server instance
   2. Server type Database Engine
   3. Server name: Your server name (the default value is typically MSSQLSERVER)
   4. Authentication: SQL Server Authentication
   5. Login: sa
   6. Password: The password you set during installation

4. Create the new user account:
   1. In Object Explorer, expand your server
   2. Right-click on "Security" folder
   3. Select "New" → "Login..."
   4. Enter a login name for your dedicated user
   5. Select "SQL Server authentication"
   6. Enter and confirm a strong password
   7. Uncheck "User must change password at next login" if it's checked
   8. Click on "Server Roles" page in the left panel
   9. Assign the required roles
   10. Check the boxes for "dbcreator" and "securityadmin" roles
   11. Click "OK" to create the user
   12. Use a strong password (alphanumeric, 15+ characters, avoid special characters)
   13. Note the SQL Server name, username, and password for later use

> [!WARNING]
> Install the software listed in the next section in the order they are listed

## 3. Software Required for Installation

1. **Install .NET Framework 4.8 Runtime** (required for web applications)
2. **Install .NET Framework 4.8.1 Runtime** (required for installers)
3. **Install IIS with the following features:**
   1. Open Server Manager → Add Roles and Features
   2. Select Web Server (IIS) role
   3. Expand Web Server and Common HTTP Features
   4. Uncheck WebDAV Publishing
   5. Check everything under .NET Framework features
   6. Under Application Development, check everything EXCEPT CGI
   7. Complete installation
   8. **IIS Configuration: Setting Folder Permissions**
      1. Navigate to `C:\inetpub\`
      2. Right-click on the `wwwroot` folder
      3. Select the **Security** tab
      4. Click **Edit** to modify usernames
      5. Click **Add**
         - Type `IIS_IUSRS` in the object names box
         - Click **Check Names** (the name will be underlined if found)
         - Click **OK**
         - Set permissions for this user: Grant **Full Control**
4. **Install URL Rewrite Module** (x64 version)
5. **Install Microsoft ASP.NET Core Runtime 8** (**Hosting Bundle**)

## 4. Browser Configuration

> [!NOTE]
> The installers require Windows Server Internet Explorer functionality to connect to network resources during the installation process.

1. **Open Edge, enable IE compatibility mode:**
   1. Open Edge Settings → Default browser
   2. Enable "Allow sites to be reloaded in Internet Explorer mode"
   3. Go to Edge Settings → Privacy, search, and services
   4. Under Security, set Enhanced Security to "Balanced" mode

2. **Open Internet Explorer, enable Active Scripting and Active Scriptlets for both Internet and Trusted Sites Zones:**
   1. Open Internet Options → Security tab
   2. Click "Custom level"
   3. Enable "Active Scriptlets" under ActiveX controls and plug-ins
   4. Enable "Active Scripting" under Scripting section

3. **Disable Internet Explorer Enhanced Security Configuration (if on Windows Server):**
   1. Open Server Manager → Local Server
   2. Find IE Enhanced Security Configuration
   3. In the Properties section on the right, locate "IE Enhanced Security Configuration" (it should say "On")
   4. Set to "Off" for Administrators

## 5. Signing Certificate Setup (Inter-App Authentication)

1. Download and install OpenSSL for Windows (Win64 Light version v3.5.0 or newer)
2. Open Command Prompt as Administrator
3. Navigate to the OpenSSL installation directory
4. Create Signing Certificate
5. Run the following commands in sequence, replacing **{YourMachine}** with your server name:

   ```bash
   cd C:\Program Files\OpenSSL-Win64
   ```

   ```bash
   cd bin 
   ```

   **Generate a Private Key:**

   ```bash
   openssl genrsa -out sign.pem 2048
   ```

   **Create a certificate signing request:**

   ```bash
   openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout sign.key -out sign.crt -subj "/CN=XMIdentity"
   ```

   **Export the certificate to PFX format:**

   ```bash
   openssl pkcs12 -export -out sign.pfx -inkey sign.key -in sign.crt -certfile sign.crt
   ```

6. The Exported files will be located at C:\Program Files\OpenSSL-Win64\bin
7. It is recommended to move them to a secure location on your machine

## 6. HTTPS/SSL Certificate Setup

1. Select your server name in the left panel
2. Double-click "Server Certificates" in the center panel
3. In the Actions panel on the right, click "Create Self-Signed Certificate"
4. In the dialog that appears:
   1. Enter a friendly name that identifies your server (e.g., "XMPro-ServerName")
   2. Select "Personal" for the certificate store
   3. Click OK
5. The certificate will now appear in the list of server certificates
6. Next, set up HTTPS bindings:
   1. In the left panel of IIS Manager, expand your server name
   2. Expand "Sites"
   3. Select "Default Web Site"
   4. In the Actions panel on the right, click "Bindings..."
   5. Click "Add..."
   6. Set Type to "https"
   7. Set IP Address to "All Unassigned"
   8. Set Port to "443"
   9. Select the SSL certificate you just created from the dropdown
   10. Check "Require Server Name Indication" if you have multiple sites on this server
   11. Click OK, then Close
   12. Test the HTTPS configuration by navigating to <https://localhost> in a browser on the server
   13. You will see a certificate warning because it's self-signed. This is normal.

> [!WARNING]
> For production environments, consider obtaining a trusted SSL certificate from a certificate authority.

> [!WARNING]
> It is recommended to restart the machine after installing and configuring all the prerequisites
