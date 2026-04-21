# Toolbar

The Toolbar is a UI component that can contain items that are used to manage screen content. Those items can be plain text or other blocks such as images and are useful for showing options to the user in a more visual form than a regular menu.

![Toolbar](../../images/image-854.png)

## Toolbar Properties

### Appearance

#### Common Properties

Toolbars have properties that are common to most Blocks: _visibility_ and _tooltip_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

## Toolbar Item Properties

### Adding Toolbar Items

The Toolbar Block has 3 areas, _before_, _center,_ and _after_. Adding new items can be done in two ways. The first one is to add it by clicking the _plus_ sign when you have either the toolbar or toolbar item selected. This will create a new item with default settings.

> [!NOTE]
> [See the Canvas article for more details on these controls.](../../concepts/application/canvas.md#block-toolbar)

![Adding toolbar items](../../images/adding-toolbar-items-1.gif)

If you have the toolbar selected and add a new item it will be added to the _before_ section which is the first one from the left. If you have the toolbar item selected and click the _plus_ sign, the new item will be added to the same section as the selected item.

Items can be moved by dragging and dropping them to the desired section.

![Moving toolbar items](../../images/moving-toolbar-items.gif)

You can also add items by clicking the _copy_ button when one of the items is selected. This will create a new item with the exact same settings as the selected item.

![Copying toolbar items](../../images/copying-toolbar-items-1.gif)

### Appearance

#### Common Properties

You can change the _visibility, styling, add a tooltip_ and _change the icon_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

#### Text

Tooltip items can have text next to the icon.

![Toolbar item text](../../images/image-1309.png)

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Locate in overflow menu

Auto - It will try to fit items as long as they are fully visible.\
Always - It will hide the item even if there is enough space to show it.\
Never - It will show the items at all times. Some items may overlap.\

![Locate in overflow menu options](../../images/image-1669.png)

### Validation

#### Common Properties

The _groups to validate_ property is common to most Blocks;

[See the Common Properties article for more details on common validation properties.](../common-properties.md#validation)

### Action

#### Common Properties

The toolbar has properties that are common to most Blocks: _navigate to_ and _show confirmation dialog_;

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
