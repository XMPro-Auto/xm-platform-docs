# Upgrade from Legacy ARM Deployment

If you're currently running XMPro v4.4.x using the legacy Azure ARM templates and planning to upgrade to v4.5/Latest using Azure Terraform, this guide provides important considerations and step-by-step instructions for a smooth migration.

The latest version introduces infrastructure-as-code deployment using Terraform, providing better maintainability, version control, and repeatable deployments.

> [!IMPORTANT]
> Version 4.5/latest is primarily an **installation method upgrade**. Your existing data, users, and configurations are fully preserved:
>
> - All database data remains unchanged (users, roles, applications, data streams)
> - User credentials and authentication continue to work
> - Existing applications and data streams function without modification
> - APIs and integrations remain compatible

---

## Required Information from Your Existing Installation

Before running the Azure Terraform upgrade, document these values from your current v4.4.x ARM deployment and Azure resources. You will need them to update your Terraform variables and configuration files:

### 1. Azure Resource Information

Document your existing Azure resource configuration:

| Configuration Item | Where to Find | Example |
| --- | --- | --- |
| **Resource Group Name** | Azure Portal or ARM deployment | `xmpro-production-rg` |
| **Azure Region** | Azure Portal or ARM deployment | `eastus`, `westeurope` |
| **Virtual Network Name** | Azure Portal → Virtual Networks | `xmpro-vnet` |
| **Subnet Names** | Azure Portal → Virtual Networks → Subnets | `xmpro-app-subnet`, `xmpro-db-subnet` |
| **App Service Plan Name** | Azure Portal → App Service Plans | `xmpro-asp` |
| **App Service Plan SKU** | Azure Portal → App Service Plans → Scale Up | `P1v2`, `P2v3` |

### 2. Database Configuration

Gather your Azure SQL Database details:

| Configuration Item | Where to Find | Example |
| --- | --- | --- |
| **SQL Server Name** | Azure Portal → SQL Servers | `xmpro-sql-server.database.windows.net` |
| **SQL Server Admin Username** | ARM parameters or Azure Portal | `sqladmin` |
| **SQL Server Admin Password** | Key Vault or secure storage | _(your secure password)_ |
| **SM Database Name** | Azure Portal → SQL Databases | `SM` |
| **AD Database Name** | Azure Portal → SQL Databases | `AD` |
| **DS Database Name** | Azure Portal → SQL Databases | `DS` |
| **Database SKU/Tier** | Azure Portal → SQL Database → Pricing Tier | `S3`, `P2` |

### 3. Application Configuration

Note your current application settings:

| Configuration Item | Where to Find | Example |
| --- | --- | --- |
| **SM App Service Name** | Azure Portal → App Services | `xmpro-sm-app` |
| **AD App Service Name** | Azure Portal → App Services | `xmpro-ad-app` |
| **DS App Service Name** | Azure Portal → App Services | `xmpro-ds-app` |
| **Custom Domain Names** | Azure Portal → App Services → Custom Domains | `xmpro.yourcompany.com` |
| **SSL Certificate Configuration** | Azure Portal → App Services → TLS/SSL Settings | App Service Managed Certificate or Custom |

### 4. Networking & Security

Capture your network security configuration:

| Configuration Item | Where to Find | Example |
| --- | --- | --- |
| **Network Security Groups** | Azure Portal → Network Security Groups | Inbound/outbound rules |
| **Application Gateway** (if used) | Azure Portal → Application Gateways | Frontend/backend configurations |
| **Private Endpoints** (if used) | Azure Portal → Private Link | SQL Database, Storage endpoints |
| **Key Vault Name** (if used) | Azure Portal → Key Vaults | `xmpro-keyvault` |

### 5. Monitoring & Logging

Document your monitoring configuration:

| Configuration Item | Where to Find | Example |
| --- | --- | --- |
| **Application Insights Name** | Azure Portal → Application Insights | `xmpro-appinsights` |
| **Log Analytics Workspace** | Azure Portal → Log Analytics Workspaces | `xmpro-logs` |
| **Diagnostic Settings** | Azure Portal → Resource → Diagnostic Settings | Enabled logs and metrics |

**Finding values from Azure CLI:**

```bash
# List resources in your resource group
az resource list --resource-group <your-resource-group> --output table

# Get App Service details
az webapp list --resource-group <your-resource-group> --output table

# Get SQL Server details
az sql server list --resource-group <your-resource-group> --output table

# Get SQL Database details
az sql db list --resource-group <your-resource-group> --server <sql-server-name> --output table
```

---

## Backup Before Upgrading

> [!CAUTION]
> **Always backup before upgrading.** While Terraform performs upgrades safely, backups ensure you can recover if needed.

**Minimum required backups:**

### 1. Azure SQL Databases

