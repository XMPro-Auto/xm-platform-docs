
# Troubleshooting

## Certificate Issues

**Problem**: Certificate errors when accessing XMPro components

1. Verify certificates are properly installed in IIS and trusted by the browser
2. Check that certificate paths in XMPro configuration are correct

## SQL Connection Issues

**Problem**: "Cannot connect to SQL Server" during installation

1. Verify SQL Server is running and accessible
2. Check SQL credentials and authentication mode
3. Ensure SQL Server allows remote connections if not installed locally

## IIS Configuration Issues

**Problem**: "HTTP Error 500.19" when accessing XMPro components

1. Verify IIS modules are correctly installed
2. Check application pool configuration
3. Ensure correct .NET version is enabled for the application pool

## Data Stream Designer DB Errors

**Problem**: "Violation of PRIMARY KEY constraint" errors during Data Stream Designer startup

1. Restart IIS using `iisreset /restart`
2. If errors persist, check SQL database for corruption or manually resolve conflicts

## HTTP Error 404.15

**Problem**: Request URL too long error when accessing XMPro applications

1. You need to make two changes to fix this issue:
   1. Increase the httpRuntime maxQueryStringLength and maxUrlLength in the system.web section
   2. Add requestFiltering settings in the system.webServer section
   3. Here's how to modify your web.config file:
      1. Navigate to `C:\inetpub\wwwroot\xmprosubscriptionmanager` and open web.config in a text editor
      2. Update the httpRuntime line in the system.web section

      ```xml
      <!-- Find this line -->
      <httpRuntime targetFramework="4.8" maxUrlLength="1024" />

      <!-- Change it to this -->
      <httpRuntime targetFramework="4.8" maxUrlLength="8192" maxQueryStringLength="8192" />    
      ```

## Stream Host Service Issues

**Problem**: Stream Host service stops unexpectedly

1. Check Windows Event Logs for error details
2. Verify service recovery options are set to restart automatically
3. Ensure proper permissions for the service account

## HTTP Error 400: Bad Request - Request Too Long

1. Open Registry Editor by pressing Win+R, typing "regedit" and pressing Enter
2. Navigate to: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters`
3. Look for these two registry keys:
   1. `MaxFieldLength`
   2. `MaxRequestBytes`
   3. If they don't exist, create them as DWORD (32-bit) values
   4. Right-click in the right pane and select:
      1. "New" → "DWORD (32-bit) Value"
   5. Name the first value `MaxFieldLength`
      1. Double-click it to edit
      2. Select "Decimal" as the base
      3. Enter a value of 65536 (or higher if needed)
      4. Click OK
   6. Right-click again and add a second DWORD value
      1. Name it `MaxRequestBytes`
      2. Double-click to edit
      3. Select "Decimal" as the base
      4. Enter a value of 65536 (or higher if needed)
      5. Click OK
   7. After adding or modifying these values, close Registry Editor
   8. Open Command Prompt as Administrator and type:

      ```cmd
      net stop http /y
      ```

      ```cmd
      net start http
      ```

      ```cmd
      iisreset
      ```

> [!WARNING]
> Always back up configuration files before making any changes to avoid unintended consequences. Contact XMPro Support if issues persist after attempting these solutions.
