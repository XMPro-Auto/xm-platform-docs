# Tree List

The Tree List UI component is a tree-like representation of textual data. This component is useful when we want to display something that has a hierarchy.

![Tree List](../../images/blocks-toolbox/image-1413.png)

## Tree List Properties

### Appearance

#### Common Properties

Properties that are common to most Blocks include _visible_ and _tooltip_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Search Enabled

A search bar will be shown on top of the list and the user can search the data.

![Search Enabled](../../images/blocks-toolbox/image-718.png)

### Value

#### Common Properties

The _value_ property is common to most Blocks;

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

When an Id is entered into the value field, it detects it automatically.

![Value](../../images/blocks-toolbox/image-381.png)

### Data Source

#### Common Properties

Properties that are common to most Blocks include: _filter, sort, show # of results,_ and _skip # of results;_

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for the Tree List.

### Data

#### Display

The Display property is required for the Tree List.

**Id**

The Id property is required for the Tree List.

#### Parent Id

Properties include the _Parent Id_ so the component knows how the fields are connected to each other. The Parent Id refers to the Id of the parent record. For example, in the hierarchy of employees, multiple people could report to one manager, so their parent Ids would be the Id of the person they are listed underneath. If the parent Id of a record is set to null or 0, it will automatically be placed as a root or main parent element on the tree.

[See the Common Properties article for more details on common data properties.](../common-properties.md)

The Parent Id property is required for the Tree List.

### Action

#### Common Properties

Properties that are common to most Blocks include: _Navigate To and Show Confirmation Dialog;_

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
