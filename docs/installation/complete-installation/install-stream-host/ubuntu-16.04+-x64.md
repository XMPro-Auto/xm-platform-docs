# Ubuntu 20.04 x64

> [!WARNING]
> **End of Life Statement for Ubuntu 20.04 Stream Host**
> <a href="#end-of-life-statement-for-ubuntu-2004-stream-host" id="end-of-life-statement-for-ubuntu-2004-stream-host"></a>
>
> [Ubuntu 20.04 LTS](https://ubuntu.com/about/release-cycle) reached its end of standard support on 31 May 2025. Security updates and maintenance for Ubuntu 20.04 will no longer be provided unless you have an extended support subscription. Running the XMPro Stream Host on an unsupported operating system may expose your environment to security vulnerabilities and compliance risks.
>
> **Recommended Action:**
XMPro strongly recommends using the [Docker-based Stream Host](docker.md) as the preferred method for all new installations and upgrades. The Docker Stream Host offers improved portability, simplified updates, and is supported on a wide range of modern platforms, including newer Ubuntu LTS releases.

## Prerequisites

### Downloads

Follow the instructions in the [Install Stream Host](./index.md) guide to download the connection profile and installer.

### Hardware and Software

XMPro Stream Host requires certain hardware and software specifications in order to install and run.

Refer to the [**hardware** requirements](../../install.md#hardware-requirements) and the [**software** requirements](../../install.md#software-requirements) in the **1. Preparation** guide.

### Software Install Commands

Install required dependencies using the following commands:

```bash
sudo apt-get update
sudo apt-get install -y wget liblttng-ust0 libkrb5-3 zlib1g uuid-runtime systemd 

# Install Dotnet Runtime
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y aspnetcore-runtime-8.0
sudo apt-get install -y dotnet-runtime-8.0

# Install Libssl
wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.2n-1ubuntu5_amd64.deb

# Downgrade Libcurl
sudo apt-get remove -y libcurl4
wget http://archive.ubuntu.com/ubuntu/pool/main/c/curl3/libcurl3_7.58.0-2ubuntu2_amd64.deb
sudo dpkg -i libcurl3_7.58.0-2ubuntu2_amd64.deb
sudo apt-mark hold libcurl3


```

## Install

When you are ready, you may install the Stream Host by using the following command:

_`sudo dpkg -i /home/adminuser/xmpro-stream-host.deb`_

During the installation process, you will be asked a few questions:

* "_Enter a Friendly Name for this Stream Host_"

    This is the name that appears when you view the Stream Hosts online.
* "_Enter Server Url to connect to_"

    This is the server where Data Stream Designer is hosted, for example: "_<https://mysampleserver/datastreamdesigner/>_". Please note that this URL needs to end in a forward slash.
* "_Enter Collection Id_"

    This is the ID of your Collection and can be copied from Data Stream Designer.
* "_Enter collection secret Key_"

    This is the secret key of your Collection and can be copied from Data Stream Designer.
* "_Enter encryption key_"

    This is the key that the Stream Host will use to encrypt or decrypt secure [user settings](https://docs.xmpro.com/docs/data-stream-designer/concepts/agents/#agent-components), for example, a SQL Server password.

These settings can be found in Data Stream Designer:

![Collection details in Data Stream Designer](../../../images/image-1489.png)

## Uninstall

To uninstall a Stream Host, use the following command:

_`sudo dpkg -r xmpro-stream-host`_

The Stream Host will then be removed. Some files, such as logs, may not be removed because they were created after the installation.

## Next Step: Agents & Connectors

The stream host installation is complete. Please click below to install the default Agents & Connectors:

* [Install Connectors](../install-connectors.md)
