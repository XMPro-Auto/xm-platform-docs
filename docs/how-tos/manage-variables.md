# Manage Variables

XMPro Variables are placeholders used to hold and maintain certain values. If you may not know some of the values that you might want to use within an XMPro Object, such as credentials or passwords, you can use Variables where the real value can be substituted later.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Variables.
>
> * [Variable](../concepts/variable.md)

## Adding a new Variable

Variables can be added via the Variables page before being used in any of the Data Streams or Applications.

1. Click on the _Variables_ page from the left-hand menu.
2. Click on _Add_.
3. Enter the details of the new Variable.
4. Choose if the value is encrypted. This determines whether or not the value can be seen by the user.
5. Click on _Save and Close._

![Adding a new Variable](../images/manage-variables-1.png)

## Using Variables

Variables can be used in Data Streams or Applications to authenticate users or to access certain data sources. Consider having the following agents in a stream:

* Azure SQL Listener

When the Azure SQL Listener is configured the user needs to enter the server details and password in order to access the available tables and columns. In this case, variables that already store the passwords and credentials can be used in the input fields. For example:

1. Add an SQL Listener from the list of Agents.
2. Click on Configure.
3. Select the Server and user details from the list of variables (ensure that the 'Use Connection Variables' option is selected).

![Select Server and user details](../images/manage-variables-2.png)

   4\. Select the correct encrypted password variable for the server.

![Select encrypted password variable](../images/manage-variables-3.png)

   5\. If selected correctly, tables and columns can now be accessed.

![Access tables and columns](../images/manage-variables-4.png)

## Removing Variables

### Single Variable

To remove a single variable, follow the steps below:

1. Open the _Variables_ page from the left-hand menu.
2. Select the variable from the list.
3. Click _Delete_.

![Remove a single variable](../images/manage-variables-5.png)

   4\. Confirm that you would like to delete the variable.

![Confirm deletion](../images/manage-variables-6.png)

### Multiple Variables

To remove multiple variables, follow the steps below:

1. Open the _Variables_ page from the left-hand menu.
2. Click _Select_.
3. Select the variables from the list.
4. Click _Delete_.

![Remove multiple variables](../images/manage-variables-7.png)

   5\. Confirm that you would like to delete the selected variables.

![Confirm deletion of multiple variables](../images/manage-variables-8.png)

## Overriding Variables

The Variables defined can be overridden by the individual Stream Host to provide the unique configuration e.g. per Asset, site, or OPC IP Address. See [How to Override Variables](stream-host.md#how-to-override-variables) for more information.
