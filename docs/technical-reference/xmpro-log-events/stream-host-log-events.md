# Stream Host Log Events

Stream Host generates log events that monitor real-time stream processing operations and runtime system health. These events cover stream processing execution, agent lifecycle management (creation, startup, and disposal), SignalR communication for live data updates, API integration operations, dependency resolution issues, and critical system failures that may cause service termination.

The tables below organize log events by severity level, with each entry showing the message template you'll see in your logs and the context explaining what triggers that event. The levels are:

- Critical
- Fatal
- Error
- Warning

## Critical Level

Critical events represent the highest severity level, indicating catastrophic failures that will cause the Stream Host to shut down completely. These require immediate attention.

| Message Template | Context Summary |
| --- | --- |
| "An unhandled exception was thrown and the stream host will shut down" | Fatal unhandled exception causing stream host termination |

## Fatal Level

Fatal events indicate critical system failures that cause the application to terminate unexpectedly. These require immediate attention as they represent complete system breakdown.

| Message Template | Context Summary |
| --- | --- |
| "Unhandled fatal error in Stream Host" | Fatal unhandled exception in main program entry point |

## Error Level

Error events indicate serious problems that prevent normal operation but don't necessarily cause application termination. These require prompt investigation and resolution.

| Message Template | Context Summary |
| --- | --- |
| "GetConfiguration method failed for {StreamObjectId}" | Agent configuration retrieval failure in AgentHandler |
| "Validate method failed for {StreamObjectId}" | Agent validation failure in AgentHandler |
| "GetAttributes method failed for {StreamObjectId}" | Agent attribute retrieval failure in AgentHandler |
| "Retrieving encryption password and parameters from API failed. If you are running an earlier version of DS that doesn't support this, you may need to enable the {nameof(GatewayFeatureFlagsElement.EnableLegacyCrypto)} feature flag and configure a {nameof(XMCryptographyElement.TripleDES)} key." | Encryption key retrieval from DS API failure with legacy fallback suggestion |
| "Error retrieving variables from API" | API variable retrieval failure during cache refresh |
| "variables.xv decryption failed, it may have been encrypted with a different key" | Variables file decryption failure due to wrong encryption key |
| "Reading variables.xv file failed" | Variables file reading/processing failure |
| "Received StopStream request with null Id" | StopStream SignalR request with null stream identifier |
| "Error in GetConfiguration" | GetConfiguration SignalR handler error |
| "Error in Validate" | Validate SignalR handler error |
| "Error in GetAttributes" | GetAttributes SignalR handler error |
| "Error in UpdateVariables" | UpdateVariables SignalR handler error |
| "Agent Destroy() failed" | Agent disposal failure in Luigi stream core |
| "API ({invocationId:l}) Error" | REST API client error during API call (Serilog) |
| "Retrieving stream information from API failed" | Stream information API retrieval failure |
| "Failed to start stream" | Stream factory startup failure |
| "Error stopping stream {StreamID} ({StreamName}) v{StreamMajorVersion}.{StreamMinorVersion}" | Stream disposal/stopping error |
| "Error processing request" | Background request processing failure |
| "Error creating agent" | Agent creation/initialization failure |
| "Error starting agent" | Agent startup failure |
| "Error deregistering from {nameof(ILiveViewManager)}" | Live view manager deregistration failure |
| "Error stopping polling task" | Polling task stop failure |
| "Agent Destroy() failed" | Agent Destroy method failure |
| "Error disposing {nameof(IAgentLoadContext)}" | Agent load context disposal failure |
| "Error receiving message" | Message processing failure in agent |
| "Error informing {nameof(IStreamMetricsService)} of published event(s)" | Metrics service event notification failure |
| "Error posting event(s) to Live View API" | Live view API posting failure |
| "Error publishing event(s)" | General event publishing failure |
| "Error informing {nameof(IStreamMetricsService)} of error" | Metrics service error notification failure |
| "Error publishing error to the Error endpoint" | Error endpoint publishing failure |
| "Error logging error" | Recursive error logging failure |
| "Error polling" | Agent polling operation failure |
| "Agent reported an error" | Agent error event reporting |
| "Agent Dispose() failed" | Agent disposal failure in AgentLoadContext |
| "Unloading AssemblyLoadContext failed" | Assembly unloading failure |
| "Unable to resolve agent dependency {FullName}" | Agent dependency resolution failure |
| "Unable to resolve unmanaged agent dependency {name}" | Unmanaged dependency resolution failure |

## Warning Level

Warning events indicate potential issues or unusual conditions that don't prevent operation but may lead to problems if not addressed. Monitor these for trends.

| Message Template | Context Summary |
| --- | --- |
| "Agent attempted to get the value of a null variable name" | Variable service null name request |
| "Failed to connect" | SignalR connection failure with retry |
| "SignalR connection closed" | Unexpected SignalR connection closure |
| "Agent attempted to decrypt a null value" | Null decryption request from agent |
| "Stopping recurrence task" | Scheduled polling task termination |
| "Loading agent {typeName} non-isolated, unexpected results may occur" | Non-isolated agent loading warning |
| "Unexpectedly resolving agent {agentTypeName} dependency {fullName} with no short assembly Name, falling back to default loading behaviour, unexpected results may occur" | Assembly name resolution fallback |
| "Unexpectedly re-resolving agent {agentTypeName} dependency {fullName} that appears to have already been loaded {existingFullName}" | Duplicate assembly resolution attempt |
| "Agent {agentTypeName} dependency {fullName} specifies no version, may not be compatible with resolved Stream Host assembly {defaultFullName}" | Version compatibility warning - no version |
| "Resolved agent {agentTypeName} dependency {fullName} to Stream Host assembly {defaultFullName} which specifies no version and may not be compatible" | Version compatibility warning - no resolved version |
| "Resolved agent {agentTypeName} dependency {fullName} to Stream Host assembly {defaultFullName} which is a different major version and may not be compatible" | Major version compatibility warning |
| "Resolved agent {agentTypeName} dependency {fullName} to Stream Host assembly {defaultFullName} which is an older minor version and may not be compatible" | Minor version compatibility warning |
