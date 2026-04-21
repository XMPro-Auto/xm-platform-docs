# Tags

Tags can be labels used to group certain contents or topics of the website together. A TagBox is a field that allows the user to select multiple Tags (such as items or categories) from a drop-down menu.

## Tags Properties

### Appearance

#### Common Properties

Tags have the option to change their _visibility, show tooltips, set placeholder,_ and change the _styling_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

Options that are specific to Tags are _Multiline, Show Clear Button, Show Dropdown Button, Show Selection Controls._

#### Styling Mode

![Styling Mode](../../images/blocks-toolbox/image-551.png)

#### Placeholder

Tags, unlike some other controls, have default placeholder text. The default value is "Select".

![Placeholder](../../images/blocks-toolbox/image-1137.png)

#### Show Clear Button

The clear button will appear on the right side. Clicking the button will remove all the Tags from the control.

![Show Clear Button](../../images/blocks-toolbox/image-1396.png)

#### Show Dropdown Button

![Show Dropdown Button](../../images/blocks-toolbox/image-299.png)

#### Show Selection Controls

![Show Selection Controls](../../images/blocks-toolbox/image-624.png)

#### Multiline

![Multiline](../../images/blocks-toolbox/image-789.png)

### Behavior

#### Common Properties

Tags have the option to be _disabled_ and _read-only_.

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

Options that are specific to Tags are _Enable Search_ and _Apply Value Mode_.

#### Readonly

![Readonly](../../images/blocks-toolbox/image-1857.png)

#### Disabled

![Disabled](../../images/blocks-toolbox/image-932.png)

#### Enable Search

Will allow the user to type in box and results will be updated.

![Enable Search](../../images/blocks-toolbox/image-992.png)

#### Apply Value Mode

The default option is Use Button which will show the OK and Cancel buttons. Instantly it will add the tag when it's selected.

![Apply Value Mode](../../images/blocks-toolbox/image-667.png)

### Value

#### Common Properties

The _value_ property is common to most Blocks;

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

The value should be an array of strings. For example, if we put the following in the Value field _**\["Sydney", "New York", "London"]**_ the results will be the following.

![Value Example](../../images/blocks-toolbox/image-741.png)

### Data Source

#### Common Properties

‌A Data Source allows Dynamic Source only. The Dynamic Source will get the value from the provided Data Source.

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for Tags.

### Data

#### Display Expression

The expression is a user-friendly name for what the user can see. For example, the text that is showing in one of the rows of the dropdown.

The Display Expression property is required for Tags.

#### Value Expression

This is the actual value stored in the background of the application in the code. For example, instead of true or false, it would be 0 or 1.

The Value Expression property is required for Tags.

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate To and Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
