
# Data Delivery Insights

## Stream Hosts Foundational Premise: Streaming Signals for Event Intelligence

### Back to Basics

The premise of a Stream Host is to ingest streaming signals as messages into the Data Stream.

The premise for a Data Stream is the capability to ingest a fire hose and achieve the desired outcome even if not all the data elements are delivered. Consider how this contrasts with an ETL system.

Neither has a primary goal of guaranteed delivery.

### What this means

If a value (e.g. a temperature reading) in the Data Stream is measured against a rule value and a call to action is created when a threshold is reached, there is no impact if the Data Stream misses some readings. These misses could occur for several reasons, one of which is buffering.

There are buffers in the Data Stream, but if they overflow and values are missed, the premise is intact.

In scenarios where multiple transactions occur concurrently, the Stream Host processes the first transaction and buffers the next. However, if the buffer reaches maximum capacity and another transaction is received, the Stream Host will drop the subsequent transaction to prevent potential bottlenecks.

## Guaranteed Delivery – Processing Files

There are circumstances where there needs to be a guarantee for the delivery of the data and the ‘dropping’ of data is unsuitable for the use case.  In these circumstances, the design should adopt a pattern that ensures auditable delivery.

### Explanation

If there is a single batch, data is split into 80 separate messages by an agent within the Data Stream, however, the next agent processes the data significantly more slowly than the previous agent which causes buffering to occur, with 80 messages coming through almost immediately the SH is unable to buffer some messages and therefore drops them.

### Recent Improvement

The v4.4.0 release includes a Stream Host with superior "buffer" functionality.

The new [Window](https://xmpro.gitbook.io/window) Agent supports a delay in transmitting events to the next Agent in a Data Stream. This enhancement aims to mitigate the risk of excessive event data buffering within the Stream Host. The flow of events can be regulated to prevent potential overload scenarios, ensuring smoother data processing and system stability.

## Data Stream Design Considerations and Patterns

When discussing the Data Stream design there are other considerations that, by way of example, point to how patterns could be applied as the design depends on the data profile and orchestrating the data.

### Not all ingested messages are processed

Introduce a mechanism to allocate batch IDs to ensure a message is processed. This relies on tracking individual messages outside the Data Stream (e.g. in a SQL table). If configured correctly, this can avoid duplication if a message is re-processed.

Another consideration could be to split the Data Stream and use storage (e.g. SQL) to process each message/record individually:

* Data Stream 1 ingests the message and saves it as a record in a table.
* Data Stream 2 then processes each record row by row.

### Introduce a delay

Introduce a delay in the Data Stream by including a “delay” Agent during processing to ensure messages are completely processed before a new message is received.

### Small polling interval

When the polling interval of the listener is small (e.g. 5 or 10 seconds), the short time frame usually results in a Data Stream that is less performant.

Consider a longer polling interval.

A general observation is that when event intelligence monitors for asset failure, subject to certain use cases, a polling interval of 3600 seconds (i.e. one hour) is sufficient to timeously perceive degradation.
