# App Designer Log Events

App Designer generates log events that provide visibility into application operations and user activities. These events cover application lifecycle management, WebSocket connection handling, connector and integration management, media file processing, AI service integrations (ChatGPT/Azure OpenAI), and user access control operations.

The tables below organize log events by severity level, with each entry showing the message template you'll see in your logs and the context explaining what triggers that event. The levels are:

- Fatal
- Error
- Warning
- Information
- Debug

## Fatal Level

Fatal events indicate critical system failures that cause the application to terminate unexpectedly. These require immediate attention as they represent complete system breakdown.

| Message Template | Context Summary |
| --- | --- |
| "Application terminated unexpectedly" | Application startup failure causing termination |

## Error Level

Error events indicate serious problems that prevent normal operation but don't necessarily cause application termination. These require prompt investigation and resolution.

| Message Template | Context Summary |
| --- | --- |
| "Unable to get Universal ID for StreamObjectID {StreamObjectID}" | Integration hub universal ID retrieval failure |
| "Failed to connect to target WebSocket server: {Url} for connection {connectionId}" | WebSocket middleware connection failures |
| "Error during WebSocket communication for connection {connectionId}" | WebSocket communication errors |
| "Unhandled error in WebSocket proxy for connection {connectionId}" | Unhandled WebSocket proxy errors |
| "Failed to parse connection info JSON" | JSON parsing errors in WebSocket middleware |
| "Unexpected error while modifying message. Sending original message instead" | Message modification errors in WebSocket |
| "Error during graceful shutdown" | Application shutdown errors |
| "Error exporting application to Git: {Message}" | Git export operation failures |
| "Error importing package from Git: {Message}" | Git import operation failures |
| "Error getting package import summary: {Message}" | Package summary retrieval failures |
| "Error getting application summary: {Message}" | Application summary retrieval failures |
| "Error getting recommendation summary: {Message}" | Recommendation summary retrieval failures |
| "Error getting Git Branches" | Git branch retrieval failures |
| "Error getting Git solutions" | Git solutions retrieval failures |
| "Error getting Git tags" | Git tags retrieval failures |
| "Failed to get entities for connection with Id {ConnectionId}" | Connection entity retrieval failures |
| "Failed to get DataStream entities" | DataStream entity retrieval failures |
| "Failed to get entity {EntityName} for connection with Id {ConnectionId}" | Specific entity retrieval failures |
| "An error occured while trying to upload media files" | Media file upload failures |
| "An error occured trying to delete media file: {mediaFileName}" | Media file deletion failures |
| "AzureOpenAI prompt response failed. Error: {Message}" | Azure OpenAI integration failures |
| "ChatGPT prompt response failed. Error: {Message}" | ChatGPT integration failures |
| "An error occurred while setting favorite for block {BlockId}" | Block favorite operation failures |
| "An error occurred while fetching favorite blocks for user {UserId} and company {CompanyId}" | Favorite blocks retrieval failures |
| "Error while importing template" | Template import failures |
| "Error while importing Application" | Application import failures |
| "Error while importing App Page" | App page import failures |
| "Error while importing Template" | Template import failures |

## Warning Level

Warning events indicate potential issues or unusual conditions that don't prevent operation but may lead to problems if not addressed. Monitor these for trends.

| Message Template | Context Summary |
| --- | --- |
| "Failed to receive valid connection info for connection {connectionId}" | Invalid WebSocket connection info |
| "Expected text message for connection info, received: {messageType}" | Unexpected WebSocket message type |
| "Invalid connection info received" | Invalid connection information |
| "Destination WebSocket is not open. State: {state}" | WebSocket destination state issues |
| "Graceful shutdown timed out after {timeout} seconds" | Shutdown timeout warnings |
| "Error during connection cleanup for {connectionId}" | Connection cleanup warnings |
| "WebSocket error during message forwarding" | Message forwarding warnings |
| "User {UserId} lacks permission for export operation" | Permission denied for exports |
| "User {UserId} lacks permission for import operation" | Permission denied for imports |
| "User {UserId} lacks permission to access package summary" | Permission denied for package access |
| "User {UserId} lacks permission to access application {ApplicationId}" | Application access permission warnings |
| "User {UserId} lacks permission to access recommendation {RecommendationId}" | Recommendation access permission warnings |
| "Cannot trigger Rule {RuleId} with Entity Id {EntityId}. The data parameter value is null." | Rule trigger data validation warnings |
| "Cannot trigger Rule {RuleId} with Entity Id {EntityId}. It either does not exist or is not published." | Rule trigger state warnings |
| "SM Server BaseUrl is not valid, Origin for AllowGet CORS policy will not be applied." | CORS configuration warnings |
| "SM Server BaseUrl is not valid, Origin for AllowPost CORS policy will not be applied." | CORS configuration warnings |
| "Subscription Manager server URL is not configured or invalid. SubscriptionManagerService may fail when used." | Service configuration warnings |
| "Data Stream Designer server URL is not configured or invalid. DataStreamService may fail when used." | Service configuration warnings |

