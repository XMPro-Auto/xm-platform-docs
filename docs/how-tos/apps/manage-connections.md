# Manage Connections

The parameters defined in a Connection allow the App to connect to a source of data like a SQL Database and expose the entities as Data Sources within the Page. Connection parameters can include credentials such as a username, password, path, URL, or location identifier that you can use to make a remote connection to the Data Source.

For example, Connection parameters to connect to an SQL Database would include the Server Name, Authentication type, Username, and password.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Data Integration.
>
> * [Data Integration](../../concepts/application/data-integration.md)
> * [How to Manage Pages](manage-pages.md)

## Adding a Connection to the Application

Connections can be added directly to an Application by adding it to the App Data. To add a Connection to an Application, follow the steps below:

1. Open the _Applications_ page from the left-hand menu.
2. Click on the _edit_ button to edit an application from the list.

![Screenshot of the Applications list page showing multiple application cards with their titles, descriptions and action buttons. Each card has an Edit button highlighted that allows editing the application.](../../images/apps/connections/app-edit.png)

![Screenshot showing the application editor with the main navigation panel on the left. The Applications section is highlighted, showing where to access the list of applications.](../../images/apps/connections/conn-1.png)

3\. Click on _App Data._  
4\. Click on _add._  
5\. Select a connector, for example, the SQL connector.  
6\. Enter the details of the Connection, including it's name.  
7\. Click on _Save_.

![Screenshot of the connection configuration dialog. The SQL connector is selected, and a form is displayed with fields for connection details including server name, authentication type, database name, username and password. The Save button is highlighted at the bottom.](../../images/apps/connections/conn-2.png)

The new Connection should appear in the list of connectors, and can now be used in the application to add Data Sources. The Connection can be used for all pages within the application it was added to.

![Screenshot of the App Data panel showing a list of existing connections. A newly added SQL connection appears in the list with its name, type, and description visible.](../../images/apps/connections/conn-3.png)

## Deleting a Connection

### Single Connection

To delete a single Connection, follow the steps below:

1. Open the _Applications_ page from the left-hand menu.
2. Click on the _edit_ button to edit an application.

![Screenshot of the Applications list showing how to access the edit function for an existing application. The Edit button is highlighted on one of the application cards.](../../images/apps/connections/conn-1.png)

3\. Click on _App Data._  
4\. Select the Connection.  
5\. Click on _Delete._  
6\. Confirm that you want to delete the Connection.

![Screenshot showing the App Data panel with a connection selected. The Delete button is highlighted in the top toolbar, indicating where to click to remove the selected connection.](../../images/apps/connections/conn-5.png)

### Multiple Connections

To delete multiple Connections, follow the steps below:

1. Open the _Applications_ page from the left-hand menu.
2. Click on the _edit_ button to edit an application.

![Screenshot of the Applications list page with the Edit button highlighted on an application card, showing how to access the application editing interface.](../../images/apps/connections/conn-1.png)

3\. Click on _App Data._  
4\. Click on _Select_.  
5\. Select multiple Connections to be deleted.  
6\. Click on _Delete_.

![Screenshot of the App Data panel in multi-select mode. Multiple connections are selected with checkboxes, and the Delete button is highlighted in the toolbar, showing how to delete multiple connections at once.](../../images/apps/connections/conn-7.png)

7\. Confirm that you want to delete the Connection.

![Screenshot of the confirmation dialog asking "Are you sure you want to delete these connections?" with Yes and No buttons. This appears when attempting to delete multiple connections.](../../images/apps/connections/conn-8.png)

> [!NOTE]
> You can cancel the multi-select by clicking on the select button again.

## Data Stream Connections

Navigate to the Data Stream Connector to access a comprehensive inventory of the Data Stream Connections for the Application. The connections are categorized based on the respective pages where they are utilized.

You can use this list to verify the current version of the Data Stream in use and make any necessary updates if required.

![Screenshot of the Data Stream Connections panel showing a list of data streams used in the application. Each connection displays its name, type, and version information, organized by the pages where they are used.](../../images/apps/connections/data-stream-connections.png)

## Further Reading

* [How to Manage Data Sources](manage-data-sources.md)
