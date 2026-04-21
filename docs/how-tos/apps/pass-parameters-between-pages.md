# Pass Parameters Between Pages

You can use Parameters if you want to send particular values to another Page. For example, if you have a list of machines, and a user selects one, the Application may open a new Page that displays information for that particular machine. In that case, you may want to pass the ID of the machine the user clicked on to the Page that is being opened.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Navigating between Pages.
>
> * [Navigation and Parameters](../../concepts/application/navigation-and-parameters.md)
> * [How to Navigate Between Pages](navigate-between-pages.md)

## Adding a Parameter to the Page

A Parameter needs to be added to the Page that is receiving the data. In this example, there are two Pages that exist in the Application: the main Landing Page and the secondary Page. The second page is the Page where the Parameter is made. To add a Parameter to a page, follow the steps below:

1. Click on _Applications_ from the left-hand menu.
2. Click on the _edit_ button of the Application from the list.

![Screenshot of the Applications list view showing multiple application cards with their name, description, and action buttons. An Edit button is highlighted on one of the application cards.](../../images/apps/add-parameter.png)

3\. Click on the page where you want to data to be sent to.  
4\. Click on _Page Data_.  
5\. Click on the _plus_ to add a Parameter.

![Screenshot of the Page Data panel with the plus button highlighted, used to add a new parameter to the page. The panel shows a list of existing parameters and their types.](../../images/apps/parameters/params-2.png)

6\. Add the name and type of the new Parameter.  
7\. Click on _Create_.  
8\. Click on _Save_.

![Screenshot of the Create Parameter dialog box where a new parameter named "MachineID" is being created with the type set to "string". The Create and Cancel buttons are shown at the bottom of the dialog.](../../images/apps/parameters/param-create.png)

Now that a Parameter has been added, create a textbox or a way to display the value when it is passed to the Page during runtime.

1. Add a textbox to the Page so you will be able to display the value when it is passed from the main page to this page.

![Screenshot showing a textbox component being added to the page from the Block Components panel. The textbox is being dragged onto the canvas area.](../../images/apps/parameters/params-4.png)

2\. Click on _Block Properties_.  
3\. Click on the '_A_' button to toggle between static and dynamic text.  
4\. Select the Parameter from the dropdown.  
5\. Click on _Save_.

![Screenshot of the Block Properties panel for a textbox. The "A" toggle button is highlighted, indicating a switch to dynamic text mode. The MachineID parameter is selected from the dropdown menu.](../../images/apps/parameters/params-5.png)

The data has to be sent from the main page to the secondary page. To pass data from the main Landing Page using the Parameter you just created, follow the steps below:

1. Go to the page you will be sending data from.
2. Select the button/link that navigates to the second page.
3. Click on _Block Properties_.
4. Click on the _Edit_ button under Pass Page Parameters.
5. Configure if the data being passed is dynamic or static.
6. Add/Select a value that you would like to pass to the parameter on the second page.
7. Click on _Apply_.

![Screenshot of the Block Properties panel showing the Navigate To section with a Page selected. The "Edit" button for Pass Page Parameters is highlighted, indicating where to configure parameters to send to the destination page.](../../images/apps/parameters/params-6.png)

![Screenshot of the Pass Page Parameters dialog. A parameter named "MachineID" is configured to receive a static value "Machine123". The dialog shows options to set the parameter type and value.](../../images/apps/parameters/params-7.png)

## Passing Dynamic Data to the Page

When navigating between pages, you can also pass dynamic data - such as the Chart value - to the next page using page parameters. First, configure the [Chart](../../blocks-toolbox/visualizations/chart.md) block then follow the steps below:

1. Click on Block Properties.
2. Under _'_Appearance' set Show Drilldown to True.

![Screenshot of the Block Properties panel for a Chart component. The Appearance section is expanded, and the "Show Drilldown" toggle is turned on, enabling chart drilldown functionality.](../../images/apps/chart-drilldown/chart-drilldown-1.png)

3\. Under 'Action', click on the Navigate To Dropdown and select Page.

4\. Select the page you want to navigate to.

5\. Click Pass Page Parameters.

6\. Pass Page Parameter blade will open.

![Screenshot showing the Pass Page Parameters dialog open for chart drilldown configuration. The dialog displays existing parameters that can receive values when a chart element is clicked.](../../images/apps/chart-drilldown/chart-drilldown-2.png)

7\. Type in the name of the parameter and select the type.

8\. Click Add.

![Screenshot of the parameter configuration in the Pass Page Parameters dialog. A new parameter is being created with a name and type specified, and the Add button is highlighted.](../../images/apps/chart-drilldown/chart-drilldown-3.png)

9\. Change the field type to Dynamic Value.

10\. Select the Chart value you want to pass on the next page.

11\. Click _Apply_.

![Screenshot showing the dynamic value configuration for a chart parameter. The dropdown menu shows available chart values like "Category", "Series", and "Value" that can be passed to the parameter.](../../images/apps/chart-drilldown/chart-drilldown-4.png)

## View values passed to other pages at runtime

Once the Parameter has been configured, launch the application to see how the data will be passed between Pages at runtime.

1. Click on _Launch_.

![Screenshot of the application editor with the Launch button highlighted in the top toolbar. This button is used to preview the application at runtime.](../../images/apps/parameters/params-8.png)

2\. Click on the link that goes to the second page.  
3\. The data sent from the first page should reach the second page.

![Screenshot showing the application in runtime view with a button labeled "Go to Details Page". This button will navigate to another page while passing parameters.](../../images/apps/parameters/params-9.png)

![Screenshot of the destination page showing the parameter value "Machine123" displayed in a textbox. This demonstrates successful parameter passing between pages.](../../images/apps/parameters/params-10.png)

## Edit a Parameter

To edit a Parameter, follow the steps below:

1. Click on _Page Data_.
2. Click on the _pencil/edit_ button for the Parameter.

![Screenshot of the Page Data panel showing a parameter named "MachineID". The pencil/edit icon next to the parameter is highlighted, indicating where to click to edit the parameter.](../../images/apps/parameters/params-11.png)

3\. Make changes to the Parameter.  
4\. Click on _Save_.

![Screenshot of the Edit Parameter dialog box. The parameter's name and type can be modified, and Save and Cancel buttons are available at the bottom of the dialog.](../../images/apps/parameters/params-12.png)

## Delete a Parameter

To delete a Parameter, follow the steps below:

1. Click on _Page Data_.
2. Click on the _pencil/edit_ button for the Parameter.

![Screenshot of the Page Data panel with the pencil/edit icon highlighted next to a parameter, showing where to click to access parameter deletion options.](../../images/apps/parameters/params-11.png)

3\. Click on _Delete._

![Screenshot of the Edit Parameter dialog with the Delete button highlighted at the bottom. This button will remove the parameter from the page.](../../images/apps/parameters/params-14.png)

4\. Confirm that you would like to delete the Parameter.

![Screenshot of the confirmation dialog asking "Are you sure you want to delete this parameter?" with "Yes" and "No" buttons to confirm or cancel the deletion.](../../images/apps/parameters/params-15.png)
