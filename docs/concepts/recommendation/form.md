# Form

A Form is a collection of fields that appear on [Recommendation Alerts](recommendation-alert.md). Forms are how relevant information can be entered and changed over the course of resolving an Alert. Forms can also contain buttons that allow specific actions to be performed in other business systems, like creating a work order in your EAM system. The Action Request Agent in the [Data Stream Designer](../data-stream/index.md) will pass the data from your form to other systems.

> [!NOTE]
> [See the Action Requests article for more details on Action Requests](action-requests.md).

When a [Recommendation Alert](recommendation-alert.md) is created from the [Rule](rule.md), the Rule's selected Form is used to determine the [fields (Blocks)](form.md#blocks) that will appear in the alert. Forms are managed through the Recommendations page.

![Form Configuration Interface](../../images/image-1614.png)

The same form can be seen as created in a Recommendation Alert:

![Form in Recommendation Alert](../../images/image-898.png)

## Category

Forms can be organized into different categories. This refers to the category under which the Form is found in the Form list. This category is separate from the [App and Data Stream Categories](../category.md).

## Actions on the Form

The following Actions can be taken on a Recommendation Form:

<table><thead><tr><th width="199">Action</th><th>Description</th></tr></thead><tbody><tr><td><a href="form.md#blocks">Blocks</a></td><td>Opens the list of Blocks that are available to the Form.</td></tr><tr><td>Properties</td><td>Opens the properties for the selected Block.</td></tr><tr><td>Save</td><td>Saves any changes made to the Form up to this point.</td></tr><tr><td>Discard</td><td>Discards any changes made to the Form up to this point.</td></tr><tr><td>Settings</td><td>Opens the Form Settings, where you can modify the Form's Name and Category or delete the Form.</td></tr><tr><td><a href="../version.md">Manage Versions</a></td><td>Versioning for the Form.</td></tr><tr><td><a href="../manage-access.md">Manage Access</a></td><td>Allows you to manage which users are allowed to view or modify this Recommendation and the Recommendation Alerts created by this Recommendation.</td></tr><tr><td><a href="../../how-tos/import-export-and-clone.md">Clone</a></td><td>Clones the Form as a new Form.</td></tr><tr><td><a href="../../how-tos/import-export-and-clone.md#exporting">Export</a></td><td>Export the Form as an encrypted file.</td></tr><tr><td>Delete</td><td>Deletes the Form.</td></tr></tbody></table>

## Blocks

The following Blocks can be added to a Recommendation Form:

<table><thead><tr><th width="199">Name</th><th>Description</th></tr></thead><tbody><tr><td>Text</td><td>A control that displays text.</td></tr><tr><td>Textbox</td><td>A control for the user to input text.</td></tr><tr><td>Text Area</td><td>A control for the user to input a large amount of text (multiline).</td></tr><tr><td>Numberbox</td><td>A control for the user to input a numeric value.</td></tr><tr><td>Datebox</td><td>A control for the user to input a date.</td></tr><tr><td>Checkbox</td><td>A control that allows the user to tick an option.</td></tr><tr><td>Dropdown</td><td>A control that allows the user to select from a predefined list.</td></tr><tr><td>Grid</td><td>A control that displays tabular data, updated as a JSON Array by an <a href="https://xmpro.gitbook.io/update-recommendation">Update Recommendation Agent</a> in a Data Stream. It is read-only when viewed in App Designer. <br>It is used to add information for users reviewing or resolving Recommendation Alerts, such as a Data Stream configured to listen for changes in an external work order system and update the Alert.</td></tr><tr><td>Button</td><td>A control that can be clicked to trigger an event or action.</td></tr></tbody></table>

Blocks are added to the Form by dragging from the Blocks tab.

![Adding Blocks to Form](../../images/image-1748.png)

Blocks can be re-ordered by dragging them up and down

![Reordering Form Blocks](../../images/image-583.png)

The properties of a Block are available in the Properties tab after clicking on a Block to select it. A Block can also be deleted by clicking on the delete button in the selection toolbar:

![Block Properties and Delete](../../images/image-607.png)

### Block Properties

<table data-header-hidden><thead><tr><th width="201">Property</th><th>Description</th></tr></thead><tbody><tr><td><strong>Property</strong></td><td><strong>Description</strong></td></tr><tr><td>Name</td><td>Name of the recommendation. This is usually one or two words that describe the form.<br>Name is how the Block is differentiated for Data Stream Agents.</td></tr><tr><td>Caption</td><td>The caption is displayed above the Block.</td></tr><tr><td><em>(Text)</em><br>Caption Style</td><td>The style of the text Block. Options include <strong>Heading 1</strong> - <strong>4</strong>, <strong>Body</strong>, <strong>Metric</strong>, and <strong>Small Text.</strong></td></tr><tr><td>Read Only</td><td>A flag that determines whether the field will allow a new value to be added on the Alert.</td></tr><tr><td>Required</td><td>A flag that determines whether the Block must have a value before the Alert can be saved.</td></tr><tr><td><em>(Dropdown)</em> <br>Items</td><td>The items that are available for selection in the dropdown. <br><strong>Text</strong> is shown in the dropdown, and <strong>Value</strong> is what will be selected and saved. </td></tr><tr><td><p><em>(Button)</em></p><p>Button Style</p></td><td><p>The style of the button in the Recommendation Alert:</p><p><strong>Text:</strong> The button has no borders. The text color depends on the Button Type.</p><p><strong>Outlined:</strong> The button has a colored outline. The border color depends on the Button Type.</p><p><strong>Contained:</strong> The button has a colored background. The color depends on the Button Type. If the Button Type is Normal, it has a black outline. </p></td></tr><tr><td><em>(Button)</em><br>Button Type</td><td><p>The color of the button in the Recommendation Alert:</p><p><strong>Danger:</strong> Red.</p><p><strong>Default:</strong> Blue.</p><p><strong>Normal:</strong> White or Black.</p><p><strong>Success:</strong> Green.</p></td></tr></tbody></table>

> [!NOTE]
> Number Selector automatically converts the entered value into a scientific notation if it is greater than 21 digits for an integer value and greater than 6 digits for a decimal value.

## Further Reading

* [How to Create and Manage Forms](../../how-tos/recommendations/manage-forms.md)
* [Action Requests: creating work orders in Data Streams with a Form button](action-requests.md)
