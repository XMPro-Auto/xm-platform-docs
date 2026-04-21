# Data Stream Designer Log Events

Data Stream Designer generates log events that track real-time data processing operations and system management activities. These events cover use case management and deployment operations, data stream import/export processes, agent configuration and deployment lifecycle, file processing activities, stream host service management, and user authentication and authorization validation throughout the system.

The tables below organize log events by severity level, with each entry showing the message template you'll see in your logs and the context explaining what triggers that event. The levels are:

- Fatal
- Error
- Warning
- Information
- Debug
- Trace
- Verbose

## Fatal Level

Fatal events indicate critical system failures that cause the application to terminate unexpectedly. These require immediate attention as they represent complete system breakdown.

| Message Template | Context Summary |
| --- | --- |
| "Application terminated unexpectedly" | Application startup failure in main program |

## Error Level

Error events indicate serious problems that prevent normal operation but don't necessarily cause application termination. These require prompt investigation and resolution.

| Message Template | Context Summary |
| --- | --- |
| "Error retrieving use case summaries for entities by user {UserId}" | Deployment manager entity summary retrieval errors |
| "Error retrieving use case summaries with version by user {UserId}" | Deployment manager version summary retrieval errors |
| "Error retrieving use case summaries by user {UserId}" | Deployment manager general summary retrieval errors |
| "Error exporting use case {UniversalId} by user {UserId}" | Use case export operation errors |
| "Error importing data streams by user {UserId}" | Data stream import operation errors |
| "Error retrieving agents for user {UserId}" | Agent retrieval operation errors |
| "Error deserializing collection mapping" | Collection mapping deserialization errors |
| "Error deserializing agent version mapping" | Agent version mapping deserialization errors |
| "Error extracting import parameters" | Import parameter extraction errors |
| "Error executing post processing logic" | Post-processing logic execution errors in collections |
| "An error occurred while setting favorite for agent {AgentId}" | Agent favorite setting errors |
| "User {UserId} does not exist or is not in the specified company" | User validation errors during agent operations |
| "An error occurred while toggling favorite for agent {AgentId} for user {UserId} in company {CompanyId}" | Agent favorite toggle errors |
| "Failed to get StreamObject Outputs for StreamObject {StreamObjectId}" | Stream object output retrieval errors |
| "Timeout occured when attempting to interact with the device" | Device interaction timeout errors |
| "Error while configuring stream object" | Stream object configuration errors |
| "Error parsing XML for data stream {FileName}" | XML parsing errors during import |
| "Error saving data stream {FileName}" | Data stream saving errors during import |
| "Error processing file {FileName}" | General file processing errors during import |
| "UseCaseFile failed to Deserialize from memory stream" | Use case file deserialization errors |
| "Failed to create UseCaseFile from memory stream" | Use case file creation errors |
| "Error occurred while importing use case" | Use case import operation errors |
| "Error occurred while importing use case version" | Use case version import operation errors |
| "Error in Stream Host" | Stream host console application errors |
| "Error in Stream Host service" | Stream host service errors |
| "Error in Stream Host ServiceRunner" | Stream host service runner errors |
| "Error starting Stream Host service" | Stream host service startup errors |
| "Error stopping Stream Host service" | Stream host service shutdown errors |

## Warning Level

Warning events indicate potential issues or unusual conditions that don't prevent operation but may lead to problems if not addressed. Monitor these for trends.

| Message Template | Context Summary |
| --- | --- |
| "User {UserId} attempted to retrieve summaries without providing request" | User input validation warnings for summaries |
| "User {UserId} attempted to retrieve summaries without providing entity IDs" | User input validation warnings for entity IDs |
| "User {UserId} attempted to access entity IDs {EntityIds} without any permission" | User permission validation warnings |
| "Invalid request for use case summaries by user {UserId}" | Invalid use case summary request warnings |
| "Unauthorized access attempt by user {UserId}" | Unauthorized access attempt warnings |
| "User {UserId} attempted to retrieve version summaries without providing request" | Version summary request validation warnings |
| "User {UserId} attempted to retrieve version summaries without providing versions" | Version summary input validation warnings |
| "User {UserId} attempted to access versions without permission" | Version access permission warnings |
| "Invalid request for version summaries by user {UserId}" | Invalid version summary request warnings |
| "Unauthorized version access attempt by user {UserId}" | Unauthorized version access warnings |
| "User {UserId} attempted to retrieve summaries without providing Universal IDs" | Universal ID input validation warnings |
| "User {UserId} attempted to access Universal IDs {UniversalIds} without permission" | Universal ID access permission warnings |
| "User {UserId} attempted to export without providing request" | Export request validation warnings |
| "User {UserId} attempted to export without providing Universal ID" | Export Universal ID validation warnings |
| "User {UserId} attempted to export use case {UniversalId} without permission" | Export permission validation warnings |
| "Unauthorized export attempt by user {UserId} for use case {UniversalId}" | Unauthorized export attempt warnings |
| "User {UserId} attempted import without providing files" | Import file validation warnings |
| "User {UserId} provided invalid import parameters: {Error}" | Import parameter validation warnings |
| "Invalid import request by user {UserId}" | Invalid import request warnings |
| "Unauthorized import attempt by user {UserId}" | Unauthorized import attempt warnings |
| "User {UserId} attempted to retrieve agents without providing request" | Agent retrieval request validation warnings |
| "User {UserId} attempted to retrieve agents without providing IDs" | Agent ID validation warnings |
| "User {UserId} attempted to access agents not in their company {CompanyId}" | Agent company access validation warnings |
| "Invalid agent request by user {UserId}" | Invalid agent request warnings |
| "SM Server BaseUrl is not valid, Origin for AllowSMGet CORS policy will not be applied" | CORS policy configuration warnings |
| "SM Server BaseUrl is not valid, Origin for AllowPost CORS policy will not be applied" | CORS policy configuration warnings |