## Information Level

Information events track normal system operations and user activities. These provide audit trails and operational insights for system monitoring.

| Message Template | Context Summary |
| --- | --- |
| "Starting web application" | Application startup |
| "Application shutdown initiated. Beginning graceful shutdown of WebSocket connections." | Graceful shutdown process |
| "Deleting connectors with Ids {ConnectorIds}" | Connector deletion operations |
| "Deleting connector with Id {ConnectorId} with versions {Versions}" | Connector version deletion |
| "Uploading connector with Id {ConnectorId}" | Connector upload operations |
| "Uploading connectors with Ids {ConnectorIds}" | Bulk connector uploads |
| "Deleting connections with Ids {ConnectionIds}" | Connection deletion operations |
| "Populating configuration with connector Id {ConnectorId} with versions {Versions}" | Configuration population |
| "Inserting record with integration id {IntegrationId} and page Id {PageId} with values {Values}" | Record insertion operations |
| "Updating record with integration id {IntegrationId} and page Id {PageId} with values {Values}" | Record update operations |
| "Deleting record with integration id {IntegrationId} and page Id {PageId}" | Record deletion operations |
| "Saving changes to connector" | Connector save operations |
| "Saving changes to connection" | Connection save operations |
| "Upload media file request received." | Media upload request logging |
| "Delete media file request received." | Media deletion request logging |
| "Creating application" | Application creation operations |
| "Editing application" | Application editing operations |
| "Saving changes to application access" | Application access save operations |
| "Reassigning categories with Ids {CategoryIds} to new category Id {NewCatId}" | Category reassignment operations |
| "Deleting application files with ids {ApplicationFileIds}" | Application file deletion |
| "Deleting application with Ids {ApplicationIds}" | Application deletion operations |
| "Deleting application pages with Ids {ApplicationPageIds}" | Application page deletion |
| "Deleting templates with Ids {TemplateIds}" | Template deletion operations |
| "Publishing application with Id {ApplicationId} with version {Version}" | Application publishing |
| "Unpublishing application with Id {ApplicationId}" | Application unpublishing |
| "Publishing applications with Ids {ApplicationIds}" | Bulk application publishing |
| "Unpublishing applications with Ids {ApplicationIds}" | Bulk application unpublishing |
| "Copying applications with Id {ApplicationId} with version {Version}" | Application copying operations |

## Debug Level

Debug events provide detailed technical information for troubleshooting specific operations. These are typically enabled only when investigating particular issues.

| Message Template | Context Summary |
| --- | --- |
| "Logging information for Client Id: {clientId} with Entity Name: {entityName}, Data Binding Id: {dataBindingId}, Filter: {filter} and Load Options: {loadOptions}" | Connector proxy debugging |
| "Logging information for Page: {pageId} with Integration: {integrationId}, Data Binding Id: {dataBindingId}, Filter: {filter} and Load Options: {loadOptions}" | Live connector debugging |
| "Triggering recommendation alert with rule Id {RuleId} and entity Id {EntityId}" | Recommendation alert triggering |
| "Updating recommendation alert fields with alert Id {AlertId} and control values {ControlValues}" | Alert field updates |
| "Unknown field {fValue.Key} when updating recommendation alert fields with alert Id {AlertId} and control values {ControlValues}" | Unknown field debugging |
| "Updating recommendation alert with alert Id {AlertId} with comments {Comments} and helpful flag set to {HelpfulFlag}" | Alert updates with comments |
| "Resolving recommendation with rule Id {RuleId} and entity Id {EntityId}" | Recommendation resolution |
| "Resolving recommendation alert with Id {AlertId}" | Alert resolution operations |
| "Setting close action request with action Id {ActionId}" | Action request closure |
| "Publishing connection with connection Id {ConnectionId} and entity name {EntityName}" | Connection publishing |
| "Publishing connector with connector Id {ConnectorId} and entity name {EntityName}" | Connector publishing |
