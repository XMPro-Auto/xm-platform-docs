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

## Production Considerations

For production deployments, you may want to:

- **Set up alerts** in Application Insights for errors or performance issues
- **Configure backups** for your SQL databases
- **Review security settings** in Azure Portal
- **Set up custom domains** (see [GitHub documentation](https://github.com/XMPro/terraform-xmpro-azure#dns-and-domain-configuration))

> [!NOTE]
> For all other advanced configurations like SMTP, custom domains, and production settings, see the [complete module documentation](https://github.com/XMPro/terraform-xmpro-azure).
