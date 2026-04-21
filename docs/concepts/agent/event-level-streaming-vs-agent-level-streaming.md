# Event-Level Streaming vs. Agent-Level Streaming

Data Streams support two agent communication models for how agents receive and process events from a Stream Host. Understanding the difference helps you choose the right approach when building or updating agents.

> [!NOTE]
> Both communication models produce identical outputs. Switching to Event-Level Streaming does not change stream logic or results, only how memory is used during processing.

## Agent-Level Streaming

In the Agent-Level Streaming model, incoming events are accumulated into a batch and passed to the agent all at once as a `JArray`. The entire dataset is held in memory until the agent finishes processing.

All agents support this model. Agents that have not yet been updated to implement Event-Level Streaming continue to receive batches automatically, and no changes to existing stream designs are required.

## Event-Level Streaming

In the Event-Level Streaming model, each event is delivered to the agent individually as it arrives. The agent handles one event at a time, and memory is released as soon as each event is forwarded downstream.

This brings two key benefits:

- **Lower memory usage**: events are never accumulated into a large in-memory batch, so memory is released as soon as each event is forwarded downstream.
- **Earlier downstream processing**: if the next agent also supports Event-Level Streaming, it can start processing each event immediately rather than waiting for the upstream agent to finish handling all events first.

Agents that require a full dataset before processing, such as applying time-series data to a model, continue to receive events in batches regardless of whether Event-Level Streaming is enabled.

Agents opt in to Event-Level Streaming by implementing the new constructor methods and publishing overloads. See [Building Agents](../../how-tos/agents/building-agents.md#upgrading-to-event-level-streaming) for details on the XMPro.IoT.Framework's `PollAsync` method, `ReceiveAsync` method, and `IAsyncEnumerable<byte[]>` overload of `OnPublishArgs`.
