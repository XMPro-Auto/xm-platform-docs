
# Agent FAQs

Frequently asked questions regarding Agents.

## Are Agents thread-safe when running in a Data Stream?

Yes, Agents are thread-safe. Each Stream Object (an Agent added to a Data Stream), including multiple instances of the same Agent, is an independent entity.

## How do Agents process events?

Each Stream Object (an Agent added to a Data Stream) has its own thread-safe incoming event queue and processing thread. They receive events via input their endpoints according to the arrows added in the Data Stream.

#### Further Reading

* [Agent Endpoints](../../concepts/agent/index.md#endpoints)

## Can Agents influence each other outside of the regular publish/subscribe mechanism?

While Agents are designed to communicate only through the arrows, there are potential ways they might interact:

1. Shared global variables (as the current Stream Host runs streams in a single process)
2. Network communications
3. Indirect effects, such as:
   * One agent consuming excessive CPU processing power
   * Multiple Agents making conflicting use of a shared resource (e.g., a physical device)
   * Multiple Agents using the same shared library in a non-thread-safe manner

## What is a Stream Host?

A Stream Host is the environment in which Data Streams run. It manages the execution of multiple Stream Objects within a single process.

#### Further Reading

* [Collection and Stream Host](../../concepts/collection.md)

## What are Arrows in the context of XMPro?

Arrows are the links between Stream Object endpoints in a Data Stream. They represent the pathways through which Stream Objects pass data to each other.

#### Further Reading

* [Adding an Agent to the Canvas](../../how-tos/data-streams/manage-data-streams.md#adding-an-agent-to-the-canvas)
* [Input Mapping and Arrow Configuration](../../concepts/data-stream/stream-object-configuration.md#input-mapping-and-arrow-configuration)

## What is a Data Stream?

A Data Stream is a visual display of data flow, where the flow is represented by Stream Objects connected by arrows that perform actions on the data in real-time.

#### Further Reading

* [Data Stream](../../concepts/data-stream/index.md)

## Do Agents have memory buffers, and how do they work?

Yes, each Agent has a memory buffer for events to be processed. This buffer is part of the Agent's thread-safe incoming event queue. Important characteristics of these buffers include:

1. Fixed size: The buffer has a predetermined capacity to prevent excessive memory consumption on Stream Host devices, especially in cases of misconfigured data streams.
2. Overflow behavior: When an agent's buffer is full, new incoming events will not be processed. This can lead to data loss if the incoming data rate consistently exceeds the agent's processing rate.
3. Configuration considerations: It's crucial to properly configure data streams and monitor agent performance to ensure that buffer overflow situations are minimized, maintaining efficient data processing.

#### Further Reading

* [Agent Event Queue Capacity](../../concepts/data-stream/index.md#agent-event-queue-capacity)
