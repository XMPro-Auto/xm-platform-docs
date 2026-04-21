# XMPro Deployment Overview

XMPro platform deployment follows a **two-phase responsibility model** designed to leverage customer infrastructure expertise while ensuring successful application deployment. This approach separates infrastructure provisioning (customer responsibility) from application deployment (XMPro/Implementation Partner responsibility), enabling efficient deployment across Azure cloud and Windows Server environments.

**Key Benefits:**

- **Clear Ownership:** Defined responsibility boundaries prevent deployment delays
- **Customer Control:** Infrastructure remains under customer governance and compliance
- **Expertise Alignment:** Customers manage infrastructure, XMPro manages application deployment
- **Flexibility:** Supports both Azure cloud and on-premises Windows Server deployments

## Deployment Responsibility Matrix

| **Customer Responsibilities** | **XMPro / Implementation Partner Responsibilities** |
| --- | --- |
| **Infrastructure Provisioning** <br/>Provision all required infrastructure resources including compute, database, storage, and networking components as specified in the respective deployment documentation (Azure Terraform, Windows Server 2022) | **Application Deployment** <br/>Deploy XMPro applications using automated deployment scripts and configuration management |
| **Platform Configuration** <br/>Configure compute resources, networking, security groups, and ensure all prerequisites are met | **Service Integration** <br/>Configure inter-service communication, authentication flows, and application-specific settings |
| **Database Setup** <br/>Install and configure SQL Server, create required databases with proper security and network access | **Data Migration** <br/>Execute database schema migrations and populate configuration data during deployment |
| **Security & Compliance** <br/>Implement firewall rules, certificate management, and ensure compliance with organizational policies | **Application Security** <br/>Configure application-level security, encryption, and authentication between XMPro services |
| **Network & Access Control** <br/>Configure network access, load balancing, and provide secure access for deployment team | **Operational Validation** <br/>Perform end-to-end testing, health checks, and validate all XMPro functionality |
| **Documentation & Handoff** <br/>Provide access credentials, network topology, and infrastructure documentation to deployment team | **Knowledge Transfer** <br/>Deliver operational documentation, training, and ongoing support for XMPro platform |

## Two-Phase Deployment Model

XMPro deployments follow a **two-phase approach** that separates infrastructure provisioning from application deployment:

### Phase 1: Infrastructure Provisioning

**Objective:** Establish the foundational infrastructure required for XMPro applications

**Customer Focus:**

- Provision resources or infrastructure
- Configure networking, security, and database systems
- Ensure all prerequisites are met per specifications

**XMPro / Implementation Partner Focus:**

- Provide technical guidance and infrastructure requirements
- Validate that infrastructure meets application needs
- Approve readiness for application deployment

### Phase 2: Application Deployment

**Objective:** Deploy and configure XMPro applications on the prepared infrastructure

**Customer Focus:**

- Provide access and coordinate with deployment team
- Review and approve go-live authorization

**XMPro / Implementation Partner Focus:**

- Execute application deployment using automated scripts
- Configure inter-service communication and security
- Perform end-to-end testing and validation
- Deliver knowledge transfer and documentation

### Key Benefits of This Approach

- **Clear Separation:** Infrastructure and application concerns are handled independently
- **Expertise Alignment:** Each party focuses on their area of expertise
- **Risk Mitigation:** Issues are identified and resolved at the appropriate phase
- **Flexibility:** Works with or without implementation partners

## RACI Matrix

| Activity | Customer | XMPro / Implementation Partner |
| --- | --- | --- |
| Infrastructure Provisioning | A/R | C |
| Platform Configuration | A/R | C |
| Database Setup | A/R | C |
| Security & Compliance | A/R | C |
| Network & Access Control | A/R | C |
| Documentation & Handoff | A/R | I |
| Application Deployment | C | A/R |
| Service Integration | C | A/R |
| Data Migration | C | A/R |
| Application Security | C | A/R |
| Operational Validation | C | A/R |
| Knowledge Transfer | I | A/R |

**RACI Legend:**

- **R** - Responsible (performs the work)
- **A** - Accountable (ensures completion and quality)
- **C** - Consulted (provides input and expertise)
- **I** - Informed (kept updated on progress)

## Documentation Requirements

### Customer Must Provide

**Infrastructure Documentation:**

- Network architecture and security configurations
- Access credentials and administrative permissions
- Environment specifications and resource details
- Compliance and security policy requirements

### XMPro / Implementation Partner Will Provide

**Deployment Documentation:**

- Installation procedures and validation steps
- Configuration guides and operational manuals
- Architecture diagrams and technical specifications
- Troubleshooting guides and ongoing support documentation

## Deployment Process Overview

### Infrastructure Deployment

[Deploy XMPro](deployment/index.md) - Infrastructure provisioning and platform deployment using:

- **Azure Terraform Deployment** - Modern container-based deployment for Azure environments
- **Windows Installer** - Native IIS deployment for on-premises Windows Server environments
- **Legacy Options** - ARM templates for v4.4 and earlier versions

### Post-Deployment Configuration

[Post-deployment](complete-installation/index.md) - Complete the setup with:

- **Tenant Configuration** - Set up your first tenant company
- **Stream Host Deployment** - Add additional processing capacity as needed
- **Agents & Connectors** - Upload and configure integration components

---

This responsibility model ensures successful XMPro deployments while maintaining clear boundaries, leveraging respective expertise, and enabling scalable deployment processes across diverse customer environments.
