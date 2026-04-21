# Subscription Manager Log Events

Subscription Manager generates log events that monitor identity and subscription management operations across the XMPro platform. These events cover user authentication and registration processes, database migration operations, email notification activities, license and subscription management, assembly loading diagnostics for system components, and OWIN/WebAPI request processing for service operations.

The tables below organize log events by severity level, with each entry showing the message template you'll see in your logs and the context explaining what triggers that event. The levels are:

- Error
- Warning
- Information
- Debug
- Verbose

## Error Level

Error events indicate serious problems that prevent normal operation but don't necessarily cause application termination. These require prompt investigation and resolution.

| Message Template | Context Summary |
| --- | --- |
| "Application_Start() failed" | Application startup failure |
| "Error loading {dllFile}" | Assembly loading diagnostics - DLL file loading failure |
| "Error loading reference {referenceName}" | Assembly loading diagnostics - reference loading failure |
| "Error loading type from {AssemblyName}" | Assembly loading diagnostics - type loading failure |
| "Cannot send User Invite. Email notification is disabled" | Registration service - user invitation blocked |
| "Unexpected Error in sending Email" | Registration service - email sending failure |
| "Cannot send Reset Password Request. Email notification is disabled" | Registration service - password reset blocked |
| "Cannot send email. Notification is Disabled" | Email notification service - disabled notification |
| "Unexpected error inside Email Module" | Email notification service - general email failure |
| "Unhandled exception in ASP.NET WebAPI controller" | WebAPI exception logging |
| "Unhandled exception processing OWIN request" | OWIN request processing failure |
| "Cookie authentication exception" | Cookie authentication error |
| "Registration request failed for {username} with error:{errorMessage}" | User registration failure |
| "Password reset failed with error: {error}" | Password reset failure |
| "Error encountered when sending invite user request: {errorMessage}" | User invitation failure |
| "No valid username claim found for external registration" | External registration claim validation |

## Warning Level

Warning events indicate potential issues or unusual conditions that don't prevent operation but may lead to problems if not addressed. Monitor these for trends.

| Message Template | Context Summary |
| --- | --- |
| "Unable to mitigate duplicate Content-Length header, client may complain or fail" | HTTP header mitigation failure |
| "{assemblyName} references {referenceName} {referenceVersion} but lower {loadedVersion} in use" | Assembly version mismatch warning |

## Information Level

Information events track normal system operations and user activities. These provide audit trails and operational insights for system monitoring.

| Message Template | Context Summary |
| --- | --- |
| "Preloading all assemblies to check for issues" | Assembly loading diagnostics startup |
| "Running SM database migrations" | Database migration execution |
| "Skipping SM database migrations" | Database migration skip |
| "Registration requested by {username} for {company} Company" | User registration initiation |
| "Password reset requested for {UserName}" | Password reset initiation |
| "Verifying password reset details for {UserName}" | Password reset verification |
| "Processing password reset for {UserName}" | Password reset processing |
| "Subscription Requested: {SubscriptionProductId}" | License service subscription request |
| "User {UserId} deleted categories: {CategoryIds}" | Category management |
| "Saving Server Variables for User {UserId}" | Server variable management |
| "User {UserId} is deleting variables: {Variables}" | Variable deletion |
| "User {UserId} is deleting variable categories: {VariableCategories}" | Variable category deletion |
| "Deleting user: {deleteUserId}" | User deletion |
| "Saving Profile Request for User: {UserId}" | User profile management |
| "Requesting License for {CompanyRequest} Company by User {UserId}" | License request |
| "Rejecting access request for user {0}" | Access request rejection |
| "Sending email to reject access request for user {0}" | Access rejection notification |
| "Rejecting subscription request for user {0}" | Subscription rejection |
| "Sending email to reject Subscription: {0}" | Subscription rejection notification |
| "Adjusted request URL from {originalUrl} to {adjustedUrl}" | Identity client URL adjustment |

## Debug Level

Debug events provide detailed technical information for troubleshooting specific operations. These are typically enabled only when investigating particular issues.

| Message Template | Context Summary |
| --- | --- |
| "Beginning Application_Start()" | Application startup initialization |
| "Beginning OwinStartup" | OWIN startup initialization |

## Verbose Level

Verbose events provide extremely detailed logging for comprehensive system tracing. These generate high volume logs and should be used sparingly.

| Message Template | Context Summary |
| --- | --- |
| "Preloading main assembly" | Assembly loading diagnostics |
| "Preloading assembly from {dllFile}" | Assembly loading from DLL |
| "Preloading {assemblyName}" | Individual assembly preloading |
| "Loading reference {referenceName}" | Reference assembly loading |
| "Incoming OWIN request" | OWIN request logging |
| "Outgoing OWIN response" | OWIN response logging |
| "Cookie authentication redirect to {url}" | Cookie authentication redirect |
| "Cookie authentication signed in" | Cookie authentication success |
| "Cookie authentication sign in" | Cookie authentication attempt |
| "Cookie authentication sign out" | Cookie authentication logout |
| "Cookie authentication identity validated" | Cookie identity validation |
| "Making request" | Identity client HTTP request |
| "Received response {status}" | Identity client HTTP response |
| "Adjusted request URL" | Identity client URL adjustment |
| "Adjusted URLs in .well-known/openid-configuration response" | OpenID configuration adjustment |