```bash
# Using Azure CLI to create database backups
az sql db export \
  --resource-group <your-resource-group> \
  --server <your-sql-server> \
  --name SM \
  --storage-key-type StorageAccessKey \
  --storage-key <your-storage-key> \
  --storage-uri https://<storage-account>.blob.core.windows.net/backups/SM_PreUpgrade_v4.4.x.bacpac \
  --admin-user <admin-username> \
  --admin-password <admin-password>

# Repeat for AD and DS databases
az sql db export \
  --resource-group <your-resource-group> \
  --server <your-sql-server> \
  --name AD \
  --storage-key-type StorageAccessKey \
  --storage-key <your-storage-key> \
  --storage-uri https://<storage-account>.blob.core.windows.net/backups/AD_PreUpgrade_v4.4.x.bacpac \
  --admin-user <admin-username> \
  --admin-password <admin-password>

az sql db export \
  --resource-group <your-resource-group> \
  --server <your-sql-server> \
  --name DS \
  --storage-key-type StorageAccessKey \
  --storage-key <your-storage-key> \
  --storage-uri https://<storage-account>.blob.core.windows.net/backups/DS_PreUpgrade_v4.4.x.bacpac \
  --admin-user <admin-username> \
  --admin-password <admin-password>
```

### 2. Azure Resource Tags (optional but recommended)

```bash
# Tag resources to identify pre-upgrade state
az resource tag \
  --resource-group <your-resource-group> \
  --tags "backup-date=$(date +%Y%m%d)" "version=4.4.x" "upgrade-ready=true"
```

### 3. App Service Configuration

```bash
# Export App Service application settings
az webapp config appsettings list \
  --resource-group <your-resource-group> \
  --name <sm-app-service-name> \
  > sm-appsettings-backup-$(date +%Y%m%d).json

az webapp config appsettings list \
  --resource-group <your-resource-group> \
  --name <ad-app-service-name> \
  > ad-appsettings-backup-$(date +%Y%m%d).json

az webapp config appsettings list \
  --resource-group <your-resource-group> \
  --name <ds-app-service-name> \
  > ds-appsettings-backup-$(date +%Y%m%d).json
```

---

## Running the Upgrade

Once you've documented all the required information and backed up your resources:

### 1. Prepare Terraform Configuration

Clone or set up the v4.5 Terraform configuration:

```bash
# Navigate to your Terraform directory
cd /path/to/xmpro-terraform

# Create a backup of your current configuration (if applicable)
cp -r . ../xmpro-terraform-backup-$(date +%Y%m%d)
```

### 2. Update Variables File

Create or update your `terraform.tfvars` file with the values you documented earlier:

```hcl
# Example terraform.tfvars for upgrade
resource_group_name     = "xmpro-production-rg"
location                = "eastus"
environment             = "production"

# Database configuration (use existing database names)
sql_server_name         = "xmpro-sql-server"
sql_admin_username      = "sqladmin"
sm_database_name        = "SM"
ad_database_name        = "AD"
ds_database_name        = "DS"

# Application configuration
sm_app_service_name     = "xmpro-sm-app"
ad_app_service_name     = "xmpro-ad-app"
ds_app_service_name     = "xmpro-ds-app"

# Preserve existing custom domains if configured
custom_domain_name      = "xmpro.yourcompany.com"

# Other settings...
```

### 3. Review Terraform Plan

Before applying, review what Terraform will change:

```bash
# Initialize Terraform (if needed)
terraform init

# Review the execution plan
terraform plan -out=upgrade-plan.tfplan

# Carefully review the output
# Look for any unexpected resource deletions or recreations
```

> [!CAUTION]
> **Review the plan carefully!** Pay special attention to:
>
> - Database resources (should show "update in-place", not "destroy/create")
> - Data migration steps
> - Any resources marked for deletion

### 4. Apply the Upgrade

Once you're satisfied with the plan:

```bash
# Apply the upgrade
terraform apply upgrade-plan.tfplan

# Monitor the output for any errors
```

The Terraform apply will:

- Update App Services to v4.5 application packages
- Perform database schema migrations automatically
- Update application settings and configurations
- Preserve all existing data and resources
- Update networking and security configurations as needed

### 5. Verify Deployment

After Terraform completes:

```bash
# Check deployment status
terraform output

# Verify App Services are running
az webapp list --resource-group <your-resource-group> --output table

# Check App Service health
az webapp show --resource-group <your-resource-group> \
  --name <app-service-name> \
  --query "state" --output tsv
```

### 6. Update Product URLs in Subscription Manager (if URLs changed)

If your App Service URLs changed during upgrade, update them in Subscription Manager:

a. **Log in to Subscription Manager** as site admin or company admin

b. **Navigate to Products**:

- Click the menu icon (☰) in the top-left
- Select "Products" from the left navigation menu

c. **Select the product to update** (App Designer or Data Stream Designer):

   ![Select Product to Edit](../../../images/installation/windows-server-2022-upgrade-52.png)

