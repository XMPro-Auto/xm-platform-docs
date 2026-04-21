# Block Properties

Block Properties are properties that define the appearance and behavior of the Block. This allows you to customize the block's content such as the heading text, or configure any data you would like to display on your application.

Each block type has different properties. To access the Block Properties tab, double-click a Block in the canvas or click on a Block in the canvas and click the Block Properties command.

![](../../images/image-1285.png)

Properties are split into several common categories. Click on a category to expand the accordion and see the Properties in that category.

The common categories are as follows:

<table><thead><tr><th width="211">Category</th><th>Description</th></tr></thead><tbody><tr><td>Appearance</td><td>Properties that define how a Block looks.</td></tr><tr><td>Behavior</td><td>Properties that define how a Block behaves.</td></tr><tr><td>Value</td><td>Properties that define what value a Block has.</td></tr><tr><td>Data Source</td><td>Properties that define what Data Source the Block has (applies to Blocks that allow a Data Source to be attached).</td></tr><tr><td>Data,<br>Columns,<br>Items</td><td>Properties that define what the Data Source properties are mapped to, or allow a static data set to be created (applies when relevant to the Block).</td></tr><tr><td>Grouping</td><td>Properties that define how the Data Source is grouped (applies when relevant to the Block).</td></tr><tr><td>Action</td><td>Properties that define what action, and validation to perform, and what Data Source to update when it or items inside the Block are clicked (applies to Blocks that allow an action).</td></tr><tr><td>Validation</td><td>Properties that define what validation should be performed on the value of the Block before allowing an action (applies to Blocks that allow user input).</td></tr></tbody></table>

## Dynamic and Expression Properties

Some properties have the option of being a Dynamic or Expression property. If the property has a button on the left with an A icon and "Static Value" when you hover it, it can be a Dynamic or Expression Property. Press the button to cycle through the modes.

<div align="center"><img src="../../images/image-1716.png" alt="Static Mode"></div>

<br>

<div align="center"><img src="../../images/image-844.png" alt="Dynamic Mode"></div>

<br>

<div align="center"><img src="../../images/image-1684.png" alt="Expression Mode"></div>

Dynamic properties allow you to select a value for the property from the Page Parameters, Variables, User Details, Device Details, and from a column or expression of the current row of a parent Block's Data Source.

### User Details

<table><thead><tr><th width="236">Property</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>Username</td><td>Returns the Username of the user that is signed in.</td><td></td></tr><tr><td>First Name</td><td>Returns the First Name of the user that is signed in.</td><td></td></tr><tr><td>Last Name</td><td>Returns the Last Name of the user that is signed in.</td><td></td></tr><tr><td>Full Name</td><td>Returns the Full Name of the user that is signed in, using the format "[First Name] [Last Name]".</td><td></td></tr><tr><td>Email</td><td>Returns the Email of the user that is signed in.</td><td></td></tr><tr><td> Preferred Language</td><td><p>Returns the regional language tag of the logged in user's preferred language. Use this to adjust text when an App will be used in multiple languages: <code>Iif(userPreferredLanguage == "en-US", "Hello world", "Oi Worldo")</code></p><table><thead><tr><th>Language</th><th>Tag</th></tr></thead><tbody><tr><td>English (United States)</td><td>en-US</td></tr><tr><td>svenska</td><td>sv-SE</td></tr><tr><td>Português (Brasil)</td><td>pt-BR</td></tr><tr><td>Русский</td><td>ru-RU</td></tr><tr><td>Español</td><td>es-ES</td></tr><tr><td>Nederlands</td><td>nl-NL</td></tr><tr><td>Deutsch</td><td>de-DE</td></tr><tr><td>français</td><td>fr-FR</td></tr><tr><td>中文 (Zhōngwén)</td><td>zh-CN</td></tr><tr><td>ελληνικά</td><td>el-GR</td></tr><tr><td>Türkçe</td><td>tr-TR</td></tr><tr><td>čeština</td><td>cs-CZ</td></tr><tr><td>suomi</td><td>fi-FI</td></tr><tr><td>Italiano</td><td>it-IT</td></tr><tr><td>Magyar</td><td>hu-HU</td></tr><tr><td>日本語 (にほんご)</td><td>ja-JP</td></tr><tr><td>slovenski jezik</td><td>sl-SI</td></tr><tr><td>Tiếng Việt</td><td>vi-VN</td></tr></tbody></table></td><td></td></tr></tbody></table>

### Device Details

<table><thead><tr><th width="238">Property</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>IsMobile</td><td><p>Returns True boolean value if the App is open on a mobile device. </p><p>Example: For Mobiles and/or Tablets will be True.</p></td><td></td></tr><tr><td>IsDesktop</td><td><p>Returns True boolean value if the App is open on a desktop device. </p><p>Example: For Laptops and/or Desktops will be True.</p></td><td></td></tr><tr><td>Culture</td><td><p>Returns the Device culture/language. </p><p>Example: If the language is set to US English will return en-US.</p></td><td></td></tr></tbody></table>

> [!NOTE]
> [See the Data Integration article for more information on Data Sources](data-integration.md#data-source).

Expression properties allow you to create short scripts to create a custom value from all the above options. [See the Variable and Expressions article to learn more about Expressions](variables-and-expressions.md).

![](../../images/image-1008.png)

The Dynamic and Expression properties will have all the Block's ancestor's Data Sources displayed in the order of closest ancestor to furthest. For example, in the following images, the bottom-most Text Block in the Page Layers has two ancestors that have a Data Source: the Data Repeater Box and the Templated List. Therefore the two data sources are listed in the Text Block's Dynamic and Expression property dropdowns.

![](../../images/image-750.png)

![](../../images/image-1709.png)

## Further Reading

* [How to Use Dynamic Properties](../../how-tos/apps/use-dynamic-properties.md)
* [How to Use Expression Properties](../../how-tos/apps/use-expression-properties.md)
* [How to Use Validation](../../how-tos/apps/use-validation.md)
