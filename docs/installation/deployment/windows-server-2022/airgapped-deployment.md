# Airgapped Deployment

## Introduction

Deploy XMPro in restricted environments without internet access using offline installation packages. This approach is essential for high-security facilities, air-gapped networks, or environments with strict compliance requirements that prohibit external connectivity. All installation files are pre-downloaded and transferred to the isolated environment before deployment.

> [!NOTE]
> For general installation concepts and detailed configuration options, see the [main installation guide](index.md).

## Prerequisites

Each server in your airgapped deployment must meet the standard prerequisites. See [Prerequisites](index.md#prerequisites) for complete requirements including:

- Windows Server 2022
- IIS with required features
- SQL Server 2022 with Mixed Mode authentication
- Certificates (signing and SSL)
- .NET Framework and .NET 8 Hosting Bundle

## Download Required Files

From a machine with internet access, download these files:

1. **Installer scripts:**
   - `https://download.app.xmpro.com/4.5.5/install-xmpro-application.ps1`
   - `https://download.app.xmpro.com/4.5.5/manifest.json`
   - (Optional) `https://download.app.xmpro.com/4.5.5/install-xmpro-prerequisites.ps1`

2. **Product packages:**
   - Open `manifest.json` in a text editor
   - Download all URLs listed in the manifest (includes SM.zip, AD.zip, DS.zip, StreamHost.zip, and other dependencies)

### Optional: Automated Download Script

Use this PowerShell script to automatically download all files from manifest.json:

```powershell
# Download manifest.json first
$manifestUrl = "https://download.app.xmpro.com/4.5.5/manifest.json"
$outputDir = "C:\XMPro-Install"
New-Item -Path $outputDir -ItemType Directory -Force | Out-Null

curl.exe -L -o "$outputDir\manifest.json" $manifestUrl --silent --show-error

# Read manifest and download all files
$manifest = Get-Content "$outputDir\manifest.json" | ConvertFrom-Json
foreach ($file in $manifest.PSObject.Properties) {
    $url = $file.Value
    $filename = Split-Path $url -Leaf
    Write-Host "Downloading $filename..."
    curl.exe -L -o "$outputDir\$filename" $url --silent --show-error
}

Write-Host "All files downloaded to $outputDir"
```

## Installation Steps

### Step 1: Prepare Installation Directory

On the Windows Server (offline), create a directory and place all files together:

```
C:\XMPro-Install\
├── install-xmpro-application.ps1
├── manifest.json
├── SM-v4.5.5.zip
├── AD-v4.5.5.zip
├── DS-v4.5.5.zip
├── SM.Database.Console-v4.5.5.exe
├── AD.Database.Console-v4.5.5.exe
├── DS.Database.Console-v4.5.5.exe
└── StreamHost-win-x64-v4.5.5.exe
```

### Step 2: Run Installer

```cmd
cd C:\XMPro-Install
powershell.exe -ExecutionPolicy Bypass -File install-xmpro-application.ps1
```

**What happens:**

- Installer detects local product zip files in same directory
- Skips download step (uses local files instead)
- Proceeds with normal installation process
- No internet connection required

> [!TIP]
> **How it works:** The installer looks for `manifest.json` and product files in the same directory as `install-xmpro-application.ps1`. If found, it uses them directly instead of downloading.

## Next Steps

After completing your Airgapped deployment, proceed to:

**[Post-deployment](../../complete-installation/index.md)** - Complete the setup and configuration of your XMPro environment.

---

## Need Help?

- [Main Installation Guide](index.md) - Standard deployment process
- [Multi-Server Deployment](multi-server-deployment.md) - Distributed deployments
- [Troubleshooting Guide](troubleshooting.md) - Fix common issues
