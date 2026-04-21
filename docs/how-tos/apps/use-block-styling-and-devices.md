# Use Block Styling and Devices

Block Styling includes options that allow you to change the text color, background color, borders, typography, dimensions, or other styling options of the Block. You can use it to customize the look and feel of the Application based on themes or color palettes for your specific organization. The style and position of the Blocks can also be customized for different devices, which is important in ensuring that users have a good user experience regardless of the screen size they are viewing your Application on.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Devices and Block Styling.
>
> * [Device](../../concepts/application/devices.md)
> * [Block Styling](../../concepts/application/block-styling.md)
> * [How to Manage Pages](manage-pages.md)

## Adding a Style Group

Style Groups can be created and customized by the user and applied to Blocks on the Canvas. To style a Block, make sure the Block you want to style is selected.

1. Click on the Block Styling tab in the Toolbox.
2. Add a Style Group by typing a name in the field under _'Style Group'_ and pressing enter.
3. Expand any category to change styles.
4. Add your custom style.
5. The style of the group will change as a result.

![Screenshot of the Block Styling panel showing a new style group named "HeaderStyle" being created. The panel displays various style categories including Background, Typography, and Dimensions that can be expanded to customize the style.](../../images/apps/styling/block-styling-1.png)

The created style group can then be applied to other Blocks. Select a different Block and enter the name of the new style Block in the field under _'Style Group'._

![Screenshot showing a different block selected on the canvas. In the Block Styling panel, the previously created "HeaderStyle" is being applied to this block by typing its name in the Style Group field.](../../images/apps/styling/block-styling-2.png)

## Adding Style to States

States include events such as hovering over a Block, clicking a Block, or changing the style for every second Block. To change the styling of a state, select the Block you want to style.

1. Click on the Block Styling tab in the Toolbox.
2. Change the state.
3. Add your custom styling.
4. The styling will be applied to the Block for that state.

![Screenshot showing the Block Styling panel with the State dropdown set to "hover". The Background category is expanded, showing that the background color has been changed to a light green for the hover state of the selected block.](../../images/apps/styling/block-styling-3.png)

In this example, if the user hovers over the Home text, the background will change from light blue to light green. To see the hovering effect in action, no state should be selected. The background color will remain light blue, and will only change to light green when the user hovers over it.

![Screenshot demonstrating the hover effect in action. The mouse cursor is hovering over a navigation item labeled "Home", which has changed its background color from light blue to light green as configured in the hover state styling.](../../images/apps/styling/block-styling-4.png)

## Configure styling between Desktop, Tablet, and Mobile Phones

To configure the styling between devices, follow the steps below:

1. Select Desktop.
2. Create a style group.
3. Change the styling. This styling will be applied to all devices automatically.
4. Change the device to tablet.
5. Change the styling for tablets. Changes will apply to screen sizes smaller than 1366 pixels.
6. Change the device to mobile.
7. Change the styling for phones. Changes will apply to screen sizes smaller than 896 pixels.

![Screenshot showing the device selector set to "Desktop" (1920px width) at the top of the editor. The Block Styling panel shows a style group being configured with desktop-specific styling options.](../../images/apps/styling/devices-1.png)

![Screenshot showing the device selector set to "Tablet" (1366px width) at the top of the editor. The Block Styling panel shows the same style group being adjusted with tablet-specific styling options that override the desktop settings.](../../images/apps/styling/devices-2.png)

![Screenshot showing the device selector set to "Mobile" (896px width) at the top of the editor. The Block Styling panel shows the style group being further customized with mobile-specific styling options that will only apply to small screen sizes.](../../images/apps/styling/devices-3.png)

## Further Reading

* [How to Design Pages for Mobile](design-pages-for-mobile.md)
* [How to Use Flex](use-flex.md)
