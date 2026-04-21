# Pivot Grid

This Block allows you to display data in the format of a Pivot Grid. The Pivot Grid can display the data in a customizable way and allows the users to specify which rows and columns are compared against each other. It consists of the grid itself as well as a field chooser which allows you to change the way the data is represented.

![Pivot Grid with field chooser displaying customizable data in rows and columns](../../images/image-1609.png)

## Pivot Grid Properties

### Appearance

#### Common Properties

Options for the appearance include its _visibility_.

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

Options that are specific to Pivot Grids include the options to _show borders, show column totals, show column grand totals, show row totals, show row grand totals, show drill down,_ and _show totals prior_.

[For details on common grid properties, see the Data Grid article](../basic/data-grid.md#common-properties).

#### Show Column Totals

This specifies if the totals across each row are counted and displayed on the side of a grouped column.

![Pivot Grid with column totals disabled](../../images/image-976.png)

![Pivot Grid with column totals enabled showing totals for grouped columns](../../images/image-674.png)

#### Show Column Grand Totals

This specifies if the totals across each row are counted and displayed on the side.

![Pivot Grid with column grand totals disabled](../../images/image-1256.png)

![Pivot Grid with column grand totals enabled showing totals on the side](../../images/image-7.png)

#### Show Row Totals

This specifies if the totals across each column are counted and displayed after each grouped row.

![Pivot Grid with row totals disabled](../../images/image-237.png)

![Pivot Grid with row totals enabled showing totals after each grouped row](../../images/image-214.png)

#### Show Row Grand Totals

This specifies if the totals for each column are counted and displayed at the bottom.

![Pivot Grid with row grand totals disabled](../../images/image-1710.png)

![Pivot Grid with row grand totals enabled showing column totals at the bottom](../../images/image-465.png)

#### Show Drilldown

When this is enabled, selecting any of the values in the data region will open a grid that drills down for each record.

![Drilldown grid showing detailed records when a value is selected](../../images/image-1275.png)

#### Show Totals Prior

By default, the totals for columns and rows are displayed at the end of the grouped row or column. If this option is enabled, the totals for columns or rows will be displayed before them, instead of after.

![Pivot Grid with totals displayed after grouped rows and columns (default)](../../images/image-11.png)

![Pivot Grid with totals displayed before grouped rows and columns](../../images/image-387.png)

### Behavior

Options for the behavior include _sorting the data by summary, allowing sorting, allowing filtering_, and _retaining the layout_.

#### Allow sorting by summary

This allows the user to sort by each individual column. To sort, right-click on a column and select _Sort by this Column._

![Right-click context menu showing 'Sort by this Column' option](../../images/image-1685.png)

#### Allow Sorting

This displays an arrow next to the row or column name. This lets the user sort the order of the columns and rows based on their names.

![Animation showing sorting functionality with arrows next to row/column names](../../images/gjdm3nfbxy.gif)

![Pivot Grid displaying sort arrows next to column headers](../../images/image-948.png)

#### Allow Filtering

This displays a filter icon next to the row or column name. This allows the user to filter the rows or columns to only display certain values.

![Pivot Grid with filter icons next to row and column names](../../images/image-783.png)

![Filter dialog showing available filter options for rows/columns](../../images/image-791.png)

#### Retain Layout

If set to true, this will save the column, row, and data layout configuration in the browser. If changes are made to the Pivot Grid, and the user leaves the page and comes back later, the layout of the table will be the same as before they left it. If this option is set to false, the layout will reset to the default fields specified under _Fields_.

### Data Source

#### Common Properties

Data Sources can be connected to a Pivot Grid. This will allow you to display data on the Pivot Grid.

[See the Common Properties article for more details on common Data Source properties.](../common-properties.md#data-source)

The Data Source property is required for the Pivot Grid.

### Fields

The fields specify the default fields that are visible for the rows and columns on the Pivot Grid. The fields can be bound to a row or column from the Data Source and certain properties can be configured.

#### Area

This specifies where on the Pivot Grid the data will be shown. This includes whether it is shown on the row, column, data area, or filter area.

#### Data Type

The data type of the row, column, or cell. This can be a number, string of characters, true or false value, or a date.

#### Data Field

This is the field from the Data Source that is going to be used when displaying the data.

![Fields configuration panel showing area, data type, and data field settings](../../images/image-390.png)
