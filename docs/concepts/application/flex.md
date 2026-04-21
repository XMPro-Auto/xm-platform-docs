# Flex

Flex (CSS Flexbox Layout Module) is a way to design flexible responsive layouts for web pages.

The main concept behind flex is the flex container. If you set a container to `display: flex;`, its child items' width or height will be expanded or shrunk to best fill the space available.

![display: flex;](../../images/concepts/application/image-248.png)

The direction the flex items will be stacked in is determined by the `flex-direction` property. The options include `row`, `row-reverse`, `column`, and `column-reverse`.

![flex-direction: column;](../../images/concepts/application/image-1713.png)

The alignment of the items in the main-axis (horizontal if `flex-direction` is `row` or `row-reverse`, vertical if `flex-direction` is `column` or `column-reverse`) is determined by the `justify-content` property. The options include `flex-start`, `flex-end`, `space-between`, `space-around`, and `center`.

![justify-content: flex-end;](../../images/concepts/application/image-1301.png)

![justify-content: space-between;](../../images/concepts/application/image-1485.png)

![justify-content: space-around;](../../images/concepts/application/image-1191.png)

![justify-content: center;](../../images/concepts/application/image-1364.png)

The alignment of the items in the cross-axis (vertical if `flex-direction` is `row` or `row-reverse`, horizontal if `flex-direction` is `column` or `column-reverse`) is determined by the `align-items` property. The options include `flex-start`, `flex-end`, `stretch`, and `center`.

![align-items: flex-end;](../../images/concepts/application/image-5.png)

![align-items: center;](../../images/concepts/application/image-1365.png)

![align-items: stretch;](../../images/concepts/application/image-539.png)

The child items of a flex container have a say in how they are altered. The `flex-grow` property on the child of a flex container defines whether the item should be the desired ratio of this item compared to its siblings.

![flex-grow ratios 1:0:0](../../images/concepts/application/image-952.png)

![flex-grow ratios 4:1:1](../../images/concepts/application/image-1565.png)

The `flex-shrink` property defines how much a flex item will shrink relative to the rest of the flex items. Best used in conjunction with the flex-basis property.

The `flex-basis` property specifies the initial length of an item on the main-axis.

![All items have flex-basis: 400px, and the flex-shrink ratios are 1:0:1](../../images/concepts/application/image-308.png)

## Further Reading

* [How to Use Flex in a Page](../../how-tos/apps/use-flex.md)
