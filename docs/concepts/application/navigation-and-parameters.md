# Navigation and Parameters

It is possible to allow navigation between Pages of an App by configuring the Action of a Block, and pass data to the Page by configuring the Pass Page Parameters option. You can add Parameters to the Page you are navigating to, and configure what value should be passed to them when the button is clicked. You can choose Dynamic or Static values.

Parameters may be needed if you want to send particular values onto another page as the user clicks on it. For example, if you have a list of machines, and a user selects one, the application may open a new page that displays information for that particular machine. In that case, you may want to pass the ID of the machine the user clicked on to the page that is being opened.

![](../../images/image-1433.png)

![The page will be navigated to with 14 as the value of the Id Parameter ](../../images/image-647.png)

You can add and edit Parameters for the current Page in the Page Data tab.

![](../../images/image-176.png)

Parameters have a Type that restricts what type of data can be sent to the Parameter. The options for Type are Boolean, DateTime, Double, Int, Long, and String.

The following Blocks allow Action:

* [Box Hyperlink](../../blocks-toolbox/actions/box-hyperlink.md)
* [Button](../../blocks-toolbox/actions/button.md)
* [Chart](../../blocks-toolbox/visualizations/chart.md)
* [Esri Map](../../blocks-toolbox/visualizations/esri-map.md)
* [Data Grid](../../blocks-toolbox/basic/data-grid.md)
* [Hyperlink](../../blocks-toolbox/actions/hyperlink.md)
* [Indicator](../../blocks-toolbox/basic/indicator.md)
* [List](../../blocks-toolbox/basic/list.md)
* [Map](../../blocks-toolbox/visualizations/map.md)
* [Templated List](../../blocks-toolbox/layout/templated-list.md)
* [Toolbar](../../blocks-toolbox/layout/toolbar.md)
* [Tree Grid](../../blocks-toolbox/basic/tree-grid.md)
* [Tree List](../../blocks-toolbox/basic/tree-list.md)

## Further Reading

* [How to Navigate between Pages](../../how-tos/apps/navigate-between-pages.md)
* [How to Pass Parameters Between Pages](../../how-tos/apps/pass-parameters-between-pages.md)
