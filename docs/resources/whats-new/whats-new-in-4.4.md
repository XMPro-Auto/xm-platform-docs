# What's New in 4.4

## Overview

In this release we have concentrated our efforts on two key initiatives: the cloud-to-edge continuum and AI & engineering excellence. These areas reflect our commitment to delivering cutting-edge solutions and ensuring excellence in artificial intelligence and engineering practices.

This page shows a curated selection of features. For more details on what's in the latest version, please read the [Release Notes](../../release-notes/v4.4.0.md).

> [!NOTE]
> **Image Migration Note:** Fig 1: The areas in focus this release - This image needs to be created and placed in the images directory.

## Cloud-to-Edge Continuum Theme

The XMPro platform needs to be performant, scalable, and monitored to be fully cloud-agnostic. We strive to implement industry best practices to achieve this.

### Stream Host Improvements

Stream Hosts are vital to Data Stream performance. We've rewritten the Stream Hosts to guarantee higher levels of performance. As part of the site's upgrade to v4.4.0, you will also need to install the new Stream Hosts.

Stream Hosts are optimized for reliable orchestration of data streams and interactions such as publish, unpublish, sync with Data Stream Designer, and handling network disconnections.  This ensures more reliable and performance-driven data flow management across cloud and edge environments.

Enhanced logging capabilities, including detailed agent lifecycle events, provide deeper insights into the operation of Stream Hosts, facilitating better monitoring and troubleshooting.

## AI and Engineering Excellence Theme

AI and Engineering is a core pillar, aiming to harness algorithms, data insights, and computational methodologies that enhance our product's capability to build innovative solutions that address complex challenges.

### Metablocks

The new feature, Metablocks, is the first step towards plug-and-play Blocks. The first two Metablocks, Unity and Unity (Legacy), demonstrate how the modular approach improves performance. It opens the ability to support different web technologies.

Metablocks represent a significant advancement in XMPro's Application Development Platform, offering a flexible, secure, and performance-oriented solution for web application development. These blocks are designed to empower engineers and developers by enhancing app performance, security posture, and overall development experience within the App Designer (AD) environment.  See [Metablocks](../../concepts/application/metablocks.md) for a full description.

### Tree Map Block

> [!NOTE]
> **Image Migration Note:** Fig 2: Tree Map Block - This image needs to be created and placed in the images directory.

[This](../../blocks-toolbox/visualizations/tree-map.md) new App Designer block (v4.4.0) allows you to visualize hierarchical data as a set of nested rectangles whose sizes are proportional to the visualized values.

You can create tactical visualizations that showcase both hierarchical and magnitude data about operations, rather than 2D lists. For example, the relative number of recommendation alerts across different asset class and location segments.

### Live Feed Block

> [!NOTE]
> **Image Migration Note:** Fig 3: Live Feed Block - This image needs to be created and placed in the images directory.

[This](../../blocks-toolbox/visualizations/autodesk-forge-1.md) new block (v4.4.0) allows you to incorporate your IP Live Feed cameras into an application.

### Recommendation Analytics Block and Recommendation Alert Discussion Block

These two new blocks (v4.3.2) pave the way for composable Recommendation Alert pages. In future releases, we will build on the composable recommendation functionality, enabling you to design your recommendation application – should you choose not to use the out-of-the-box option.

[Recommendation Analytics](../../blocks-toolbox/recommendations/recommendation-analytics.md) gives a quick view of the percentage change and alerts generated for an asset – ideal for analyzing recommendations and supporting decision-making processes.

[Recommendation Alert Discussion](../../blocks-toolbox/recommendations/recommendation-alert-discussion.md) facilitates collaboration by allowing teams to discuss and act upon recommendations within the platform.

### Global Notification

Communicate important information to all users across the XMPro suite with the new Global Notification feature.

Global Administrators can display a [global notification](../../how-tos/manage-site-settings.md#global-notification) for a specific period, such as planned maintenance downtime along with a hyperlink to release notes. Choose from a type of hint, warning, or error to style the notification icon and banner color.

> [!NOTE]
> **Image Migration Note:** Fig 4: A global notification appears on the landing page - This image needs to be created and placed in the images directory.

### Admin Reports

Do you want to upgrade your Agent and Connector integrations but are unsure which versions are currently loaded or where they've been used? We've added [reports](../../how-tos/manage-site-settings.md#reports) (v4.3.7) to support designers in creating an upgrade path.

A master report to find the most recent version installed, and a detail report to identify Applications and Data Streams that are using older versions.

> [!NOTE]
> **Image Migration Note:** Fig 5: Data Stream Designer's Agent Usage Report - This image needs to be created and placed in the images directory.

## Support Issues Addressed

We addressed two major support issues.

### Subscription Manager Memory Issue

We've resolved a critical memory management issue, ensuring smoother operation and enhancing the platform stability ([v4.4.0](../../release-notes/v4.4.0.md#subscription-manager)).

### Live View Issue

We've resolved a connection management issue by automatically turning off Live View ([v4.3.7](../../release-notes/archived/v4.3.7.md#data-stream-designer)).  This reduces the additional load on the Data Stream Designer.

## Conclusion

This update is primarily about the improvement and scaling of Stream Hosts as part of our commitment to performance within our Cloud to Edge Continuum theme.  We also have many new features as part of the AI & Engineering Intelligence Themes.

## Previous Versions

- [What's New in 4.3](whats-new-in-4.3.md)
- [What's New in 4.2](whats-new-in-4.2.md)
- [What's New in 4.1.13](whats-new-in-4.1.13.md)
- [What's New in 4.1](whats-new-in-4.1.md)
- [What's New in 4.0](whats-new-in-4.0.md)
