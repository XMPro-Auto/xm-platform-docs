# Range Slider

A Range Slider is an input field that can be used to select a numeric value within a given range. This is useful when there is a limited number of options the user should select from and eases the validation for the user's input.

## Range Slider Properties

### Appearance

#### Common Properties

The Range Slider has the option to change its _visibility_ and to show _tooltips_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

Options that are specific to Range Sliders include the ability to change the _mode, range,_ or _labels_. The appearance of the labels such as the positioning and format of the labels can also be configured.

#### Mode

In point mode, only the single point that the user selected will be visible. When in range mode, the Range Slider allows you to specify whether or not to show the range line between the two selected values.

![Mode](../../images/blocks-toolbox/image-170.png)

#### Show Range

When the show range option is set to true, the range that is selected will be highlighted.

![Show Range](../../images/blocks-toolbox/image-272.png)

#### Show Labels

Show labels will add a value on both sides of the slider so the user will know the numeric range.

![Show Labels](../../images/blocks-toolbox/image-1808.png)

#### Label Position

This gives you the option to add the labels either above the slider or underneath the slider.

![Label Position](../../images/blocks-toolbox/image-1841.png)

#### Label Format

The label format option allows you to choose what type of numeric range the slider is. Some of the options that are available include but are not limited to currency, decimal, fixed point, seconds, minutes, days, or hours.

![Label Format](../../images/blocks-toolbox/image-1173.png)

### Behavior

#### Common Properties

Properties that are common to most Blocks include: _read-only_ and _disabled_.

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Min and Max

This affects the minimum and maximum values for where the range starts.

![Min and Max](../../images/blocks-toolbox/image-865.png)

#### Step

This affects the intervals that are allowed between the values that can be chosen. For example, if the step interval is set to 50, and the user selects 45, the slider value will automatically be set to 50.

![Step](../../images/blocks-toolbox/gwemoVRcpa.gif)

### Value

If the _point_ option is selected as the _mode_, there will only be one value. However, if the _range_ option is selected as the mode, you can choose a _start value_ or an _end value_.

#### Point Value

This determines what the selected value is when the mode is set to the _point_ option.

#### Range Start and End value

This determines the range that is selected from the start value to the end value. This is available when the _range_ option is selected for the mode.

![Range Start and End Value](../../images/blocks-toolbox/image-855.png)

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate To and Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
