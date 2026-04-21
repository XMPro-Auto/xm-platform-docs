# Power BI

Power BI is a control that allows you to embed reports inside your application. Power BI is a business analytics service that provides a platform where users can create interactive visualizations of data that can be used on reports or event boards. For more details, visit the [official Microsoft website](https://powerbi.microsoft.com/en-us/what-is-power-bi).

![](../../images/image-686.png)

## Power BI Properties

### Appearance

#### Common Properties

Options for the appearance include its _visibility_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

### Behavior

#### Use Variables

This allows you to choose between manually entering a value for the _Report ID_ or selecting from a static variable. If the Application Mode is set to 'Application', Use Variables will also allow you to select a static variable for the _Group Id, Tenant Id, Application Id, and Application Secret._

![](../../images/power-bi-1.gif)

#### Report Id

The report Id can be found inside the URL of the report you want to embed. To find the report's Id:

1. Sign in Power BI.
2. Open the report you want to embed.
3. Copy the GUID from the URL. The GUID is the number between **/reports/** and **/ReportSection.** For example, if the url has **.../reports/de0db6db-232f-b5b5-1abe1d71da76/ReportSection....**, the report Id you would enter is **de0db6db-232f-b5b5-1abe1d71da76.**

The Report Id property is required for the Power BI Block.

#### Authentication Mode

There are two options for the authentication mode: _user_ and _application_.

User authentication is used when you want to embed the report for your organization. The users will be required to sign in and have a Power BI account. This will also require you to have a Power BI embedded license for this.

Application authentication will embed the contents of the Power BI report into the page and the user will not be asked to sign in to view the report. In order to set up application authentication, the _group Id, tenant Id, Application Id_, and _Application secret_ of your report need to be entered. For more information about where to find the value for these fields, [read the official Microsoft Documentation](https://docs.microsoft.com/en-us/power-bi/developer/embedded/embed-sample-for-your-organization?tabs=net-core).

If the Authentication mode is set to 'Application', the Group Id, Tenant Id, Application Id, and Application Secret properties are required for the Power BI Block.
