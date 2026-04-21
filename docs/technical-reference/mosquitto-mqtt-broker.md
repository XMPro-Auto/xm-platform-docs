# Self-Hosted Mosquitto MQTT Broker Implementation

## Introduction

This reference guides organizations to build and maintain their own Mosquitto MQTT broker implementation, removing dependency on XMPro's previous pre-built Mosquitto MQTT broker solution while maintaining compatibility with XMPro platform requirements.

## What You'll Find Here

* Sample Dockerfile and configuration for building your own Mosquitto container
* Basic authentication setup using environment variables
* Migration guidance from XMPro's previous implementation
* Deployment configuration example

> **Note**: This is a reference implementation. Organizations should review and adapt the configuration based on their specific security, networking, and operational requirements before production deployment. This implementation requires a mosquitto.conf configuration file, proper volume mounts for data persistence, and consideration of TLS/SSL setup for production environments. Organizations are responsible for understanding and configuring Mosquitto MQTT broker according to their needs.

## Sample Implementation with Basic Authentication

For reference, here's a sample implementation with basic authentication:

### Dockerfile

```dockerfile
FROM eclipse-mosquitto:2

COPY entrypoint.sh /entrypoint.sh  
RUN mkdir -p /etc/mosquitto && touch /etc/mosquitto/passwd && chmod 0700 /etc/mosquitto/passwd && \
    chown mosquitto:mosquitto /etc/mosquitto/passwd && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
```

### Entrypoint Script (entrypoint.sh)

```bash
#!/bin/sh

# Set up MQTT credentials from environment variables
if [ -n "$MQTT_USER" ] && [ -n "$MQTT_PASSWORD" ]; then
    echo "Setting up MQTT authentication..."
    mosquitto_passwd -b /etc/mosquitto/passwd "$MQTT_USER" "$MQTT_PASSWORD"
    echo "Authentication configured for user: $MQTT_USER"
else
    echo "No MQTT credentials provided. Running without authentication."
fi

# Start Mosquitto with custom configuration
exec mosquitto -c /mosquitto/config/mosquitto.conf
```

### Sample Configuration File (mosquitto.conf)

```conf
allow_anonymous true
password_file /etc/mosquitto/passwd
listener 1883
log_dest file /mosquitto/logs/mosquitto.log
```

### Key Features

* **Authentication**: Uses environment variables `MQTT_USER` and `MQTT_PASSWORD`
* **Configuration**: Expects mosquitto.conf at `/mosquitto/config/mosquitto.conf`
* **Password Management**: Automatically creates password file from environment variables

## Implementation Details

### Build Process

```bash
# Build the custom image
docker build -t your-mosquitto .

# Run with authentication and proper volume mounts
docker run -d \
  --name mosquitto-broker \
  -e MQTT_USER=youruser \
  -e MQTT_PASSWORD=yourpass \
  -p 1883:1883 \
  -v /path/to/your/mosquitto.conf:/mosquitto/config/mosquitto.conf:ro \
  -v mosquitto-data:/mosquitto/data \
  -v mosquitto-logs:/mosquitto/log \
  your-mosquitto

# Alternative with bind mounts
docker run -d \
  --name mosquitto-broker \
  -e MQTT_USER=youruser \
  -e MQTT_PASSWORD=yourpass \
  -p 1883:1883 \
  -v $(pwd)/mosquitto.conf:/mosquitto/config/mosquitto.conf:ro \
  -v $(pwd)/data:/mosquitto/data \
  -v $(pwd)/logs:/mosquitto/log \
  your-mosquitto
```

### Container Configuration

The implementation expects:

* Base image: `eclipse-mosquitto:2`
* Configuration file: `/mosquitto/config/mosquitto.conf`
* Password file: `/etc/mosquitto/passwd` (auto-generated)
* Required environment variables: `MQTT_USER`, `MQTT_PASSWORD`

## Migration from XMPro

Organizations migrating from XMPro's mosquitto implementation should:

1. Build their own container using this reference
2. Deploy to their own container registry  
3. Update deployment manifests to reference the new image
4. Test authentication and configuration compatibility

### Deployment Configuration

Replace XMPro image reference in your deployment manifest:

```yaml
# Replace XMPro image reference in your deployment manifest:
spec:
  containers:
  - name: mosquitto
    image: your-registry/your-mosquitto:latest
    # Configure ports, environment variables, volume mounts, 
    # resource limits, and other deployment requirements
    # according to your infrastructure and security policies
```
