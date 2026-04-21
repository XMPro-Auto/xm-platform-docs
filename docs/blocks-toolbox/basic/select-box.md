# Select Box

The Select Box component is an editor that allows a user to select an item from a drop-down list. This is useful when there are many options or items to select from and it may be hard for the user to find one particular item. This UI control allows the user to navigate to the item faster.

## Select Box Properties

### Appearance

#### Common Properties

A Select Box has the option to change its _visibility, styling mode, placeholder, tooltip_ and _show clear button_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

#### Styling Mode

![Styling Mode](../../images/blocks-toolbox/image-1731.png)

#### Placeholder and Show Clear Button

The placeholder is the text that will be displayed before a value is selected. The show clear button will add a button to clear the selected item.

![Placeholder and Clear Button](../../images/blocks-toolbox/image-1012.png)

### Behavior

#### Common Properties

The select box has the option to be _disabled_ and _read-only_.

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Enable Search

The user can search the items in the select box.

![Enable Search](../../images/blocks-toolbox/image-514.png)

#### Store User Selection

When enabled, your selection at runtime is saved in your browser's local data, so that it is remembered when the page reloads. This includes re-opening the App and returning from a drill-down.

### Value

#### Common Properties

This option is used to select the default value and must match a value from the Data Source.

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

![Value](../../images/image-333.png)

### Data Source

#### Common Properties

‌The Data source can be Static or Dynamic. Static values have to be entered manually while Dynamic will get the value from the provided Data Source.

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for the Select Box.

#### Static Items

If a Dynamic Data Source is not used, you can enter key dates to display manually under the Data section.

#### Dynamic Data Source

This option allows you to connect the control to a specific Data Source such as a database to pull data dynamically. This will give you additional options to sort, filter, show, or skip certain records.

### Data

This is only available if the Data Source is Dynamic. Here we have the option to set the values of the buttons as well as what text will be displayed. ‌

[See the Common Properties article for more details on common data properties.](../common-properties.md)

#### Display Expression

The expression is a user-friendly name for what the user can see. For example, the text that is displayed to the user.

The Display Expression property is required for the Select Box.

#### Value Expression

This is the actual value stored in the background of the application in the code. For example, instead of true or false, it would be 0 or 1.

The Value Expression property is required for the Select Box.

### Grouping

This is only available if the Data Source is Dynamic. Here we have the option to set how the items in the select box will be grouped.

If Grouping is enabled, the Group By Expressions property is required for the Select Box.

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate To and Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
