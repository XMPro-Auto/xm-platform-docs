# Health Checks

> [!NOTE]
> For Azure Terraform deployments, see the [Azure Terraform Implementation Guide](../installation/deployment/azure-terraform/implementation-guide.md#health-checks-configuration) for automated health checks configuration.

<div class="video-container">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/W1LWcSUrgTs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## Overview

Health checks are diagnostic tools that monitor the readiness of your XMPro services. They evaluate various aspects of system health including:

- XMPro service availability
- Database connectivity
- Redis Cache status (when configured)

Health checks are disabled by default but are highly recommended for production environments to ensure service reliability and enable automatic recovery mechanisms.

## Health Endpoints

Each XMPro application exposes health check endpoints:

| Application | Health Endpoint | Health UI |
| --- | --- | --- |
| Application Designer (AD) | `/health` | `/health-ui` |
| Data Stream Designer (DS) | `/health` | `/health-ui` |
| Subscription Manager (SM) | `/health` | `/health-ui` |
| XMPro AI | `/health` | `/health-ui` |

The health endpoint returns JSON with detailed status information:

```json
{
  "status": "Healthy",
  "data": {},
  "description": "Service is running",
  "duration": "00:00:00.0123456",
  "tags": ["database", "cache"]
}
```

## Health UI

The Health UI provides a user-friendly display of health check results:

- Accessible via `/health-ui` path
- Shows real-time status of all configured health checks
- Displays response times and error details
- Provides historical health data

## Configure Health Checks

> [!NOTE]
> For Azure Terraform deployments, health checks are automatically configured and enabled. See the [Azure Terraform Implementation Guide](../installation/deployment/azure-terraform/implementation-guide.md#health-checks-configuration) for details.

## Adding Third-Party Endpoints

> [!NOTE]
> For Azure Terraform deployments, third-party endpoints can be configured through environment variables. See the [Azure Terraform Implementation Guide](../installation/deployment/azure-terraform/implementation-guide.md#health-checks-configuration) for details.
