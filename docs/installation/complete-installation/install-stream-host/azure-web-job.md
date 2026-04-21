# Azure Web Job

## Prerequisites

The first Azure Web Job is created as part of the Azure ARM Template and has already met the [**hardware** requirements](../../install.md#hardware-requirements) and [**software** requirements](../../install.md#software-requirements).

If you require more Stream Hosts, follow these steps to add additional Azure Web Job Stream hosts.

## Setting up a Web Job

XMPro Stream Host can be hosted as a Web Job in Azure. Following are the steps required to set up a web job:

1. Install a Stream Host locally as a Console Application

> [!WARNING]
> Read the instructions in the [Install Stream Host on Windows x64 article](windows-x64.md).

1. Copy the installed files and add them to this [zip](https://firebasestorage.googleapis.com/v0/b/gitbook-legacy-files/o/assets%2F-MZAQh4Gn3jXbTJU2Mb4%2F-MdQnhG4EDOuuKUgRaen%2F-Md__5-am8y9M1w3Ms85%2FSH%20WebJob.zip?alt=media&token=31a4ebd0-111a-4081-af43-dbfef057e559)

> [!NOTE]
> Installed files can usually be found at _C:\Program Files\XMPro Stream Host\\*_

1. Azure may restrict file uploads to 50Mb. If so, remove these from the zip to cut down the size:

* Cache folder
* Logs folder
_ \_.jar files
_ \_.pdb

1. Create a Web Job as per the instructions on the [Microsoft Documentation site](https://docs.microsoft.com/en-us/azure/app-service/webjobs-create#CreateContinuous).

2. Choose the following settings:

| **Name** | **Value** |
| --- | --- |
| File Upload | Select the zip created above |
| Type | Continuous |
| Scale | Single Instance |

> [!NOTE]
> It is recommended to use a separate App service for Web Jobs to keep Data Stream Designer and Stream Hosts separate.

## Next Step: Agents & Connectors

The stream host installation is complete. Please click below to install the default Agents & Connectors:

* [Install Connectors](../install-connectors.md)
