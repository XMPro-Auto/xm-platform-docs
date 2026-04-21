# Packaging Connectors

## Getting Started

The XMPro Package Manager is a Windows 11 desktop application that enables you to package a new Connector or update details for an existing Connector. [See the Connector article for more information on Connectors.](../../concepts/connector.md)

This application takes you through the process of specifying all the properties your Connector requires, adding or changing the controls for each user setting, and uploading the DLL files of the [Connector code](building-connectors.md). It will provide you, upon completion, with a file that can be uploaded to Application Designer after which you can use the Connector in App Pages.

You can download the software from the Microsoft Windows 10 Store or clicking [here](https://www.microsoft.com/en-us/p/xmpro-package-manager/9n3f4wnslgzk?activetab=pivot:overviewtab).

![](../../images/image-1163.png)

After installing the XMPro Package Manager, launch the application from the Microsoft Store or search for “XMPro Package Manager” in the Start menu and then click on “XMPro Package Manager”.

![](../../images/package-manager-interface.png)

## New / Import

On the first screen of the application, you can either create a new Connector package or import and update an existing one.

> [!NOTE]
> Use the arrows at the bottom of the page section to move forward or backward in the application.
>
> When you import an existing package, you have the option to export the package as a JSON file. This is useful either to compare packages or for source control and version management.
>
> You can also import the JSON file from an existing package, which is particularly useful if you need to modify translations added through the [Include Multilingual Support](packaging-connectors.md#include-multilingual-support) feature.

![](../../images/new-import-package.png)

## Details

The Details form allows you to specify or edit the properties of a Connector. These properties are listed and explained below.

![](../../images/image-1443.png)

### Name

The name of the Connector is what the Connector will be known as once it is uploaded to the Application Designer platform, for example, “_SQL Connector_”.

### Description

The description is a brief explanation of what the Connector does, for example, “_This Connector allows you to read/update a SQL Database table_“.

### Version

The [version](../../concepts/version.md) of the Connector. Any real number is acceptable, for example, "_1.02_".

> [!WARNING]
> If you make a change to an existing Connector, make sure you increment the version number as Application Designer will not allow you to upload two of the same Connectors with the same version.

### Entry Point

The entry point is the namespace and class name of the actual Connector’s DLL file.

For example, if a Connector with the class name “_Connector”_ is located in the _XMPro.AzureSQLConnectors_ namespace, the Entry Endpoint for it would be “_XMPro.AzureSQLConnectors.Connector”._

### Icon File

The icon used to represent your Connector. Click the _Browse_ button, navigate to where you’ve stored the file via the Explorer and select the new image file.

> [!NOTE]
> It is recommended that you upload either a JPG or PNG file with a size of 64×64 pixels to accommodate for retina displays.

## References

The References form is where you upload the file(s) required for the Connector to execute. Only files in the _Selected File(s)_ list will be included in the package, and any DLLs must be created in .NET.

To upload a file, click the _Browse_ button next to the _DLL File(s)_ field and navigate to where the files are located. Select all the files needed and click the _Add_ button to add them to the _Selected File(s)_ list.

To remove a file from the list, click the _Delete_ button next to the file name in the _Selected File(s)_ list.

<table><thead><tr><th width="132">Type</th><th>Description</th></tr></thead><tbody><tr><td>Plugin</td><td>The DLL file that was generated when you built the project containing your Connector source code.</td></tr><tr><td>Reference</td><td>Additional DLL file(s) referenced by the Plugin File, such as Newtonsoft.Json. <br>You do not need to upload the <em>XMIoT.Framework.dll</em> file as this DLL is automatically included.</td></tr><tr><td>Resource</td><td>Additional DLL file(s) needed by the Reference File. </td></tr></tbody></table>

![](../../images/image-1331.png)

## Settings

Depending on what your Connector does, it might require that the user provide certain information, such as a server URL, username, or password. For each of these information fields (or _settings_), you need to specify which control should be used and what each control represents, for example, the SQL Connector will require the user to add a server URL. The user should provide this value using a text-box control. Thus, you need to create a control with a type of “TextBox” and a caption that reads “Server URL” in the XMPro Package Manager application.

The following controls are available to be used to capture user input:

| <ul><li>Button</li><li>CheckBox</li><li>CheckList</li><li>DropDown</li><li>EditList</li><li>FileUpload</li></ul> | <ul><li>Filter</li><li>Grid</li><li>Group</li><li>HTML Editor</li><li>NumberBox</li></ul><p></p> | <ul><li>ScriptBox</li><li>TextBox</li><li>Title</li><li>TokenBox</li><li>VariableBox</li></ul><p></p> |
| --- | --- | --- |

Each control has several properties that have to be set and not all properties apply to all controls. For example, options apply to a drop-down control and not a text-box control.

The table below contains a list of all the available properties, their description, and to which controls they are applicable.

<table><thead><tr><th width="214.33333333333331">Property Name</th><th width="190">Control Type</th><th>Description</th></tr></thead><tbody><tr><td>Allow Custom Text</td><td>Drop-Down</td><td>Allows the user to type custom text in the drop-down field if checked.</td></tr><tr><td>Allow Custom Tokens</td><td>Token Box</td><td>Allows the user to add custom tokens if checked.</td></tr><tr><td>Caption</td><td>All</td><td>Text that will be displayed with the group or setting. The caption is usually one or two words, describing the value that should be provided by the user, for example, “Server URL”.</td></tr><tr><td>Default Value</td><td>Title</td><td>The default value of the title.</td></tr><tr><td>Font Size</td><td>Script Box</td><td>Size of the font in the Script Box.</td></tr><tr><td>Help Text</td><td>All, excluding Groups</td><td>If you need to provide the user with any additional information about the purpose of the setting or helpful instructions, specify it in this field.</td></tr><tr><td>Key</td><td>All</td><td>Uniquely identifies the group or setting.</td></tr><tr><td>Keywords</td><td>Script Box</td><td>Define your variables or other custom keywords here, so that they will be available in the editor’s IntelliSense.</td></tr><tr><td>Options <br>(Drop Down)</td><td>Drop-Down</td><td>Use the Options-area to add values to the drop-down menu by specifying the Text and Value fields and then clicking Save. You may also choose an option to be used as the default option by checking the “Set as Default Value” box.</td></tr><tr><td>Options <br>(HTML Editor)</td><td>HTML Editor</td><td>Allows you to specify placeholders that can be mapped to input fields in the input received by the Agent.</td></tr><tr><td>Postback</td><td>All</td><td>If checked, will cause the form to do a postback to retrieve values from the server when the field loses focus (when the user clicks out of the field).</td></tr><tr><td>Required</td><td>All, excluding Groups</td><td>The control will be validated to make sure that a value has been specified if this box is checked.</td></tr><tr><td>ScriptBox Height</td><td>Script Box</td><td>Height of Script Box.</td></tr><tr><td>ScriptBox Mode</td><td>Script Box</td><td>Language in which script has to be written.</td></tr><tr><td>ScriptBox Theme</td><td>Script Box</td><td><p>The theme of the Script Box. Themes available include the following:</p><ul><li>Ambiance</li><li>Chaos</li><li>Chrome</li><li>Clouds</li><li>Clouds_midnight</li><li>Cobalt</li><li>Cromson_editor</li><li>Dawn</li><li>Dreamweaver</li></ul></td></tr><tr><td>ScriptBox Width</td><td>Script Box</td><td>Width of Script Box.</td></tr><tr><td>Secure</td><td>All</td><td>The value of the control will be treated as a secure value if this box is checked (encrypted and not displayed on the form in plain text). An example of a secure value is a SQL Server password.</td></tr><tr><td>Show Grid Lines</td><td>Grid</td><td>The grid lines of the grid will be shown if checked.</td></tr><tr><td>Show Header</td><td>Grid</td><td>The header of the grid will be displayed, if checked.</td></tr><tr><td>Sort Index</td><td>All</td><td>This is used to determine the group or setting’s position and works with increments of 10. Adjust this value to move the group or setting up or down on the form.</td></tr><tr><td>Unique Key</td><td>Grid</td><td>Mark a specific column as being unique, for example, an identity column.</td></tr><tr><td>Visible</td><td>All</td><td>This field sets the initial visibility of the group or setting.</td></tr></tbody></table>

![](../../images/image-69.png)

### Adding Settings

Settings are grouped logically into one or more groups, such as authentication, criteria, and output.

Create a group first, then add controls for settings to the group. To do this, follow the steps below:

1. Click on the plus-icon (top right, next to the Settings header). A form section will open, allowing you to specify a group for the settings.
2. Specify a unique value that can be used as the key for the group.
3. Add the caption you would like to use.
4. Click _Save._
5. Next, we are going to add a setting. Click on the plus-icon next to the group you’ve created.
6. Choose the type of control you would like to use.
7. Add a unique key for your control. Please note that this key needs to correspond to what you defined in your code.
8. Add a caption for your control.
9. If needed, add a default value.
10. If required, add help text.
11. Select the options that apply from the list of check-boxes.
12. Click _Save_.

![](../../images/add-group.png)

![](../../images/add-setting.png)

## Output

### Export as JSON file

Tick the checkbox **Export as JSON file too?** if you would like to export the file as JSON too. It will later be saved to the same directory as the XMP file with the file name _category\_name\_version_.json.

### Include Multilingual Support

Tick the checkbox **Include Multilingual Support?** if you would like to add support for languages other than English. Uncheck languages you don't want to include.

This feature leverages generative AI to provide language translation. It is available only if the following requirements are met:

* You are connected to the internet.
* Open AI is configured (Click [here](packaging-connectors.md#configure-openai-api) for instructions on how to do so).

> [!NOTE]
>
> * **What is Translated:**  The Connector description and static properties added when packaging the Connector are translated, whereas internal messages and dynamic properties added when [building the Connector](building-connectors.md) are not.
> * **Minimum XMPro Product Version:** The tables below outline the minimum versions of XMPro App Designer (AD) and XMPro Package Manager (PM) required for multilingual support.
> * **If Automated Translations Are Incorrect:** Edit the translations in the JSON file and repackage it with an incremented version number.
>  
>   <table style="width:100%; table-layout:fixed;">
>    <thead>
>      <tr>
>        <th style="width:49%;">AD Multilingual Support</th>
>        <th style="width:17%;">Pre v4.4.16</th>
>        <th style="width:17%;">v4.4.16+</th>
>        <th style="width:17%;">v4.5.4+</th>
>      </tr>
>    </thead>
>    <tbody>
>      <tr>
>        <td>Internal messages and dynamic properties</td>
>        <td>✗</td>
>        <td>✗</td>
>        <td>✗</td>
>      </tr>
>      <tr>
>        <td>Connector description and static properties</td>
>        <td>✗</td>
>        <td>✓</td>
>        <td>✓</td>
>      </tr>
>      <tr>
>        <td>Static property drop-down options</td>
>        <td>✗</td>
>        <td>✗</td>
>        <td>✓</td>
>      </tr>
>    </tbody>
>   </table>
>  
>   <table style="width:100%; table-layout:fixed;">
>     <thead>
>       <tr>
>         <th style="width:49%;">PM Multilingual Support</th>
>         <th style="width:17%;">Pre v1.3.18</th>
>         <th style="width:17%;">v1.3.18+</th>
>         <th style="width:17%;">v4.5.4+</th>
>       </tr>
>     </thead>
>     <tbody>
>       <tr>
>         <td>Internal messages and dynamic properties</td>
>         <td>✗</td>
>         <td>✗</td>
>         <td>✗</td>
>       </tr>
>       <tr>
>         <td>Agent description and static properties</td>
>         <td>✗</td>
>         <td>✓</td>
>         <td>✓</td>
>       </tr>
>       <tr>
>         <td>Static property drop-down options</td>
>         <td>✗</td>
>         <td>✗</td>
>         <td>✓</td>
>       </tr>
>     </tbody>
>   </table>

![](../../images/pm-output-1.png)

### Configure OpenAI API

1. Click _Configure OpenAI._
2. A form will open for you to add or modify the OpenAI Endpoint and Api Key.
3. Click _Save._

![PM Config OpenAI](../../images/configure-openai.png)

## Review: Details

Lastly, you can navigate back through the steps to review the details that you’ve specified. If you are satisfied, complete the wizard by clicking the Save button below before navigating to the folder where you would like the package to be exported. Your package will be created with the file name _category\_name\_version_.xmp.

> [!NOTE]
> If you imported an existing file, take care to:
>
> * either click 'Save as new Connector' to generate a new Connector, or click 'Save' to generate a new version of the original Connector.
> * ensure you select a different location folder or increment the version to avoid overwriting the original.

![](../../images/pm-success-connector.png)

## Further Reading

* [How to upload your new Connector to Application Designer](manage-connectors.md)

> [!NOTE]
> You need to have the correct permissions set against your user to be able to edit and upload Connectors. This is a role not typically given to all users.
