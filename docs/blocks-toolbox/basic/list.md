# List

A List is a UI component that displays a collection of items in the form of a list. The List is scrollable if there are too many items to fit in its container, or it can also be separated into pages. A List can be connected to a Data Source to retrieve and display specific values. Lists can be useful if you want to display a list of items to the user.

> [!TIP]
> It is recommended that you read the article listed below to improve your understanding of Data Sources.
>
> * [How to Create and Manage Data Sources](../../how-tos/apps/manage-data-sources.md)

## List Properties

### Appearance

#### Common Properties

Properties that are common to most Blocks include _visible and tooltip;_

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

#### Enable Paging

The default option is to show all the results. The user can specify how many items should be displayed per page and pages will be displayed under the List.

![Enable Paging](../../images/blocks-toolbox/image-1038.png)

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Search Enabled

It will add a search bar where the user can search the items in the List.

### Value

#### Common Properties

This option is used to select the default value and must match a value from the Data Source.

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

### Data Source

‌Data sources can be Static or Dynamic. Static values have to be entered manually while Dynamic will get the value from the provided Data Source.

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for the List.

#### Static Items

If a Dynamic Data Source is not used, you can enter key dates to display manually under the Data section.

#### Dynamic Data Source

This option allows you to connect the control to a specific Data Source such as a database to pull data dynamically. This will give you additional options to sort, filter, show, or skip certain records.

### Data

#### Display Expression

The expression is a user-friendly name for what the user can see. For example, the text that is showing in the List.

The Display Expression property is required for the List.

### Grouping

This is only available if the Data Source is Dynamic. Here we have the option to set how the items in the list will be grouped.

If Grouping is enabled, the Group By Expression property is required for the List.

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate to_ and _Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
