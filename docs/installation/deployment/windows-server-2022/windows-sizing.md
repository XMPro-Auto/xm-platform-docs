# Sizing Recommendations

This guide provides recommendations for Windows Server resource sizing when deploying XMPro.

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

## Windows Server Sizing

| Component | Small | Medium | Large |
| --- | --- | --- | --- |
| Subscription Manager (SM) <br>**1**<br> | 2 CPU<br>8GB RAM | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM |
| Application Designer (AD)<br><br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| Data Stream Designer (DS)<br><br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| Stream Host Server (SH) <br>**2,3**<br> | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |
| SQL Database Server <br>(Combined for SM, AD, DS) <br>**4** | 2 CPU<br>8GB RAM | 4 CPU<br>16GB RAM | 8 CPU<br>32GB RAM |

> [!NOTE]
> **Footnotes**
>
> **1** High volumes of concurrent users may require additional compute.
>
> **2** Multiple Stream Hosts can be deployed to the Stream Host Server.
>
> **3** If the Stream Host needs more resources, consider increasing the RAM before adding additional CPU cores as Stream Hosts perform in-memory processing of events.
>
> **4** High volumes of recommendations may require additional compute and storage.

## Single-Server vs Multi-Server Deployment

For smaller deployments, all XMPro components can run on a single server. For medium to large deployments, consider distributing components across multiple servers:

| Deployment Size | Recommended Configuration |
| --- | --- |
| **Small** | Single server with all components (minimum 8 CPU, 32GB RAM) |
| **Medium** | Separate application server and database server |
| **Large** | Dedicated servers for each component with database cluster |

## Default Configuration

The Windows Server installer deploys all XMPro products to a single IIS server by default. This configuration is suitable for:

* Development and evaluation workloads
* Small production deployments
* Proof-of-concept environments

For production deployments with higher workloads, consider the [Multi-Server Deployment](multi-server-deployment.md) guide.

## Additional Considerations

### Virtual Machine Sizing

When running XMPro on virtual machines (VMware, Hyper-V, etc.), ensure:

* CPU resources are not over-committed
* Memory is dedicated (not ballooned or shared)
* Storage uses SSD or high-performance disks
* Network has low latency to the database server

### SQL Server Requirements

The SQL Server sizing recommendations assume:

* SQL Server 2022 Standard Edition or higher
* Mixed Mode authentication enabled
* Dedicated SQL Server instance (not shared with other applications)

For high-availability deployments, consider SQL Server Always On Availability Groups.