## Information Level

Information events track normal system operations and user activities. These provide audit trails and operational insights for system monitoring.

| Message Template | Context Summary |
| --- | --- |
| "Starting web application" | Application startup information |
| "Stream Metrics Service - Started" | Metrics cleanup service initialization |
| "Stream Metrics Service - No task is running, check for new job" | Metrics cleanup service task status |
| "Stream Metrics Service - There is a task still running, wait for next cycle" | Metrics cleanup service concurrency control |
| "Stream Metrics Service - Skipping cleanup as another instance may already have completed the operation" | Metrics cleanup service coordination |
| "Stream Metrics Service - Initiate graceful shutdown" | Metrics cleanup service shutdown |
| "Retrieving use case summaries for {Count} universal IDs" | Use case summary retrieval operations |
| "Exporting use case to Git with universal Id {UniversalId} with version {Version}" | Use case export operations |
| "Saving changes to dashboard" | Dashboard modification operations |
| "Creating dashboard" | Dashboard creation operations |
| "Cloning dashboard with Id {DashboardId} with clone name {CloneName}" | Dashboard cloning operations |
| "Revoking collection key with Id {CollectionId}" | Collection key management operations |
| "Serializing variable {Variable} files" | Variable serialization operations |
| "Deleting collection with Id {CollectionId}" | Collection deletion operations |
| "Saving changes to collection" | Collection modification operations |
| "Creating collection" | Collection creation operations |
| "Saving changes to variable" | Variable modification operations |
| "Deleting variables with names {VariableNames}" | Variable deletion operations |
| "Uploading file with max width {MaxWidth} and height {MaxHeight}" | File upload operations |
| "Publishing use case with Id {UseCaseId} with major version {MajorVersion}" | Use case publishing operations |
| "Unpublishing use case with Id {UseCaseId}" | Use case unpublishing operations |
| "Publishing use cases with Ids {UseCaseIds}" | Bulk use case publishing operations |
| "Unpublishing use cases with Ids {UseCaseIds}" | Bulk use case unpublishing operations |
| "Copying stream with Id {StreamId} with version {Version}" | Stream copying operations |
| "Exporting use case by Id {UseCaseId} with version {Version}" | Use case export by ID operations |
| "Exporting use case with universal Id {UniversalId} with version {Version}" | Use case export by Universal ID operations |
| "Cloning use case with Id {UseCaseId} and name {CloneName}" | Use case cloning operations |
| "Deleting use case with Id {UseCaseId}" | Use case deletion operations |
| "Deleting stream with Id {StreamId} with major version {MajorVersion}" | Stream deletion operations |
| "Deleting all devices failures by use case Id {UseCaseId}" | Device failure cleanup operations |
| "Deleting specific device with Id {DeviceId}" | Specific device deletion operations |
| "Saving changes to use case" | Use case modification operations |
| "Creating use case" | Use case creation operations |
| "Reassigning categories with Ids {CategoryIds} to new category Id {NewCategoryId}" | Category reassignment operations |
| "Reassigning collection with collection Id {CollectionId} with use case Id {UseCaseId}" | Collection reassignment operations |
| "Importing use case with Id {UserCaseId}" | Use case import operations |
| "Importing stream with version {StreamVersion} with use case Id {UseCaseId}" | Stream import operations |
| "Configuring agent with Id {AgentId}" | Agent configuration operations |
| "Remote configuration for agent with Id {AgentId} and version {version}" | Remote agent configuration operations |
| "Updating settings with name {SettingName}" | Settings update operations |

## Debug Level

Debug events provide detailed technical information for troubleshooting specific operations. These are typically enabled only when investigating particular issues.

| Message Template | Context Summary |
| --- | --- |
| "API {message:l}" | API operation debug messages |

## Trace Level

Trace events provide the most detailed diagnostic information for deep troubleshooting. These are typically used for low-level debugging.

| Message Template | Context Summary |
| --- | --- |
| "Authorization header validation succeeded: {reason}" | Bearer token validation success |
| "Authorization header validation failed: {reason}" | Bearer token validation failures |
| "Bearer token validation failed: {reason}" | Bearer token processing failures |

## Verbose Level (Serilog)

Verbose events provide extremely detailed logging for comprehensive system tracing. These generate high volume logs and should be used sparingly.

| Message Template | Context Summary |
| --- | --- |
| "API ({invocationId:l}) {instance:l}.{method:l}({parameters})" | REST client method invocation tracing |
| "API ({invocationId:l}) Returning {returnValue}" | REST client method return value tracing |
| "API ({invocationId:l}) {statusCode} {requestUri}" | REST client HTTP response tracing |
| "API ({invocationId:l}) {method:l} {requestUri}" | REST client HTTP request tracing |
