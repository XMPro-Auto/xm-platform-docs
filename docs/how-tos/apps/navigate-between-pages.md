# Navigate Between Pages

It is possible to allow navigation between Pages of an App by configuring the Action of a Block. This allows you to separate your content within the application into sections that can be easily navigated by the user.

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of Navigating between Pages.
>
> * [Navigation and Parameters](../../concepts/application/navigation-and-parameters.md)
> * [How to Manage Pages](manage-pages.md)

## Configuring Navigation between Pages

To add Navigation between Pages, make sure the Application has more than one Page. [See the Manage Pages article to read more about adding Pages.](manage-pages.md)

![Screenshot showing the application editor with multiple pages listed in the left sidebar under the Pages section. Each page is represented as a card with its name.](../../images/apps/navigation/nav-1.png)

When a new Page is created, they are automatically configured to have links going back to the landing page, which can be seen at the top of the screen.

![Screenshot showing the automatic navigation link back to the landing page, appearing as a breadcrumb navigation at the top of the screen.](../../images/apps/navigation/nav-2.png)

Some Pages do not automatically have links to other Pages. For example, the Landing page does not have links going to other pages. To add Navigation between Pages, follow these steps:

1. Click on _Applications_ from the left-hand menu.
2. Click on the _edit_ button of the Application from the list.

![Screenshot of the Applications list view showing multiple application cards with an Edit button highlighted on one of them.](../../images/apps/parameters/params-1.png)

3\. Select a Page from the Application's Edit menu.  
4\. Click on _Blocks_.  
5\. Under '_Actions_', select an action such as a button.  
6\. Drag and drop it onto the Page of the application.

![Screenshot showing the Blocks toolbox with the Actions section expanded. A button component is being dragged from the toolbox onto the page canvas.](../../images/apps/navigation/nav-4.png)

7\. Select the button.  
8\. Click on _Block Properties._  
9\. Under '_Action_,' click on the _Navigate To_ Dropdown and select _Page_.

![Screenshot of the Block Properties panel with the Action section open. The Navigate To dropdown is set to "Page" in the properties.](../../images/apps/navigation/nav-5.png)

10\. Select the page you want to navigate to.

![Screenshot showing the dropdown list of available pages that can be selected as the navigation target for the button.](../../images/apps/navigation/nav-6.png)

11\. Under '_Appearance,_' give the button a name.  
12\. Click on _Save_.

![Screenshot of the Block Properties panel with the Appearance section open. The Name field is filled with "Go to Page 2" and the Save button is highlighted at the bottom.](../../images/apps/navigation/nav-7.png)

## Navigating between Pages at Runtime

After the Navigation between Pages has been added, you can Launch the App to see what it will look like at runtime. Follow the steps below to Launch and view the App:

1. Click on _Launch_.
2. The button is visible on the Page. Click on the button to navigate to the other selected Page.

![Screenshot showing the app in preview mode with the navigation button visible on the page.](../../images/apps/navigation/nav-8.png)

![Screenshot showing the cursor hovering over the navigation button, indicating it's about to be clicked.](../../images/apps/navigation/nav-9.png)

3\. The page will open.

![Screenshot showing the destination page after the navigation button has been clicked. This shows the result of successful navigation between pages.](../../images/apps/navigation/nav-10.png)

## Deleting Navigation between Pages

You can delete the navigation functionality by either deleting the Block itself or by deleting the settings under _Action_ in the _Block Properties_ tab.

![Screenshot of the Block Properties panel showing how to remove navigation by clearing the Action settings. The Navigate To dropdown is being set to "None".](../../images/apps/navigation/nav-11.png)

## Navigating Using Back URL

You can include a back URL to the current page when configuring a Navigate To URL, so that the user can return to the original page. For example, you want to open an Alert from a custom templated list and the alert drill-down needs a back URL.

To append a back URL, follow these steps:

1. Click on _Block Properties_.
2. Under '_Action_', click on the _Navigate To_ Dropdown and select _URL_.
3. Toggle the URL mode to Expression Mode.
4. Click the dropdown to edit the expression value.

![Screenshot showing the Block Properties panel with URL configuration. The URL field is in Expression Mode and the expression editor dropdown is open.](../../images/apps/navigation/backurl-1-4.png)

5\. Note the current page parameters under Constants.

![Screenshot of the expression editor showing the Constants section with current page parameters like appId, pageId, and categoryName that can be used in the back URL.](../../images/apps/navigation/backurl-5.png)

6\. Configure the URL with back parameters, similar to the below:

```
"https://xmad-sample.azurewebsites.net/viewalert;id="+"12345"+";backUrl=render;backParams=\{\\"appId\\":\\""+appId+"\\",\\"pageId\\":\\""+pageId+"\\",\\"categoryName\\":\\""+categoryName+"\\",\\"appVersion\\":\\""+appVersion+"\\"\\}"
```

![Screenshot showing the completed expression for the back URL with all parameters properly formatted in the expression editor.](../../images/apps/navigation/backurl-6.png)

## Copying App Link

You can copy the App link if you want to share it. This creates a link to the published app version - or to the latest version if there is no published version.

1. Click More.
2. Click Copy App Link.

![Screenshot showing the More dropdown menu in the application editor with the "Copy App Link" option highlighted.](../../images/apps/navigation/app-link.png)

## Copying Page Link

You can copy a specific App Page link if you want to share it. This will create a link to the specific app version and page.

1. Open the Page.
2. Click Copy Page Link.

![Screenshot showing the Page editor with the "Copy Page Link" button highlighted in the toolbar.](../../images/apps/navigation/page-link.png)

## Further Reading

* [How to Pass Parameters between Pages](pass-parameters-between-pages.md)
