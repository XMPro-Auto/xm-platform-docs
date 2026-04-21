# Running Data Streams

## Running Data Streams

Data Streams need to be running to start performing the functions they have been designed to do. When you click on the "_Publish_" button, your Stream will start running. As soon as this button is clicked, the engine will look at which Collection each Agent in the Data Stream is associated with. It will then look at which Stream Hosts are available for use in each Collection and use those Stream Hosts to allow Agents in that Collection to execute actions. To read more about how Stream Hosts and Collections work, click [here](../collection.md).

To verify which collection an Agent will use, click on the "_Configure_" button.

![Configure button](../../images/concepts/data-stream/image-1756.png)

![Collection selection](../../images/concepts/data-stream/image-776.png)

## Viewing Live Data

The _Live View_ functionality in Data Stream Designer allows you to view data as it is processed by the Agents in your Stream. For each Agent in your Stream, you can let the data display in either a grid, gauge, or chart. To view this data, select the "Live View" button after publishing your Stream. Next, select the Agents you would like to view the data for.

> [!NOTE]
> Pre v4.3.7, users should close the _Live View_ before navigating away to signal to the Stream Host to stop sending the data.

![Live View](../../images/concepts/data-stream/IC_3.png)

## Further Reading

* [How to Use Live View](../../how-tos/data-streams/use-live-view.md)
