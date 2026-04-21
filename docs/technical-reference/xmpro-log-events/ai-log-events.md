# AI Log Events

AI generates log events that monitor the core application operations including web application lifecycle, file upload activities, and HTTP request processing. These events provide essential monitoring and troubleshooting information for the AI platform.

The tables below organize log events by severity level, with each entry showing the message template you'll see in your logs and the context explaining what triggers that event. The levels are:

- Fatal
- Error
- Information

## Fatal Level

Fatal events indicate critical system failures that cause the application to terminate unexpectedly. These require immediate attention as they represent complete system breakdown.

| Message Template | Context Summary |
| --- | --- |
| "Application terminated unexpectedly" | Application startup failure causing termination |

## Error Level

Error events indicate serious problems that prevent normal operation but don't necessarily cause application termination. These require prompt investigation and resolution.

| Message Template | Context Summary |
| --- | --- |
| "An error occurred on {RequestPath} with {Message}" | HTTP request processing errors |

## Information Level

Information events track normal system operations and user activities. These provide audit trails and operational insights for system monitoring.

| Message Template | Context Summary |
| --- | --- |
| "Starting web application" | Application startup logging |
| "Uploading file with max width {MaxWidth} and height {MaxHeight}" | File upload operations |
