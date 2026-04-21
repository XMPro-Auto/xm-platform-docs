# Sizing Guideline

This is a guideline for the compute resources needed for the different components in a deployment.

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

## On-Premise

| Component | Small | Medium | Large |
| --- | --- | --- | --- |
| Subscription Manager (SM) <br>**1**<br> | 2 CPU<br>8GB RAM | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM |
| Application Designer (AD)<br><br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| Data Stream Designer (DS)<br><br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| Stream Host Server (SH) <br>**2,3**<br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| SQL Database Server <br>(Combined for SM, AD, DS) <br>**4** | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |

> [!NOTE]
>
> #### Footnotes
>
> **1** High volumes of concurrent users may require additional compute.
>
> **2** Multiple Stream Hosts can be deployed to the Stream Host Server.
>
> **3** If the Stream Host needs more resources, consider increasing the RAM before adding additional CPU cores as Stream Hosts perform in-memory processing of events.
>
> **4** High volumes of recommendations may require additional compute and storage.

## Azure

Estimates for Azure target the Premium v3 service plan for applications, and Azure SQL Database for the databases.

Azure SQL database estimates are based on the General-Purpose service tier and use the DTU-based purchasing model (a blended measure of compute, storage, and IO resources).

| Component | Small | Medium | Large |
| --- | --- | --- | --- |
| Subscription Manager (SM) App Service Plan<br>**1** | P1v3 | P1v3 | P2v3 |
| Application Designer (AD) App Service Plan<br> | P1v3 | P2v3 | P3v3 |
| Data Stream Designer (DS) App Service Plan<br> | P1v3 | P1v3 | P2v3 |
| Stream Host Server (SH) App Service Plan<br>**2,3** | P1v3 | P2v3 | P3v3 |
| Azure SQL Database <br>(For each of SM, AD, DS) <br>**4** | Standard – 20 DTUs | Standard – 50 DTUs | Standard – 100 DTUs |

> [!NOTE]
> **Footnotes**
>
> **1** High volumes of concurrent users may require additional compute.
>
> **2** Multiple Stream Hosts can be deployed to the Stream Host App Service Plan.
>
> **3** If the Stream Host needs more resources, consider increasing the RAM before adding additional CPU cores as Stream Hosts perform in-memory processing of events.
>
> **4** High volumes of recommendations may require additional compute and storage.

For additional details please see [Azure App Service Pricing](https://azure.microsoft.com/en-au/pricing/details/app-service/windows/) and [Azure SQL Database Pricing](https://azure.microsoft.com/en-au/pricing/details/azure-sql-database/single/#pricing).

## AWS

Estimates for AWS target Amazon EC2 T3 instances for applications, and an Amazon RDS T3 instance for the databases.

| Component | Small | Medium | Large |
| --- | --- | --- | --- |
| Subscription Manager (SM) EC2 Instance<br>**1** | t3.large | t3.large | t3.xlarge |
| Application Designer (AD) EC2 Instance<br> | t3.large | t3.xlarge | t3.2xlarge |
| Data Stream Designer (DS) EC2 Instance<br> | t3.large | t3.large | t3.xlarge |
| Stream Host Server (SH) EC2 Instance<br>**2,3** | t3.large | t3.xlarge | t3.2xlarge |
| Amazon RDS for SQL <br>(Combined for SM, AD, DS) <br>**4** | t3.large | t3.xlarge | t3.2xlarge |

> [!NOTE]
>
> #### Footnotes
>
> **1** High volumes of concurrent users may require additional compute.
>
> **2** Multiple Stream Hosts can be deployed to the Stream Host Server.
>
> **3** If the Stream Host needs more resources, consider increasing the RAM before adding additional CPU cores as Stream Hosts perform in-memory processing of events.
>
> **4** High volumes of recommendations may require additional compute and storage.

For additional details please see [AWS EC2](https://aws.amazon.com/ec2/instance-types/) and [RDS instance types](https://aws.amazon.com/rds/instance-types/).
