# Redis Cache Implementation

> [!NOTE]
> For Azure Terraform deployments, Redis autoscaling is automatically configured when enabled.

## Introduction

XMPro uses Redis as a distributed caching solution to improve performance and enable scalability across multiple application instances. Redis is automatically activated when you enable AutoScale in your XMPro configuration and will gracefully fall back to single-server operation when disabled.

This guide explores Redis implementation in XMPro, focusing on how Redis server configuration impacts XMPro performance and behavior. We'll cover usage patterns across products, data caching strategies, capacity management scenarios, configuration best practices, and troubleshooting guidance - with particular attention to what happens when Redis capacity limits are reached.

## Redis Usage per XMPro Product

XMPro uses Redis to store data for caching and passing through data for SignalR. The XMPro Products use it as follows:

| Product | Redis Usage |
| --- | --- |
| **App Designer** | Full (Cache + SignalR) |
| **Data Stream Designer** | SignalR Only |
| **Subscription Manager** | SignalR Only |
| **AI** | None |
| **Stream Host** | None |

### Data Caching

- **Purpose**: Caches real-time Data Stream data sent by the [XMPro App Agent](https://xmpro.gitbook.io/integrations/xmpro-app/) to App Designer via the [Data Streams Connector](https://xmpro.gitbook.io/integrations/data-streams-connector/) Data Source. This allows preservation of temporary data even if the App Designer server restarts and avoids consuming the server's memory.
- **Structure**: Key Values are stored in the Redis Cache as a mix of Hash and List types. Groups of Keys are created for each Connection created with the **Data Streams Connector**. The keys are prefixed to indicate their grouping with the following format: `DS:<AD Connection Id>-<DS Stream Object Id>:*`

### SignalR Backplane

- **Purpose**: Enables SignalR message distribution across multiple server instances. SignalR is used to send real time data between XMPro Products like Database changes or Notifications. This ensures that when one server instance receives a message, all other instances are automatically notified, keeping users connected to different servers synchronized with the same real-time information.
- **Single Server Performance**: Even on a single server deployment, Redis backplane can improve SignalR performance by offloading message routing from server memory to Redis, reducing memory pressure and improving scalability for high-frequency real-time updates.

## Redis Cache Capacity and Expiry Configuration in XMPro

The [XMPro App Agent](https://xmpro.gitbook.io/integrations/xmpro-app/how-to-use/configuration-guide#server) and [Data Streams Connector](https://xmpro.gitbook.io/integrations/data-streams-connector/how-to-use/configuration#cache) provide options to configure how data is stored: Cache Size limits, Sliding Expiry, and Cache Clearing.

1. **Cache Size Limits**:
   - XMPro implements its own cache size management via the Agent and Connector
   - When inserting new items that exceed the configured cache size, oldest items are removed to give way to new data

2. **Sliding Expiry**:
   - Cache items have configurable sliding expiration times
   - Items are automatically removed by Redis after expiration
   - Expiration is refreshed on access to keep frequently used data in cache

3. **Cache Clearing**:
   - Cache items can be cleared via the XMPro App Agent if the Data Stream definition is changed, making the cached data no longer relevant
   - Only data related to that XMPro App Agent is cleared

## Impact When Capacity is Reached on the Redis Server

When a Redis server reaches its memory capacity limits, the impact on the XMPro Products varies significantly between SignalR Backplane and Data Caching usage patterns. Understanding these differences is critical for capacity planning and performance expectations.

**Overview**

- **SignalR**: Automatic fallback to default behavior, no functionality loss within servers
- **Data Caching**: Data sent by the data stream while at capacity will not be cached, creating gaps in the cached data timeline; caching resumes when capacity is restored. See [Data Caching Impact (Stored Data)](#data-caching-impact-stored-data) for details as actual behavior depends on Redis server configuration.

### SignalR Backplane Impact (Message Pass-Through)

**SignalR Usage:**

- Redis serves as a temporary message broker between XMPro servers
- Messages are passed through Redis but not permanently stored
- Used by App Designer, Data Stream Designer, and Subscription Manager

**Behavior When Capacity Reached:**

1. **Automatic Fallback**: XMPro falls back to single-server SignalR using its configured product SQL database - no functionality loss

2. **Performance Impact**:
   - Increased database load as cache misses increase
   - Potential for increased latency in real-time data updates

3. **User Impact**:
   - Real-time updates work normally for users on the same server
   - Cross-server real-time synchronization temporarily unavailable

   **Example:** When Design User A updates a block or agent, Design Users B & C on the same server see the real-time update immediately, but Design Users X, Y & Z on a different server won't see it until they refresh or Redis capacity is restored.

4. **Recovery**: Automatic restoration when Redis capacity returns - no manual intervention needed

5. **Data Safety**: No data loss - SignalR uses Redis for pass-through messaging only, all business data remains in SQL databases

### Data Caching Impact (Stored Data)

**Data Caching Usage:**

- Redis stores actual cached data from Data Streams Connector
- Cached data persists in Redis for performance optimization
- Used primarily in App Designer for metric data in a dashboard application page

**Behavior When Capacity Reached:**

1. **App Designer Cached Data**:
   - **Data Loss**: Cached real-time values displayed in applications will be lost
   - **New Data Behavior**: Behavior for which data is lost depends on the configured Redis Memory Policy:
     - With `allkeys-lru` policy: New data replaces old data
     - With `noeviction` policy: New data is rejected, existing cached data remains
   - **Application Display**: Users will see gaps in historical dashboard data

2. **Recovery**: When Redis capacity returns to normal, the cache will gradually repopulate as new data flows through the application. If it is important to fill in the gap, missed data would have to be resent via the Data Stream.

## Redis Server Configuration

> [!NOTE]
> For Azure Terraform deployments, Redis autoscaling is automatically configured when enabled.

### Connection Configuration

- Redis connection is configured via connection strings
- Supports both standard Redis and Azure Redis Cache
- Connection multiplexer is registered as a singleton for connection pooling

### Redis Memory Policies

These policies are configured during Redis service setup. They determine how Redis handles memory limits and what happens when the server reaches its maximum memory capacity. Redis server typically uses:

- **Default Policy**: `noeviction` - Returns errors when memory limit reached
- **Recommended**: `allkeys-lru` - Evicts least recently used keys
- **Alternative**: `volatile-lru` - Evicts LRU keys with expiration set

## Recommendations

### Data Caching Recommendations

These Redis configuration practices specifically address XMPro data caching performance and help prevent the capacity-related data gaps described above.

**Configure Appropriate Eviction Policies**

- Set Redis `maxmemory-policy` to `allkeys-lru` to automatically remove least-recently-used data when capacity is reached
- Configure `maxmemory` limit based on available resources
- Consider Redis clustering for high-volume deployments

**Cache Size Configuration**

- Adjust XMPro cache size limits based on your expected data throughput
- Balance between memory usage and cache expiry duration
- Monitor cache effectiveness and adjust limits accordingly

### General Recommendations

These broader Redis server configurations support overall system performance and reliability.

**Monitor Redis Memory Usage**

- Set up monitoring for Redis memory consumption
- Configure alerts before reaching capacity
- Plan for Redis scaling based on data volume

**High Availability**

- Use Redis persistence for critical cache data
- Implement Redis replication for failover
- Consider Redis Sentinel or Cluster for production

## Troubleshooting

When Autoscaling is enabled, Redis connection can be checked using the XMPro Health check URL. Common issues are:

> [!TIP]
> For comprehensive information about XMPro health check endpoints and troubleshooting, see the [Health Checks](./health-checks.md) technical reference.

1. **Connection Failures**: Redis server is unhealthy from the Health Check URL

   **Fix**: Restart Redis service, verify network connectivity, and confirm correct connection string in XMPro configuration

2. **Memory Errors**: Monitor Redis memory usage and eviction statistics

   **Fix**: Increase Redis memory allocation, set `maxmemory-policy` to `allkeys-lru`, or optimize XMPro cache size limits

3. **Performance Degradation**: Review cache hit/miss ratios and adjust cache sizes

   **Fix**: Increase Redis memory, adjust cache expiration times, or review data patterns to optimize cache effectiveness

See the [Redis Documentation](https://redis.io/) on how to solve more issues regarding the Server.

### Diagnostic Commands

Use these common [Redis CLI commands](https://redis.io/docs/latest/commands/) from your Redis server or any machine with Redis CLI to help in your investigation

```bash
# Check Redis memory usage
redis-cli INFO memory

# Monitor evicted keys
redis-cli INFO stats | grep evicted

# View current memory policy
redis-cli CONFIG GET maxmemory-policy
```

## Summary

Redis serves different functions across XMPro products, with SignalR backplane providing graceful fallback when capacity is reached, while data caching can experience gaps in cached data. Understanding these behavioral differences and properly configuring Redis memory policies, monitoring, and capacity planning ensures optimal XMPro performance and prevents data loss scenarios. The key insight is that Redis server configuration directly affects how XMPro handles capacity constraints, making proper setup and monitoring essential for reliable operation.
