# Stream Host

A Stream Host is an application that can either be installed as a Docker container, a Windows Service, or a Console Application. Stream Hosts enable Data Streams to run and execute actions and are also responsible for getting the configurations of [Non-Virtual Agents](../concepts/agent/virtual-vs-non-virtual-agents.md#non-virtual-agents).

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Stream Host.
>
> * [Stream Host](../concepts/collection.md#stream-hosts)

## How to Deploy a Stream Host

The recommended Stream Host deployment is as a Docker container - see the [Docker](../installation/complete-installation/install-stream-host/docker.md) instructions.

For installation instructions, see [Deploy Stream Host](../installation/complete-installation/install-stream-host/docker.md).

## Logs

### How to Check Logs

To check the logs for a Steam Host,  follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.
4. Select the desired Stream Host.

![Stream Host Logs](../images/stream-host-logs.png)

### How to Set the Log Level

You can change the Log level to either Info or Trace. To change the Log Level, follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.
4. Select the desired Stream Host.

> [!NOTE]
> [See the Collection and Stream Hosts article for more information on the Log Level.](../concepts/collection.md#set-log-level)

![Stream Host Log Level](../images/stream-host-log-level.png)

   5\. Click on Set Log level.\
   6\. From the dropdown, select either Info or Trace.

![Stream Host Log Level Select](../images/stream-host-log-level-select.png)

   7\. Click on OK.

![Stream Host Log Level OK](../images/stream-host-log-level-ok.png)

### How to Filter Log Levels

You can filter and narrow down the errors and messages that have already been logged in the table. For example, if you filter for _Info_ errors, only info level errors will be displayed. To filter the log level for a Steam Host,  follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.
4. Select the desired Stream Host.

![Stream Host Filter Logs](../images/stream-host-filter-logs.png)

   5\. Click the icon next to the Level column.\
   6\. Select the Log Level.\
   7\. Click OK.

![Stream Host Filter Logs Select](../images/stream-host-filter-logs-select.png)

### How to Clean the Logs

To clean the logs for a Steam Host,  follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.
4. Select the desired Stream Host.

![Stream Host Clean Logs](../images/stream-host-filter-logs.png)

   5\. Click the Delete Logs button.\
   6\. Confirm your action.

![Stream Host Clean Logs Confirm](../images/stream-host-clean-logs-confirm.png)

### How to Export Logs

To export the logs for a Steam Host,  follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.
4. Select the desired Stream Host.
5. Click the "three dots" button.
6. Click Export all data or Export Selected rows.

![Stream Host Export Logs](../images/stream-host-export-logs.png)

## How to Find Online Hosts

To find online Stream Hosts, follow the steps below:

1. Open the Collection page.
2. Select the Collection.
3. Click the Stream Hosts button.

![Stream Host Find Online](../images/stream-host-find-online.png)

## How to Override Variables

Although each Stream Host in a given Collection downloads the same definition of a Data Stream, the [Variables](manage-variables.md) defined in Data Stream Designer can be overridden by the individual Stream Host to provide the unique configuration e.g. per Asset, site, or OPC IP Address.

The options to override variables for a Stream Host are:

* [Using Environment Variables](stream-host.md#using-environment-variables) - enables the scalable and efficient creation of multiple Docker Stream Hosts through scripting.
* [Using Variables.xv files](stream-host.md#using-variablesxv-files) - requires manual edits for each Stream Host.

In practice you'd use one or the other, but it may be helpful that the Stream Host

The Stream Host retrieves variable values in the following order:

1. Environment Variable, if no match then...
2. Variables.xv File, if no match then...
3. Variables (i.e. as detailed in [Using a Variable](../concepts/variable.md#using-a-variable))

### Using Environment Variables

_v4.4.2_

This option can be applied to any Stream Host install scenario, although it is better suited for when running [Stream Host on Docker](../installation/complete-installation/install-stream-host/docker.md).

Create an environment variable that is applied to a running Stream Host instance, prefixing the name of the variable that should be overridden with `xmvariable__`

```bash
xmvariable__NameOfVariable1=foo
xmvariable__NameOfVariable2=bar
xmvariable__NameOfVariable3=noop
```

### Using Variables.xv files

> [!NOTE]
> This option is not supported when running Stream Host on Docker.

1. Open the Collection page.
2. Select the Collection.
3. Hover on More.
4. Click Variables.
5. Click Select file and upload the encrypted variables.xv file, found in the Data folder of the Stream Host's installation directory e.g. "_C:\Program Files\XMPro Stream Host\Data_".
6. You can enter overrides for any Variables.
7. Click Download to get the updated file.
8. Replace the original file in your Stream Host folder with the new one.
9. Restart your Stream Host to load the updated variables.

![Stream Host Variables 1](../images/stream-host-variables-1.png)

![Stream Host Variables 2](../images/stream-host-variables-2.png)
