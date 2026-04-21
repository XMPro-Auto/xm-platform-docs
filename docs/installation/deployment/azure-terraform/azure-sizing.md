# Sizing Recommendations

This guide provides recommendations for Azure resource sizing when deploying XMPro.

## Overview

Small, medium, and large sizing estimates are provided. The small option starts with the minimum recommended resources and, generally, each subsequent size doubles the number of CPU cores and available RAM. Not all components experience the same increase in load, so the estimates may not increase at the same rate for all components.

Many factors influence the number of Apps and Data Streams a deployment can effectively run. These factors include:

* the number of data streams,
* how frequently the streams process data,
* the size of the data payload,
* the number of recommendations to be monitored,
* the number of apps and event boards being served,
* the complexity of apps and event boards (the number of elements and integration points),
* and the number of concurrent users accessing the apps and event boards.

As a rough guide, an example workload for a _Medium_-sized deployment would be:

* ~200 Data Streams running across
* ~15 Stream Hosts,
* serving data and triggering recommendations for ~10 Apps

## Azure App Service Plans and Database Sizing

Estimates for Azure target the Premium v3 and v4 service plans for applications, and Azure SQL Database for the databases.

Azure SQL database estimates are based on the General-Purpose service tier and use the DTU-based purchasing model (a blended measure of compute, storage, and IO resources).

| Component | Small | Medium | Large |
| --- | --- | --- | --- |
| Subscription Manager (SM) App Service Plan<br>**1** | P1v3 or P0v4 | P1v3 or P1v4 | P2v3 or P1v4 |
| Application Designer (AD) App Service Plan<br> | P1v3 or P0v4 | P2v3 or P1v4 | P3v3 or P2v4 |
| Data Stream Designer (DS) App Service Plan<br> | P1v3 or P0v4 | P1v3 or P1v4 | P2v3 or P2v4 |
| Stream Host (SH) Container Instances<br>**2,3** | 1 CPU, 4GB RAM | 2 CPU, 8GB RAM | 4 CPU, 16GB RAM |
| Azure SQL Database <br>(For each of SM, AD, DS) <br>**4** | Standard – 20 DTUs | Standard – 50 DTUs | Standard – 100 DTUs |

> [!NOTE]
> **Footnotes**
>
> **1** High volumes of concurrent users may require additional compute.
>
> **2** Multiple Stream Hosts can be deployed as separate container instances.
>
> **3** If the Stream Host needs more resources, consider increasing the RAM before adding additional CPU cores as Stream Hosts perform in-memory processing of events.
>
> **4** High volumes of recommendations may require additional compute and storage.

## Premium v3 vs v4 Service Plans

Azure offers both Premium v3 (Pv3) and Premium v4 (Pv4) App Service Plans:

* **Premium v3**: Standard tier with good performance
* **Premium v4**: Latest generation with better price-performance ratio

Both are suitable for XMPro deployments. The v4 plans generally offer better value.

## Default Configuration

The example Terraform infrastructure module uses **B2** SKU for all App Service Plans by default, which provides:

* 2 vCPU cores
* 3.5 GB RAM
* Suitable for development and evaluation workloads

For production deployments, we recommend upgrading to Premium v3 or v4 plans. You can customize the SKU for each service independently in the infrastructure layer configuration.

## Additional Resources

For detailed Azure pricing information, see:

* [Azure App Service Pricing](https://azure.microsoft.com/en-us/pricing/details/app-service/windows/)
* [Azure SQL Database Pricing](https://azure.microsoft.com/en-us/pricing/details/azure-sql-database/single/#pricing)
* [Azure Container Instances Pricing](https://azure.microsoft.com/en-us/pricing/details/container-instances/)
