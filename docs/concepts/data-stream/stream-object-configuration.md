# Stream Object Configuration

## Data Stream and Agent Configuration

### User Settings

All [Agents](../agent/index.md) will individually be associated with a [Collection](../collection.md). This Collection may or may not be different from the default Collection set for your Data Stream. This setting will always be listed among the rest of the user settings.

There are a number of Agents that do not require any settings, for example, the Event Printer Agent. This Agent simply prints events and you do not need to specify settings such as a server URL, username, password, or upload a file.

Other Agents, however, require settings to be filled in before you can successfully run the stream. For example, consider having a CSV listener Agent in your Data Stream. The CSV listener Agent will require you to specify the following values:

* Specify a polling interval (seconds)
* Upload a CSV file
* Specify the CSV definition (name of each column in the CSV file along with what data type the values in each column are)

If these values have been provided correctly, the data will be read from the CSV file you specified when you [publish](../../how-tos/publish/index.md) your stream.

![](../../images/concepts/data-stream/image-451.png)

## Input Mapping and Arrow Configuration

Some Agents allow inputs to be mapped if the _Require Input Map_ property has been set to _true_ during [packaging](../../how-tos/agents/packaging-agents.md). What Input Mapping allows you to do is to specify that a specific Agent receives its input in a specific structure. This causes the arrows leading to an Agent to be made configurable and will allow the user to map the inputs of an agent to incoming attributes, for example:

Consider having the following Agents in a stream:

* CSV Listener
* SQL Server Writer

The CSV Listener is configured to get data from a file that contains the following headings:

* Timestamp (of type _DateTime_)
* ReadingNo (of type _Long_)
* Temperature\_A01 (of type _Double_)
* Vibration\_A01 (of type _Double_)
* Result (of type _Double_)

![](../../images/concepts/data-stream/image-1182.png)

The task the SQL Server Writer needs to perform is to write the data it receives to a SQL Server database, but it expects the structure of the data to be in a specific format. The table we need to write the data to has the following columns:

* ID (bigint, identity column)
* ReadingNo (bigint)
* Temperature (float)
* Vibration (float)
* Results (float)
* Timestamp (datetime)

For the data to be written to the database in a specific format, you need to map the correct columns in the CSV file to the correct SQL Server table columns. To do this, both the CSV Listener and the SQL Server Writer Agents need to be configured first. To configure an Agent, click on the Agent and then on the “_Configure_” button. Fill in all the details required, for example, the SQL Server instance name and credentials.

Next, you can go ahead and configure the Input Mapping by clicking on the arrow that connects the CSV Listener and the SQL Server Writer Agents. Then, click on “_Configure_“. Choose which column should be mapped to which column by selecting the correct value from the drop-down menu for each row. Please note that the data types of the items being mapped to each other need to be the same. If not, the value in the left column will be disabled and you will not be able to select it.

Remember that, even though the same principle applies to all Agents, input mapping might be done differently for different Agents.

![](../../images/concepts/data-stream/image-274.png)

### Mapping Functions

In some cases, you might have to map a large number of inputs for an Agent. Some functions have been implemented to make the process of mapping a large number of fields easier, such as _Match by Expression_, _AutoMap_, and _Show Unmapped_.

#### AutoMap

By clicking on the “_AutoMap”_ button, Data Stream Designer will match all the fields that are common between the Agents involved, for example, if you look at the stream in the image below, you will notice that both the SQL Server Writer Agent and the CSV Listener has the fields listed below in common, which will automatically be mapped if they have the same data type.

* ReadingNo
* Timestamp

![](../../images/concepts/data-stream/image-654.png)

#### Match by Expression

The _Match by Expression_ function allows for an expression to be used to make mapping a large number of fields easier and quicker. The fields can be mapped by using any of the following options:

* Prefix
* Postfix
* Expression

![](../../images/concepts/data-stream/image-1030.png)

The **Prefix** option allows you to specify that columns should be matched based on the first part of a column name, for example:

* In the CSV listener Agent, there is a column named “A01\__Temperature_“
* In the SQL Server Writer Agent, there is a column named “_Temperature_“

In the images below, “_A01” is specified as the postfix. Based on the prefix given, the column “A01_\__Temperature_” in the CSV Listener can be matched to the column “_Temperature_” in the SQL Server Writer Agent.

![](../../images/concepts/data-stream/image-559.png)

![](../../images/concepts/data-stream/image-972.png)

The **Postfix** option allows you to specify that columns should be matched based on the last part of a column name, for example,

* In the file uploaded to the CSV listener Agent, there are columns named “_Temperature\_A01_“ and “_Vibration\_A01_“
* In the table referenced in the SQL Server Writer Agent configurations, there are columns named “_Temperature_“ and “_Vibration_“

In the images below, “_\_A01_” is specified as the postfix. Based on the postfix given, the columns “_Temperature\_A01_“ and “_Vibration\_A01_“ in the CSV Listener can be matched to the columns “_Temperature_“ and “_Vibration_“ in the SQL Server Writer Agent.

![](../../images/concepts/data-stream/image-1405.png)

![](../../images/concepts/data-stream/image-1398.png)

The **Expression** option allows you to use a regular expression to match the columns, for example,

* In the file uploaded to the CSV Listener Agent, there is a column named “_Device\_Temperature\_Fahrenheit_“
* In the table referenced in the SQL Server Writer Agent configurations, there is a column named “_Temperature_“

In the images below, “_Device\_$1\_Fahrenheit_” is used as the regular expression. Based on this expression, the column “_Device\_Temperature\_Fahrenheit_” in the CSV listener is mapped to the column “_Temperature_” in the SQL Server Writer Agent.

![](../../images/concepts/data-stream/image-1094.png)

![](../../images/concepts/data-stream/image-1041.png)

#### Show Unmapped

The **Show Unmapped** function allows you to filter the rows displayed, based on if the columns have been mapped. If you chose to filter items based on if they are mapped or not, all the records that haven’t been mapped yet will be listed, for example,

* In the image below, “_ReadingNo_” and “_Timestamp_” have been mapped for both Agents using the _AutoMap_ function. However, there are three records that remain that need to be mapped. In some scenarios, there might be a lot more records with some being mapped and others not.

![](../../images/concepts/data-stream/image-554.png)

![](../../images/concepts/data-stream/image-847.png)

## Further Reading

* [How to Manage Input Mappings](../../how-tos/data-streams/setup-input-mappings.md)
* [How to Configure a Stream Object](stream-object-configuration.md)
