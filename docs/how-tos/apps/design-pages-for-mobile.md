# Design Pages for Mobile

When designing Pages, you may want to use responsive web design principles to support different screen sizes with the same App. This is easily accomplished with Block Styling and Devices. The default Page Layouts that you can choose from when creating a page have built-in responsive styling applied to the cards. For an example of this, see the [Responsive Page Layout Example](../../concepts/application/page.md#responsive-page-layout-example).

> [!NOTE]
> It is recommended that you read the article listed below to improve your understanding of how to design pages for mobile.
>
> * [How to Use Block Styling and Devices](use-block-styling-and-devices.md)
> * [How to Manage Pages](manage-pages.md)
> * [How to Use Flex](use-flex.md)

## How to Make Responsive Card Layout

To create a responsive card layout just like the default page layouts, follow the steps below:

1. Create a Page with the first, single-card layout.
2. Clone the Horizontal Stacked Layout, Vertical Stacked Layout, and Card until you have the layout that you desire. Please note that the order in the Page Layers will also be the order, from top to bottom, that items appear in mobile.
3. If you want rows and columns to take up a different ratio on the page, adjust the Flex Grow of the relevant items. Make sure to uncheck [Style Groups](use-block-styling-and-devices.md#adding-a-style-group) when applying styles to a specific element if you do not want the style to apply to the Style Group. [More info on Flex can be found here](use-flex.md).
4. Switch to Mobile view with the middle Devices section of the command buttons.
5. Adjust the heights of the elements. Any styles added in Mobile mode will apply only when the device's screen width is smaller than a threshold. In this case, change the first Horizontal Stacked Layout's Min height to 200%.

<video autoplay loop muted playsinline style="max-width: 100%; height: auto;">
  <source src="../../images/mobile-design-clone.mp4" type="video/mp4">
</video>

<video autoplay loop muted playsinline style="max-width: 100%; height: auto;">
  <source src="../../images/mobile-design-flex-grow.mp4" type="video/mp4">
</video>

![Screenshot of switching to Mobile View in the Devices section](../../images/apps/mobile/mobile-design-switch-view.png)

![Screenshot showing how to adjust element heights in Mobile View](../../images/apps/mobile/mobile-design-adjust-heights.png)
