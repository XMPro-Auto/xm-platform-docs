# Radio Buttons

The RadioGroup is a UI component that contains a list of options for users to choose from. This is useful if you only want the user to select a single item out of the options in the list.

## Radio Buttons Properties

### Appearance

#### Common Properties

The Radio Button has the option to change its _visibility_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

An option that is specific to Radio Button includes the ability to change its orientation.

#### Orientation

The default value is Vertical which means Radio Buttons will be displayed top to bottom. By changing to Horizontal, the Radio Buttons will be displayed left to right.

![Orientation](../../images/blocks-toolbox/image-1098.png)

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

‌[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Disable

This affects the Radio Buttons group to be shown as read-only.

![Disable](../../images/blocks-toolbox/image-965.png)

### Value

#### Common Properties

This option is used to select the default value and must match a value from the Data Source.

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

### Data Source

#### Common Properties

‌A Data Source can be Static or Dynamic. Static values have to be entered manually while Dynamic will get the value from the provided Data Source.

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for Radio Buttons.

#### Static Items

If a dynamic Data Source is not used, you can enter key dates to display manually under the Data section.

#### Dynamic Data Source

This option allows you to connect the control to a specific Data Source such as a database to pull data dynamically. This will give you additional options to sort, filter, show, or skip certain records.

### Data

#### Display Expression

The expression is a user-friendly name for what the user can see. For example, the text that is displayed to the user.

The Display Expression property is required for Radio Buttons.

#### Value Expression

This is the actual value stored in the background of the application in the code. For example, instead of true or false, it would be 0 or 1.

The Value Expression property is required for Radio Buttons.

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate To and Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
