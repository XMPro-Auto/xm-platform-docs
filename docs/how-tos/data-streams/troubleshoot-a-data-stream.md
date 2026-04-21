# Troubleshoot a Data Stream

When creating and configuring a Data Stream, there is a chance it may not be working as expected, and you may have to find out more information as to why it is not behaving the way it should. There are a few options available on how to troubleshoot a Data Stream. Troubleshooting is required if you want to make sure the flow of data is accurate.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Data Streams.
>
> * [Data Stream](../../concepts/data-stream/index.md)
> * [How to Manage Data Streams](manage-data-streams.md)

## Troubleshoot using Live View

To troubleshoot using the Live View, follow the steps below:

1. Click on _Publish_.

![Click Publish button to publish the data stream](../../images/data-streams/troubleshooting/ts-1-1.png)

1. Click on _Live View_.
2. Select the Agent/s to view the Live Data for.
3. Click _Save_.

![Select agents in Live View to monitor data flow](../../images/data-streams/troubleshooting/ts-2-1.png)

> [!NOTE]
> If data is not being displayed when it should be, or if the values are not being displayed as expected, something may be going wrong with the Agent.

![Live View interface showing data stream monitoring](../../images/data-streams/troubleshooting/manage-ds-howtoopen2.png)

![Example of live data being displayed](../../images/data-streams/troubleshooting/ts-4.png)

## Troubleshooting using Error Endpoints

To Troubleshoot using the Error Endpoints, follow the steps below:

1. Drag an _Event Printer_ agent onto the canvas. They can be found under 'Action Agents.'
2. Add an arrow from the error endpoint connected to the Event Printer.
3. Click on _Publish_.

![Using Event Printer to capture errors from error endpoints](../../images/data-streams/troubleshooting/ts-5-1.png)

1. Click on _Live View_.
2. Select the _Event Printer_.
3. Click _Save_.

![Viewing error output in Event Printer](../../images/data-streams/troubleshooting/ts-6.png)

## Troubleshooting when there is no data visible

In some cases, the Event Printer does not show any data when trying to troubleshoot the Data Stream. If this is the case, the Collections Stream Host may be able to give some information.

1. Open the _Collections_ page from the left-hand menu.
2. Click on the _Collection_.
3. Click on _Stream Hosts_.
4. Select the Stream Host.
5. View the logs from the Stream Host.

> [!NOTE]
> Any errors that are generated from an Agent which are printed from the error endpoint are also printed in the Stream Host logs.

![Accessing Stream Host logs from Collections page](../../images/data-streams/troubleshooting/image-1005.png)

## Troubleshooting when there are no Stream Hosts

If the Stream Host is not running at all, you can view the logs from the install directory of the Stream Host on your computer. The install folder is named _XMPro Stream Host_ and is usually found in the _Program Files_ in the _C Drive_.

![Stream Host installation directory location](../../images/data-streams/troubleshooting/image-1333.png)

![Navigating to Stream Host logs in Program Files](../../images/data-streams/troubleshooting/troubleshoot-9.png)

![Stream Host logs directory structure](../../images/data-streams/troubleshooting/troubleshoot-10.png)

![Viewing Stream Host log files for troubleshooting](../../images/data-streams/troubleshooting/troubleshoot-11.png)
