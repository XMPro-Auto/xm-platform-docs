# Step 1: Prepare Your Environment

Before you can deploy XMPro on Azure, you need to prepare your computer and Azure account. This page walks you through everything you need, step by step.

> [!TIP]
> **Time needed**: About 30 minutes to complete all steps
>
> **What you'll have when done**: A working environment ready to deploy XMPro

## Quick Overview

You'll need to:

1. **Install 3 tools** on your computer (Terraform, Azure CLI, and optionally Docker)
2. **Set up Azure authentication** so Terraform can create resources
3. **Test everything works** before moving to deployment

Let's get started!

## What You Need

### Your Computer

- **Windows, Mac, or Linux** - any modern computer will work
- **Internet connection** - for downloading tools and deploying to Azure

### Azure Account

- **Azure subscription** - Pay-as-you-go or company subscription
- **Contributor permissions** - to create resources in Azure
- **Credit card or billing setup** - deployment costs approximately $50-200/month depending on usage

> [!NOTE]
> **New to Azure?** You can get a [free Azure account](https://azure.microsoft.com/en-us/free/) with $200 credit to get started.

### Cost Estimate

- **Small deployment** (testing/evaluation): ~$50-100/month
- **Medium deployment** (production): ~$100-200/month  
- **Large deployment** (enterprise): ~$300+/month

> [!TIP]
> **Don't worry about sizing right now!** The default deployment configuration works great for most scenarios. You can always scale up or down later based on your actual usage.

## Install Required Tools

You need to install 3 tools on your computer. Don't worry - this is straightforward!

### Step 1: Install Terraform

Terraform is the tool that creates Azure resources for you.

1. **Download Terraform**: Go to [terraform.io/downloads](https://developer.hashicorp.com/terraform/install)
2. **Follow the installation guide** for your operating system
3. **Test it works**: Open a terminal/command prompt and run:

   ```bash
   terraform version
   ```

   You should see version information (like `Terraform v1.5.0`)

### Step 2: Install Azure CLI

The Azure CLI lets Terraform talk to your Azure account.

1. **Download Azure CLI**: Go to [Azure CLI installation guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
2. **Follow the installation guide** for your operating system  
3. **Test it works**: In your terminal/command prompt, run:

   ```bash
   az version
   ```

   You should see version information

### Step 3: Install Docker (Optional)

Docker helps test that everything is working. This step is optional but recommended.

1. **Download Docker Desktop**: Go to [docker.com/get-started](https://docs.docker.com/desktop/)
2. **Install and start Docker Desktop**
3. **Test it works**: In your terminal/command prompt, run:

   ```bash
   docker --version
   ```

> [!TIP]
> **Stuck on installation?** Each tool has detailed installation guides. Take your time - getting these tools installed correctly is important for the next steps.

## Connect to Your Azure Account

Now you need to connect Terraform to your Azure account so it can create resources.

### Step 1: Login to Azure

1. **Open your terminal/command prompt**
2. **Login to Azure**:

   ```bash
   az login
   ```

3. **A web browser will open** - login with your Azure account
4. **Return to terminal** - you should see your subscription information

### Step 2: Set Your Subscription (If You Have Multiple)

If you have multiple Azure subscriptions, choose which one to use:

1. **List your subscriptions**:

   ```bash
   az account list --output table
   ```

2. **Set the subscription** you want to use:

   ```bash
   az account set --subscription "Your Subscription Name"
   ```

### Step 3: Verify Your Access

Make sure you have the right permissions to create resources in Azure:

```bash
# Check your current account
az account show

# Verify you have Contributor or Owner role
az role assignment list --assignee $(az account show --query user.name -o tsv)
```

> [!NOTE]
> **That's it!** Terraform will use your Azure CLI login to authenticate. No service principal needed!

## Test Everything Works

Let's make sure all your tools are installed correctly before moving to deployment.

### Quick Test

Run these commands to verify everything is ready:

```bash
# Test Terraform
terraform version

# Test Azure CLI
az account show

# Test Docker (if you installed it)
docker --version
```

**What you should see**:

- ✅ Terraform shows a version number  
- ✅ Azure CLI shows your account information
- ✅ Docker shows a version number (if installed)

> [!NOTE]
> **Something not working?** Don't worry! Review the installation steps above or check the troubleshooting section below.

## Need Help?

**Common Problems and Solutions:**

**"terraform: command not found"**

- Make sure you downloaded Terraform for your operating system
- Try restarting your terminal/command prompt
- Check the [Terraform installation guide](https://developer.hashicorp.com/terraform/install)

**"az: command not found"**  

- Make sure you downloaded Azure CLI for your operating system
- Try restarting your terminal/command prompt  
- Check the [Azure CLI installation guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)

**Azure login problems**

- Try: `az logout` then `az login --use-device-code`
- Make sure you have the right permissions in your Azure subscription
- Contact your Azure administrator if you can't create resources

**Still stuck?**

- Double-check you followed each step above
- Make sure you're using the latest versions of the tools
- Try the installation on a different computer to isolate the issue

## You're Ready

🎉 **Congratulations!** Your environment is prepared. Now you can deploy XMPro to Azure.

**[👉 Step 2: Deploy XMPro](deployment/azure-terraform/index.md)** - Follow the simple deployment guide to get XMPro running on Azure.
