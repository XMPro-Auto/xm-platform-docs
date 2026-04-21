# Configure Logging (Optional)

[Watch the video tutorial](https://youtu.be/N5f1_4F6g84)

## Overview

Application logging refers to recording and storing information about the events and activities that occur within a software application. It involves capturing relevant data, such as error messages, warnings, user interactions, and system events, and storing them in a log file or database.

Application logging is essential for troubleshooting and debugging, as it helps identify and analyze issues that may arise during the application's execution. It also provides valuable insights into the application's performance, usage patterns, and security.

[Serilog](https://serilog.net/) is the diagnostic logging library used in the XMPro suite, and the following logging outputs are supported:

* [Logging to file](#logging-to-file)
* [Application Insights](#application-insights)
* [Application Insights plus Telemetry](#application-insights-plus-telemetry) _(Added v4.3.6)_
* [Datadog](#datadog)

> [!NOTE]
> Subscription Manager currently only supports logging to file.

## Enable Logging

> [!NOTE]
> From v4.4.4., logging for all products is always enabled and the feature flag does not need to be enabled. Lightweight logging to file is active by default and we recommend that it is reviewed.

Repeat these steps for any of the XMPro products (Application Designer, Data Stream Designer, and AI XMPro) - except Subscription Manager and Stream Hosts.

1. Navigate to the IIS location where the XMPro product has been installed.
2. Open the _appsettings.json_ file.
3. Set `enableLogging` in the `featureFlags` object to _true_.
4. Save the file.
5. Restart the XMPro product service.

```json
"xmpro": {
  "appDesigner": {
    "featureFlags": {
      "enableLogging": true
    }
  }
}
```

## Logging to File

This utilizes the Serilog file sink. See [Serilog sinks file documentation](https://github.com/serilog/serilog-sinks-file) for a complete set of configuration options.

Below are examples for each XMPro Product.

### Subscription Manager

1. Open the _web.config_ file.
2. Add the Serilog keys to the `appSettings` element.
3. Save the file and restart the Subscription Manager service.

```json
<appSettings>
    <add key="serilog:using:File" value="Serilog.Sinks.File" />
    <add key="serilog:using:Expressions" value="Serilog.Expressions" />
    <add key="serilog:write-to:File.path" value="%BASEDIR%/App_Data/logs/sm-log-.txt"/>
    <add key="serilog:write-to:File.rollingInterval" value="<rollingInterval> " />
    <add key="serilog:write-to:File.rollOnFileSizeLimit" value="true" />
    <add key="serilog:write-to:File.outputTemplate" value="{Timestamp} [{Level}] ({Name}) Company: {Company} UserId: {UserId} {NewLine}{Message}{NewLine}{Exception}"/>
</appSettings>
```

> [!NOTE]
> It might be encrypted, which will require you to decrypt it first. For instructions, please refer to the [How to encrypt and decrypt a web.config file](https://docs.xmpro.com/knowledge-base-2/how-to-encrypt-and-decrypt-a-web-config-file/) Knowledge Base article.

### Stream Hosts

_Changed in v4.4.0_

#### Using appsettings.json

1. Close or stop the Stream Host.
2. Navigate to the file location where the Stream Host has been installed.
3. Open the _appsettings.json_ file.
4. Add the "File Logging" Serilog configuration.
5. Save the file and restart or reopen the Stream Host.

```json
{
  "FileLogging": {
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning"
      }
    },
    "WriteTo": [
      {
        "Name": "File",
        "Args": {
          "path": "C:\\some\\path\\to\\logs\\log.txt",
          "rollingInterval": "Day",
          "outputTemplate": "{Timestamp:yyyy-MM-dd HH:mm:ss} [{Level:u3}] {SourceContext} Message: {Message:lj}{NewLine}{Properties}{NewLine}{Exception}{NewLine}"
        }
      }
    ]
  }
}
```

#### Using Environment Variables

> [!NOTE]
> This is the preferred approach for our Stream Host Docker Images (Linux). The environment variables will take precedence over the same configuration in the appsettings.json file.

1. Add the environment variables to the platform / service running the Stream Host.
2. Restart the Stream Host.

```yaml
# Example taken from a Docker Compose file.
environment:
  # Other environment variables
  - xm__filelogging__writeto__1__name=File
  - xm__filelogging__minimumlevel__default=Information
  - xm__filelogging__writeto__1__args__path=/app/logs/sh-log-.txt
  - xm__filelogging__writeto__1__args__rollinginterval=Day
  - xm__filelogging__writeto__1__args__outputtemplate=[{Timestamp:yyyy-MM-dd HH:mm:ss} {Level:u3} ({TraceId}:{SpanId})]{NewLine}  {Message:j}{NewLine}  {Properties:j}{NewLine}  {Exception}{NewLine}
```

### Other XMPro Products

Repeat these steps for all the XMPro products except Subscription Manager and Stream Hosts: App Designer, Data Stream Designer, and AI XMPro.

1. Open the _appsettings.json_ file.
2. Add the "File" Serilog configuration inside the WriteTo array.
3. Save the file and restart the XMPro product service

```json
{
  "Serilog": {
    "WriteTo": [
      {
        "Name": "File",
        "Args": {
          "path": "./App_Data/Logs/log_.txt",
          "rollingInterval": "Day",
          "fileSizeLimitBytes": 1048576,
          "rollOnFileSizeLimit": true,
          "outputTemplate": "{Timestamp:yyyy-MM-dd HH:mm:ss} [{Level:u3}] {Message:j}{NewLine}{Properties:j}{NewLine}{Exception}{NewLine}"
        }
      }
    ]
  }
}
```

> [!NOTE]
> The above example provides for the following:
>
> * Log files will now be added to the "Logs" folder located within the "App_Data" directory in the site's root folder.
> * Log files are stored in the "App_Data" folder because it is a protected directory in IIS, preventing access via direct web links. This ensures the security of the log data.
> * It rolls over to a new file daily, or when the file size exceeds 1MB (this helps to prevent large log files and also gives an easy way to calculate the maximum storage consumption when combined with the retention setting
> * It retains only the last 14 log files
> * File names will have the format log_{Date}.txt with an extra sequence number appended if it rolls over due to the size limit, for example:
>   * log_20240321.txt
>   * log_20240321_001.txt
>   * log_20240321_002.txt
>   * log_20240322.txt

## Application Insights

This utilizes the Serilog application insights sink. See [Serilog sinks file for Application Insights](https://github.com/serilog-contrib/serilog-sinks-applicationinsights) for a complete set of configuration options.

Below are the steps for an _**example**_ of how it can be used in App Designer, Data Stream Designer, Stream Hosts, and AI XMPro:

1. Open the _appsettings.json_ file.
2. Add the "ApplicationInsights" Serilog configuration inside the WriteTo array.
3. Save the file and restart the XMPro product service or Stream Host.

```json
{
  "Serilog": {
    "WriteTo": [
      {
        "Name": "ApplicationInsights",
        "Args": {
          "connectionString": "<connection string>",
          "telemetryConverter": "Serilog.Sinks.ApplicationInsights.TelemetryConverters.TraceTelemetryConverter, Serilog.Sinks.ApplicationInsights"
        }
      }
    ]
  }
}
```

## Application Insights plus Telemetry

This utilizes the Serilog application insights sink to write events to Microsoft Azure Application Insights and collect valuable Telemetry data.

Below are the steps for an _**example**_ of how it can be used in App Designer, Data Stream Designer, Stream Hosts, and AI XMPro:

1. Set `enableApplicationInsightsTelemetry` in the `featureFlags` object to _true -_ the same as you already did [here](#enable-logging) for `enableLogging`.
2. Open the _appsettings.json_ file.
3. Add the "ApplicationInsights" configuration.
4. Save the file and restart the XMPro product service or Stream Host.

```json
{
  "ApplicationInsights": {
    "ConnectionString" : "InstrumentationKey=<Instrumentation Key here>";
  }
}
```

## Datadog

This utilizes the Serilog datadog sink. See [Serilog Sinks File for Datadog](https://github.com/DataDog/serilog-sinks-datadog-logs) for a complete set of configuration options.

Below are the steps for an _**example**_ of how it can be used in App Designer, Data Stream Designer, Stream Hosts, and AI:

1. Open the _appsettings.json_ file.
2. Determine the site parameter by checking [here](https://docs.datadoghq.com/getting_started/site/#access-the-datadog-site).
3. Get the endpoint/URL and port number by checking [here](https://docs.datadoghq.com/logs/log_collection/?tab=host#supported-endpoints).
4. Add the "DatadogLogs" Serilog configuration inside the WriteTo array.
5. Save the file and restart the XMPro product service or Stream Host.

```json
{
  "Serilog": {
    "WriteTo": [
      {
        "Name": "DatadogLogs",
        "Args": {
          "apiKey": "<api key>",
          "source": "<source>",
          "host": "<host>",
          "configuration": {
            "url": "<url>",
            "port": port
          }
        }
      }
    ]
  }
}
```