- Click on the product name (e.g., "App Designer")
- In the product details panel:
  - Update **Product Log Out URL** to match your new URL
  - Example: Change `https://old-app.azurewebsites.net/server/logout` to `https://new-app.azurewebsites.net/server/logout`

d. **Scroll down and update Product URLs**:

   ![Update Product URLs](../../../images/installation/windows-server-2022-upgrade-53.png)

- In the **PRODUCT URLS** section at the bottom
- Update the URL to match your new App Service URL

e. **Save the changes**:

- Click the "Save" button at the top of the product details panel

f. **Repeat for Data Stream Designer** if its URL also changed

> [!TIP]
> **Terraform Upgrade Best Practices:**
>
> - Run `terraform plan` multiple times before applying to ensure you understand all changes
> - Use workspaces to isolate upgrade testing: `terraform workspace new upgrade-test`
> - Consider upgrading a non-production environment first to validate the process
> - Keep your database backups accessible throughout the upgrade

---

## Post-Upgrade Validation

After the upgrade completes, validate your installation:

### 1. Verify App Services are running

```bash
# Check all App Services status
az webapp list --resource-group <your-resource-group> \
  --query "[].{Name:name, State:state, DefaultHostName:defaultHostName}" \
  --output table

# Check specific App Service health
az webapp show --resource-group <your-resource-group> \
  --name <sm-app-service> \
  --query "{Name:name, State:state, OutboundIpAddresses:outboundIpAddresses}" \
  --output json
```

### 2. Test application endpoints

```bash
# Test SM health endpoint
curl -k https://<sm-app-service>.azurewebsites.net/health

# Test AD health endpoint
curl -k https://<ad-app-service>.azurewebsites.net/health

# Test DS health endpoint
curl -k https://<ds-app-service>.azurewebsites.net/health
```

### 3. Verify database connectivity

```bash
# Check database status
az sql db show --resource-group <your-resource-group> \
  --server <sql-server-name> \
  --name SM \
  --query "{Name:name, Status:status, MaxSizeBytes:maxSizeBytes}" \
  --output table
```

### 4. Test login

Test login with your existing credentials at:

- Subscription Manager: Your configured SM URL (e.g., `https://sm.yourcompany.com`)
- App Designer: Your configured AD URL
- Data Stream Designer: Your configured DS URL

### 5. Check health endpoints

Verify products can connect to each other by accessing the health UI:

- Subscription Manager: `https://<sm-app-service>.azurewebsites.net/health-ui`
- App Designer: `https://<ad-app-service>.azurewebsites.net/health-ui`
- Data Stream Designer: `https://<ds-app-service>.azurewebsites.net/health-ui`

### 6. Verify Stream Host connectivity (if applicable)

- Check Azure Container Instance or VM status (depending on your deployment)
- Verify Stream Host appears online in Data Stream Designer
- Check Stream Host logs in Azure Log Analytics

### 7. Test existing functionality

- Open existing applications in App Designer
- Verify existing data streams in Data Stream Designer
- Confirm user access and permissions work correctly
- Verify custom domains and SSL certificates are working

### 8. Check monitoring and logging

```bash
# Verify Application Insights is receiving telemetry
az monitor app-insights component show \
  --app <app-insights-name> \
  --resource-group <your-resource-group> \
  --query "{Name:name, InstrumentationKey:instrumentationKey, ProvisioningState:provisioningState}"

# Query recent logs
az monitor app-insights query \
  --app <app-insights-name> \
  --analytics-query "requests | where timestamp > ago(1h) | summarize count() by resultCode" \
  --offset 1h
```

---

## Rollback (if needed)

If you encounter issues and need to rollback:

### 1. Restore Azure SQL Databases from backups

```bash
# Import database from BACPAC backup
az sql db import \
  --resource-group <your-resource-group> \
  --server <your-sql-server> \
  --name SM \
  --storage-key-type StorageAccessKey \
  --storage-key <your-storage-key> \
  --storage-uri https://<storage-account>.blob.core.windows.net/backups/SM_PreUpgrade_v4.4.x.bacpac \
  --admin-user <admin-username> \
  --admin-password <admin-password>

# Repeat for AD and DS databases
```

### 2. Restore App Service Configuration (if needed)

```bash
# Restore application settings from backup
az webapp config appsettings set \
  --resource-group <your-resource-group> \
  --name <app-service-name> \
  --settings @appsettings-backup-<date>.json
```

### 3. Verify rollback

```bash
# Check App Services are running
az webapp list --resource-group <your-resource-group> --output table

# Test application access
curl -k https://<sm-app-service>.azurewebsites.net/health
```

> [!CAUTION]
> **Rollback Considerations:**
>
> - Database rollback will lose any data created after the backup
> - Ensure all users are logged out before rolling back
> - Test rollback procedures in a non-production environment first
> - Document the issue before rolling back for troubleshooting purposes

> [!TIP]
> **Need assistance?** Contact XMPro Support or your Implementation Partner for help with the upgrade or rollback process.
