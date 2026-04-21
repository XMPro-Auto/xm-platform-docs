# Use Flex

Flex styles are a way of changing the layout of the page so it is responsive. When using Flex, the layout and position of the Blocks will respond to fit the screen, which is important in ensuring that users have a good user experience regardless of the screen size they are viewing your Application on.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Devices and the Style Manager.
>
> * [Device](../../concepts/application/devices.md)
> * [Style Manager](../../concepts/application/block-styling.md)
> * [How to Use Style Manager and Devices](use-block-styling-and-devices.md)

## Enabling Flex Styles

To enable Flex styles, follow the steps below:

1. Select the parent Block of the Blocks you want to configure the position for.
2. Click on _Block Styling_.
3. Choose _Flex_ for the display or _enable_ the flex container.

![Screenshot of the Block Styling panel showing the Display dropdown set to "Flex". The Flex Container checkbox is checked, activating additional flex properties below it including Direction, Justify, and Align items options.](../../images/apps/flex/flex-1.png)

## Flex Container

### Direction

The direction determines which direction the content will go. It can either be:

1. Row - Left to right
2. Reverse row - right to left
3. Column – Top to Bottom
4. Reverse column – Bottom to Top

![Screenshot showing a flex container with Direction set to "Row". Three colored blocks are arranged horizontally from left to right in a single row within the container.](../../images/apps/flex/flex-2.png)

![Screenshot showing a flex container with Direction set to "Row Reverse". Three colored blocks are arranged horizontally from right to left (reversed) in a single row within the container.](../../images/apps/flex/flex-3.png)

![Screenshot showing a flex container with Direction set to "Column". Three colored blocks are stacked vertically from top to bottom in a single column within the container.](../../images/apps/flex/flex-4.png)

![Screenshot showing a flex container with Direction set to "Column Reverse". Three colored blocks are stacked vertically from bottom to top (reversed) in a single column within the container.](../../images/apps/flex/flex-5.png)

### Justify

Justify determines the way the contents are laid out. It can either be:

1. Start
2. End
3. Space Between (puts spaces between the Blocks)
4. Space Around (puts an equal amount of space around each Block)
5. Center

![Screenshot showing a flex container with Justify set to "Start". Multiple blocks are aligned at the beginning of the container with no space between them and the starting edge.](../../images/apps/flex/flex-6.png)

![Screenshot showing a flex container with Justify set to "End". Multiple blocks are aligned at the end of the container with no space between them and the ending edge.](../../images/apps/flex/flex-7.png)

![Screenshot showing a flex container with Justify set to "Space Between". Blocks are distributed evenly across the container with the first block at the start and the last block at the end, with equal spacing between blocks.](../../images/apps/flex/flex-8.png)

![Screenshot showing a flex container with Justify set to "Space Around". Blocks are distributed with equal space around each block, including half-spaces at the beginning and end of the container.](../../images/apps/flex/flex-9.png)

![Screenshot showing a flex container with Justify set to "Center". Multiple blocks are centered in the container with equal space on both left and right sides of the group.](../../images/apps/flex/flex-10.png)

### Align-Items

Determines the vertical alignment of the Blocks. It can either be:

1. Start
2. End
3. Stretch
4. Center

![Screenshot showing a flex container with Align-Items set to "Start". Blocks of different heights are aligned at the top of the container, regardless of their individual heights.](../../images/apps/flex/flex-11.png)

![Screenshot showing a flex container with Align-Items set to "End". Blocks of different heights are aligned at the bottom of the container, regardless of their individual heights.](../../images/apps/flex/flex-12.png)

![Screenshot showing a flex container with Align-Items set to "Stretch". All blocks are stretched vertically to fill the entire height of the container regardless of their content.](../../images/apps/flex/flex-13.png)

![Screenshot showing a flex container with Align-Items set to "Center". Blocks of different heights are centered vertically in the container, with equal space above and below each block.](../../images/apps/flex/flex-14.png)

## Blocks inside the Flex Container

### Grow

Grow will grow the item to fit the container.

![Screenshot showing the Block Styling panel with the Flex Grow property set to 1 for a selected block. The block expands to fill available space in the flex container.](../../images/apps/flex/flex-15.png)

If multiple Blocks have a grow value greater than 0, they will take up a ratio of the available space.

![Screenshot showing multiple blocks with different Flex Grow values. The blocks with higher grow values take proportionally more space than those with lower values, demonstrating the ratio-based distribution.](../../images/apps/flex/flex-16.png)

### Shrink

Shrink determines whether an item is allowed to shrink if the screen is too small or if other Blocks take up too much space. Shrink will not work if the Block has a minimum width or height.

![Screenshot showing the Block Styling panel with the Flex Shrink property set to 1 for a selected block. The block is allowed to shrink when there's not enough space in the container.](../../images/apps/flex/flex-17.png)

### Basis

This determines the default size of the object along its direction axis.

![Screenshot showing the Block Styling panel with the Flex Basis property being configured. The property is set to a specific pixel value, establishing the initial main size of the flex item.](../../images/apps/flex/flex-18.png)

### Order

The order will change the order of the Blocks. Blocks with no order will be displayed first, followed by the ordered Blocks going in ascending order.

![Screenshot showing the Block Styling panel with the Order property set to a specific number. Blocks are visibly arranged in a different order than their DOM sequence due to the order property.](../../images/apps/flex/flex-19.png)

### Align-Item

Aligns the individual Blocks. They can either be:

1. Start
2. End
3. Stretch
4. Center

![Screenshot showing a flex container where a single highlighted block has Align-Self set to "Start". This block is aligned to the top of the container while other blocks follow the container's alignment rules.](../../images/apps/flex/flex-20.png)

![Screenshot showing a flex container where a single highlighted block has Align-Self set to "End". This block is aligned to the bottom of the container while other blocks follow the container's alignment rules.](../../images/apps/flex/flex-21.png)

![Screenshot showing a flex container where a single highlighted block has Align-Self set to "Stretch". This block is stretched to fill the container's height while other blocks maintain their original dimensions.](../../images/apps/flex/flex-22.png)

![Screenshot showing a flex container where a single highlighted block has Align-Self set to "Center". This block is vertically centered in the container while other blocks follow the container's alignment rules.](../../images/apps/flex/flex-23.png)

## Further Reading

* [How to Design Pages for Mobile](design-pages-for-mobile.md)
