# Deploy Stream Connector Infrastructure (Optional)

## Overview

Stream Connector enables dedicated data stream connectivity between XMPro environments or external systems using an MQTT broker and a purpose-built Stream Host. For more information, see the [XMPro Stream Integration documentation](https://xmpro.gitbook.io/integrations/xmpro-stream).

This is an optional post-deployment step. Stream Connector infrastructure is recommended, but is not required for standard XMPro platform operation.

Stream Connector infrastructure requires two components:

1. **MQTT Broker** - an Eclipse Mosquitto MQTT broker that handles message routing between environments
2. **Stream Connector Stream Host** - a dedicated Stream Host pre-configured to communicate over MQTT

## Prerequisites

Before deploying Stream Connector infrastructure, ensure you have:

- A deployed XMPro platform (via [Azure Terraform](../deployment/azure-terraform/index.md) or [Windows Server](../deployment/windows-server-2022/index.md))
- A Collection created in Data Stream Designer for the Stream Connector SH (see [Getting Collection Credentials](#getting-collection-credentials))
- An MQTT broker deployed and accessible (see Step 1)

## Step 1: Deploy MQTT Broker

Stream Connector infrastructure requires an MQTT broker for message routing. Choose a deployment method based on your environment:

| Deployment Method | How to Deploy |
| --- | --- |
| Terraform | Set `enable_stream_connector = true` in your infrastructure layer variables. The module deploys an Eclipse Mosquitto broker on Azure Container Apps automatically. See the [Azure Terraform deployment guide](../deployment/azure-terraform/index.md). |
| Docker | Deploy your own Mosquitto broker using the [Mosquitto MQTT Broker reference implementation](../../technical-reference/mosquitto-mqtt-broker.md). |
| Windows | Deploy your own Mosquitto broker using the [Mosquitto MQTT Broker reference implementation](../../technical-reference/mosquitto-mqtt-broker.md). |

Record the broker connection details (hostname, port, username, password) for use in Step 3.

## Step 2: Deploy Stream Connector Stream Host

Deploy a dedicated Stream Host for Stream Connector infrastructure. The Stream Connector SH requires its own Collection credentials - see [Getting Collection Credentials](#getting-collection-credentials).

| Deployment Method | How to Deploy |
| --- | --- |
| Terraform | Set `enable_stream_connector_stream_host = true` in your application layer variables and provide the collection credentials. See the [Azure Terraform deployment guide](../deployment/azure-terraform/index.md). |
| Docker | Follow the [Docker Stream Host guide](install-stream-host/docker.md), configuring the MQTT broker connection via environment variables. |
| Windows | Follow the [Windows Stream Host guide](install-stream-host/windows-x64.md), configuring the MQTT broker connection in the Stream Host settings. |

## Step 3: Configure Server Variables

After deploying the MQTT broker and Stream Connector SH, configure the `StreamAsConnector:*` server variables in both **Application Designer** and **Data Stream Designer**. These variables provide the MQTT broker connection settings that enable communication between AD and the Connector Data Streams.

For the full list of required server variables and multi-environment setup instructions, see the [XMPro Stream Integration documentation](https://xmpro.gitbook.io/integrations/xmpro-stream).

> [!IMPORTANT]
> The server variable values must be identical in both AD and DS for the same environment. Mismatched values will prevent streams from being discovered.

## Getting Collection Credentials

Collection credentials are **required** when deploying the Stream Connector SH. To obtain them:

1. Open **Data Stream Designer**
2. Click **Collections** in the left navigation menu
3. Select a Collection (or create a new one for Stream Connector infrastructure)
4. Copy the **Id** and **Key** fields
5. Use these values when configuring the Stream Connector SH in your chosen deployment method

For more details, see [Collection and Stream Host Concepts](../../concepts/collection.md).

## Verification

After deployment, verify both components are running:

1. **MQTT Broker** - confirm the broker is accessible on its configured port (1883 for plain, 8883 for TLS)
2. **Stream Connector SH** - verify it appears as a connected host in Data Stream Designer under its own collection
3. **Server Variables** - confirm the `StreamAsConnector:*` variables are configured identically in both AD and DS

## Troubleshooting

### MQTT Broker Not Starting

If the MQTT broker container fails to start:

1. Check the container logs for configuration errors
2. Verify network connectivity and port availability
3. Confirm the broker credentials are valid

For the reference implementation details, see the [Mosquitto MQTT Broker guide](../../technical-reference/mosquitto-mqtt-broker.md).

### Stream Connector SH Not Connecting

If the Stream Connector SH doesn't appear in Data Stream Designer:

1. **Check container/service logs** for connection errors
2. **Verify MQTT broker is reachable** from the Stream Host network
3. **Check collection credentials** - verify they match what was configured in Data Stream Designer

### Rotating Collection Credentials

If collection credentials are rotated after deployment, update the Stream Connector SH configuration with the new credentials and restart the Stream Host.
