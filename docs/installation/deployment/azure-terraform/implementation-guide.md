# Implementation Guide

## Introduction

This guide provides step-by-step instructions for deploying XMPro on Azure using the Terraform module. For detailed technical specifications, configuration options, and module documentation, please refer to the [GitHub README](https://github.com/XMPro/terraform-xmpro-azure).

## Prerequisites

Before starting, ensure you have:

- Completed all [Common Prerequisites](../../install.md)
- Completed all [Azure-specific requirements](../../azure-terraform-preparation.md)

## Deployment Options

The XMPro Terraform module provides several deployment examples:

### Option 1: Basic Deployment (Recommended for Getting Started)

1. **Clone the repository and use the basic example:**

   ```bash
   git clone https://github.com/XMPro/terraform-xmpro-azure.git
   cd terraform-xmpro-azure/examples/basic
   ```

2. **Copy and customize the configuration:**

   ```bash
   # Linux/Mac:
   cp terraform.tfvars.example terraform.tfvars
   
   # Windows:
   copy terraform.tfvars.example terraform.tfvars
   
   # Edit terraform.tfvars with your values
   ```

3. **Review the example configuration** in the [Basic Usage section](https://github.com/XMPro/terraform-xmpro-azure#basic-usage) of the README.

### Option 2: Production Deployment

For production deployments, refer to the [Using Custom Company Name for Production Workloads](https://github.com/XMPro/terraform-xmpro-azure#using-custom-company-name-for-production-workloads) section in the README which covers:

- Production-grade App Service SKUs
- Custom domain configuration
- Email notification setup
- Existing database integration

### Option 3: Custom Implementation

Create your own Terraform configuration using the module directly. See the [Module Source Options](https://github.com/XMPro/terraform-xmpro-azure#module-source-options) in the README for different ways to reference the module.

## Deployment Process

### Step 1: Initialize Terraform

```bash
terraform init
```

### Step 2: Plan Your Deployment

```bash
terraform plan
```

### Step 3: Apply Configuration

```bash
terraform apply
```

### Step 4: Access Your Applications

After deployment, retrieve the application URLs:

```bash
terraform output
```

> [!TIP]
> For detailed deployment instructions and troubleshooting, see the [GitHub README](https://github.com/XMPro/terraform-xmpro-azure).

## Configuration Reference

The module supports extensive configuration options. Key areas include:

- **Required Variables**: See [Required Variables](https://github.com/XMPro/terraform-xmpro-azure#required-variables)
- **Basic Configuration**: See [Basic Configuration](https://github.com/XMPro/terraform-xmpro-azure#basic-configuration)
- **Database Options**: See [Database Configuration](https://github.com/XMPro/terraform-xmpro-azure#database-configuration)
- **Container Registry**: See [Container Registry](https://github.com/XMPro/terraform-xmpro-azure#container-registry)
- **Service Sizing**: See [Service Configuration](https://github.com/XMPro/terraform-xmpro-azure#service-configuration)

## Deployment Scenarios

### Evaluation Mode vs For Production Workloads

The module supports two deployment modes. See [Evaluation vs For Production Workloads](https://github.com/XMPro/terraform-xmpro-azure#-evaluation-vs-for-production-workloads) in the README for detailed explanation.

### Using Existing Database

For scenarios where you have an existing SQL Server, see [Existing Database Support](https://github.com/XMPro/terraform-xmpro-azure#%EF%B8%8F-existing-database-support).

### Custom Domain Configuration

To configure custom domains with automatic SSL certificates, refer to the [DNS and Domain Configuration](https://github.com/XMPro/terraform-xmpro-azure#dns-and-domain-configuration) section.

### Configure Autoscale

The module supports distributed caching via Redis for improved performance and scalability. Autoscale is disabled by default.

> [!NOTE]
> Currently, autoscale functionality is only available for Subscription Manager (SM). Support for Application Designer (AD) and Data Stream Designer (DS) will be added in future releases.

#### Prerequisites

Before enabling autoscale, you need:

- An existing Azure Cache for Redis instance or compatible Redis service
- Redis connection string with authentication credentials
- Network connectivity between App Services and Redis instance

#### Enabling Autoscale

Autoscale with Redis is configured through two simple variables:

```hcl
# In your terraform.tfvars
enable_auto_scale = true
redis_connection_string = "your-redis.redis.cache.windows.net:6380,password=your-password,ssl=True,abortConnect=False"
```

When `enable_auto_scale = true`:

- The module sets `AutoScaleEnable = "true"` in the SM Key Vault
- The Redis connection string is stored securely in Key Vault as `REDIS` secret
- Currently, only Subscription Manager (SM) uses the Redis configuration via Key Vault

#### Creating Azure Cache for Redis

To create an Azure Cache for Redis instance, see the [Azure Cache for Redis documentation](https://learn.microsoft.com/en-us/azure/azure-cache-for-redis/cache-overview).

Once created, use the connection string in your Terraform configuration:

```hcl
enable_auto_scale = true
redis_connection_string = "mycompany-redis.redis.cache.windows.net:6380,password=<primaryKey>,ssl=True,abortConnect=False"
```

#### Post-Deployment Configuration

After enabling autoscale:

1. Verify Key Vault secrets are configured:

   ```bash
   az keyvault secret show --vault-name "kv-sm-xmpro-xxx" --name "AutoScaleEnable"
   az keyvault secret show --vault-name "kv-sm-xmpro-xxx" --name "REDIS"
   ```

2. Subscription Manager will automatically use the Redis configuration from Key Vault
3. Monitor Redis metrics in Azure Portal for performance

> [!IMPORTANT]
> The module does not create or manage Redis instances. You must provide an existing Redis connection string.

> [!TIP]
> To learn more about Redis configuration and its impact on XMPro performance, see the [Redis Cache Implementation](../../../technical-reference/redis-cache-implementation.md).

### Health Checks Configuration

The module automatically configures comprehensive health checks for Application Designer (AD) and Data Stream Designer (DS) services. Health checks are enabled by default via feature flags.

#### Automatic Health Check Configuration

Health checks are automatically enabled by default for Application Designer (AD) and Data Stream Designer (DS) services.

#### Health Check Endpoints

The following services expose health check endpoints:

| Service | Health Check URL | Health UI URL |
| --- | --- | --- |
| Application Designer | `/health` | `/health-ui` |
| Data Stream Designer | `/health` | `/health-ui` |

> [!NOTE]  
> Subscription Manager (SM) does not expose health check endpoints. It uses traditional Windows Web App monitoring. To verify SM is running, use the `/version` endpoint instead.

#### Cross-Service Monitoring

Each service (AD, DS) is automatically configured to monitor other services that expose health endpoints.

#### Monitoring Health Status

To verify service status:

```bash
# Check individual service health
curl "$(terraform output -raw ad_app_url)/health"
curl "$(terraform output -raw ds_app_url)/health"

# Check SM version (alternative to health check)
curl "$(terraform output -raw sm_app_url)/version"

# Access Health UI dashboard in browser
"$(terraform output -raw ad_app_url)/health-ui"
```

Expected response: `200 OK` with health status JSON showing the status of all monitored services.

#### Health Dashboard

The Health UI provides a visual dashboard accessible at `/health-ui` on AD and DS services. The dashboard shows:

- Real-time status of all XMPro services
- Response times and availability metrics  
- Service dependency health status
- Historical health data

> [!NOTE]
> For detailed health check configuration and troubleshooting, see the [Health Checks](../../../technical-reference/health-checks.md) technical reference.

#### Third-Party Health Checks

> [!NOTE]
> Configuration for third-party health check monitoring services (such as Azure Application Insights availability tests, external monitoring tools, or custom health check endpoints) is coming in a future release.

### SSO Configuration

> [!NOTE]
> SSO configuration for Azure Terraform deployments is coming in a future release.

> [!TIP]
> For comprehensive SSO setup guides, troubleshooting, and best practices, see the technical references on SSO:
>
> - [SSO - Azure Entra ID](../../../technical-reference/sso-azure-ad.md)
> - [SSO - ADFS](../../../technical-reference/sso-adfs.md)

## Post-Deployment Validation

### Verify Deployment

After deployment, verify your applications are running:

```bash
# List deployed resources
az resource list --resource-group $(terraform output -raw resource_group_name) --output table

# Check application versions
curl -f "$(terraform output -raw ad_app_url)/version"
curl -f "$(terraform output -raw ds_app_url)/version"
curl -f "$(terraform output -raw sm_app_url)/version"
```

### Access Applications

Navigate to the URLs provided by `terraform output`:

- **SM (Subscription Manager)**: Configure users and licenses
- **AD (App Designer)**: Build applications
- **DS (Data Stream Designer)**: Create data pipelines

### Initial Configuration

1. Navigate to Subscription Manager URL
2. Login with admin credentials
3. Configure company settings
4. Set up additional users and roles
5. Configure license keys

### Admin Logins

After deployment, you can access the platform with these accounts:

| User | Type | Password |
| --- | --- | --- |
| <admin@xmpro.onxmpro.com> | Super Admin | Value from `site_admin_password` variable |
| {firstname}.{lastname}@{company_name}.onxmpro.com | Company Admin | Value from `company_admin_password` variable |

> [!WARNING]
> The username format is critical: `firstname.lastname@company_name.onxmpro.com`

### License Management

#### Evaluation Mode

When `is_evaluation_mode = true`, the deployment includes:

- Automatic license provisioning via licenses container
- Pre-configured evaluation product IDs and keys
- No manual license requests required
- **Forces company name to "Evaluation" (overrides any `company_name` variable value)**

> [!NOTE]
> The `examples/basic` configuration uses `is_evaluation_mode = true` as default for quick evaluation deployments.

> [!NOTE]
> To use a custom company name, you must set `is_evaluation_mode = false` and request licenses from XMPro for your specific company name.

#### For Production Workloads (Default)

When `is_evaluation_mode = false` (default), you need to manually request licenses:

1. Login using the Super Admin account `admin@xmpro.onxmpro.com`
2. Navigate to Company → Subscriptions
3. Click "Update License" for each product (AD, DS)
4. Generate license requests and submit to XMPro support
5. Upload received licenses

> [!NOTE]
> License requests require SMTP configuration to be enabled during deployment. See the [Module Documentation](https://github.com/XMPro/terraform-xmpro-azure#email-configuration) for SMTP setup.

## Troubleshooting

For common deployment issues and solutions, see:

- [Troubleshooting Guide](troubleshooting.md) in this documentation
- [Troubleshooting section](https://github.com/XMPro/terraform-xmpro-azure#-troubleshooting) in the GitHub README

## Cleanup

To remove all deployed resources:

```bash
terraform destroy
```

## Next Steps

After successful deployment:

1. **Access Applications**
   - Navigate to the URLs from terraform output
   - Log in with admin credentials

2. **Configure Applications**
   - Set up users and permissions
   - Configure data streams
   - Create applications

3. **Review Security**
   - Enable Azure AD authentication
   - Configure network restrictions
   - Review audit logs

## Support

For deployment issues:

- Review the [Troubleshooting Guide](troubleshooting.md)
- Check Terraform logs: `terraform show`
- Contact XMPro support with deployment details
