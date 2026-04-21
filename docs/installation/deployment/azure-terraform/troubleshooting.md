# Troubleshooting

This guide helps you fix common issues when deploying XMPro on Azure.

> [!TIP]
> **Most issues are solved by:**
>
> - Running `az login` to refresh your Azure authentication
> - Making sure you're in the right directory (`terraform-xmpro-azure/examples/layered/infra` or `.../app`)
> - Using a different Azure region if you get "quota exceeded" errors

## Most Common Issues

### 1. "Terraform command not found"

**Solution:**

```bash
# You haven't installed Terraform yet. Download it from:
# https://developer.hashicorp.com/terraform/install

# After installing, restart your terminal and try:
terraform version
```

### 2. "Error: building account... Please ensure you have logged in"

**Solution:**

```bash
# Login to Azure:
az login

# If that doesn't work, try:
az logout
az login --use-device-code
```

### 3. "Subscription not found" or wrong subscription

**Solution:**

```bash
# List your subscriptions:
az account list --output table

# Switch to the right one:
az account set --subscription "Your Subscription Name"

# Verify you're on the right subscription:
az account show
```

### 4. "Resource already exists" errors

**Problem:** Azure resource names must be globally unique.

**Solution:**
Edit your `terraform.tfvars` and add a unique prefix:

```hcl
prefix = "mycompany123"  # Add this line with a unique value
```

### 5. Deployment takes forever (more than 30 minutes)

**Common causes:**

- Azure is slow in your region - this is normal for first deployment
- Database creation can take 10-15 minutes alone

**What to check:**

1. Look at the Azure Portal - are resources being created?
2. Check terraform output - is it progressing?
3. If stuck for over 45 minutes, try:

   ```bash
   # Cancel with Ctrl+C, then:
   terraform destroy  # Clean up partial deployment
   terraform apply    # Try again
   ```

### 6. "Insufficient quota" or "SubscriptionIsOverQuotaForSku"

**Problem:** Your Azure subscription has limits on resources.

**Quick Solution:**
Use smaller resource sizes in `terraform.tfvars`:

```hcl
app_service_sku_name = "B1"  # Instead of B2
sql_sku_name = "Basic"        # Instead of S0
```

**Long-term Solution:**
Request a quota increase in Azure Portal under "Quotas".

### 7. Login problems after deployment

**Can't login with admin credentials?**

Check your passwords in `terraform.tfvars`:

- Must be at least 8 characters
- Must have uppercase, lowercase, number, and special character
- No spaces or quotes in the password

**Forgot what you set?**
Look in your `terraform.tfvars` file for:

- `site_admin_password`
- `company_admin_password`

### 8. Application layer errors (Step 5 - terraform plan/apply failures)

**Problem:** Errors during application deployment, often related to infrastructure references.

**Common errors and solutions:**

**"Resource group not found"**

```bash
# Problem 1: resource_group_name in terraform.tfvars doesn't match infrastructure output
# Solution: Get the correct name from infrastructure layer:
cd ../infra
terraform output resource_group_name
# Copy the exact output to your app/terraform.tfvars

# Problem 2: You're in a different Azure subscription
# Solution: Check which subscription you're using:
az account show
# If wrong, switch to the same subscription used for infrastructure:
az account set --subscription "Your Subscription Name"
```

**"SQL Server not found" or "cannot connect to database"**

```bash
# Problem: sql_server_fqdn is incorrect or database not ready
# Solution 1: Get correct SQL server name:
cd ../infra
terraform output sql_server_fqdn
# Copy to app/terraform.tfvars

# Solution 2: Verify SQL server exists in Azure Portal
# Check your resource group for the SQL server resource
```

**"Storage account not found"**

```bash
# Problem: storage_account_name doesn't match infrastructure
# Solution:
cd ../infra
terraform output storage_account_name
# Update in app/terraform.tfvars
```

**"App Service Plan not found"**

```bash
# Problem: Referenced App Service Plan names don't exist
# Solution: Get all infrastructure outputs and verify names match:
cd ../infra
terraform output
# Check that ad_service_plan_name, ds_service_plan_name, sm_service_plan_name match
```

**Best practice:** Always run `terraform plan` in the app layer before `apply`. This validates all your infrastructure references are correct.

### 9. Applications won't start (App Service issues)

**Quick fixes to try:**

1. **Restart the services** in Azure Portal:
   - Go to your resource group
   - Click on each App Service (SM, AD, DS)
   - Click "Restart"

2. **Check the logs** in Azure Portal:
   - Go to your App Service
   - Click "Log stream" in the left menu
   - Look for error messages

3. **Wait a bit longer**:
   - First startup can take 5-10 minutes
   - Check the `/version` endpoint:

     ```bash
     curl "$(terraform output -raw sm_app_url)/version"
     ```

## Getting More Help

### Check Your Setup

Run this to verify everything is working:

```bash
# Check Terraform:
terraform version

# Check Azure login:
az account show

# Check your configuration:
terraform validate
```

### Collect Information for Support

If you need to contact support, run:

```bash
# Save all outputs:
terraform output > terraform-outputs.txt

# Get resource group name:
terraform output resource_group_name

# List what was created:
az resource list --resource-group $(terraform output -raw resource_group_name) --output table
```

### View Logs in Azure Portal

1. **Go to Azure Portal** (portal.azure.com)
2. **Find your resource group** (named like `rg-yourcompany-dev-xmpro`)
3. **Click on Application Insights** resource
4. **Click "Logs"** to see application logs
5. **Click "Failures"** to see errors

### Common Error Messages Explained

| Error | What it means | Solution |
| --- | --- | --- |
| "terraform: command not found" | Terraform isn't installed | [Install Terraform](https://developer.hashicorp.com/terraform/install) |
| "Error: building account" | Not logged into Azure | Run `az login` |
| "SubscriptionIsOverQuotaForSku" | Azure limits exceeded | Use smaller SKUs or request quota increase |
| "Resource already exists" | Name conflict | Add unique `prefix` in terraform.tfvars |
| "Container image not found" | Wrong version specified | Use `imageversion = "latest"` in terraform.tfvars |
| "SSL/TLS connection error" | Network/firewall issue | Check corporate firewall or try different network |

## Still Stuck?

1. **Double-check the basics:**
   - Are you in the right directory? (`terraform-xmpro-azure/examples/layered/infra` or `.../app`)
   - Did you run `terraform init` first?
   - Is your `terraform.tfvars` file saved?

2. **Try a clean deployment:**

   ```bash
   terraform destroy  # Remove everything
   terraform apply    # Start fresh
   ```

3. **Use a different Azure region:**

   ```hcl
   # In terraform.tfvars, try:
   location = "eastus2"  # or "westeurope", "southeastasia"
   ```

4. **Contact Support:**
   - Use the [XMPro Support Portal](https://xmpro.na1.teamsupport.com/login/user)
   - Include your error messages
   - Describe what step failed

> [!NOTE]
> For advanced troubleshooting and detailed technical issues, see the <a href="https://github.com/XMPro/terraform-xmpro-azure" target="_blank">complete module documentation</a>.
