# Navigate Between Apps

It is possible to allow navigation between Apps by configuring the Action of a Block on the launching App to navigate to the destination App's URL and set it's landing page's Parameter. This allows you to separate your content into different applications that can still be easily navigated by the user.

**Important Considerations:**

* The parameter name in both Apps must match exactly
* The destination App must be published and accessible to users of the launching App.

> [!NOTE]
> We're going to achieve this by combining concepts from the following articles:
>
> * [How to Navigate Between Pages](navigate-between-pages.md)
> * [How to Pass Parameters Between Pages](pass-parameters-between-pages.md)

## Configure the destination App

Add a Parameter and a textbox to display the value when it is passed to the Page during runtime.

See [How to Add a Parameter](pass-parameters-between-pages.md#adding-a-parameter-to-the-page) to the Page for detailed steps.

### Add a Parameter

1. Click Applications from the left-hand menu.
2. Click the edit button of the destination App from the list.
3. Click Page Data on the landing page
4. Click the plus to add a Parameter
5. Add the name and type of the new Parameter
6. Click Create.
7. Click on Save.

### Add a display (Optional)

Add a Textbox to the Page so you can display the parameter value when it is passed from the launching App.

1. Click Block Properties
2. Click the 'A'  button to toggle from static to dynamic text.
3. Select the Parameter from the dropdown.
4. Click Save.

## Configure the launching App

Add a Button to launch the second app and populate the page parameter you just created in the URL using a dynamic expression.

### Add a Button

1. Click Applications from the left-hand menu.
2. Click the edit button of the Application from the list.
3. Select a Page from the Application's Edit menu.
4. Click on Blocks.
5. Under 'Actions', select an action such as a button.
6. Drag and drop it onto the Page of the application.
7. Select the button.
8. Click on Block Properties.
9. Under 'Action,' click on the Navigate To Dropdown and select URL.
10. Click the 'A' button to toggle the URL from static to expression mode.
11. Click the dropdown to edit the expression value.
12. Enter the destination App's URL with parameters (e.g., "<https://your-xmpro-instance.com/render;appId=123?assetId="+{Variable.AssetID}>)
13. Under 'Appearance,' give the button a name.
14. Click Save.

See [How to Copy the App Link](#copy-the-app-link) for details on how to copy the launch App's URL.

### Copy the App Link

You can copy the App link if you want to share it. This creates a link to the published app version - or to the latest version if there is no published version.

1. Click More.
2. Click Copy App Link.

![Screenshot showing the More dropdown menu in the application editor with the "Copy App Link" option highlighted.](../../images/apps/navigation/app-link.png)

## Further Reading

* [How to Pass Parameters between Pages](pass-parameters-between-pages.md)
