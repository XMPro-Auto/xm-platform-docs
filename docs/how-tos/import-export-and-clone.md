# Import, Export, and Clone

All XMPro Objects allow you to export them as a file and import them to other companies or instances of XMPro Products. This allows you to continue working on the same XMPro Object such as a Data Stream or Application in a different environment without losing all your work or having to start from scratch.

## Exporting

All XMPro Objects (Agents, Applications, Data Streams, and Recommendations) can be exported as a file with a corresponding file extension.

| XMPro Object | Extension |
| --- | --- |
| Agents | _.xmp_ |
| Connectors | .xmp |
| Applications | _.xapp_ |
| App Pages | .xapg |
| Data Streams | _.xuc_ |
| Recommendations | _.xr_ |
| Forms | .xfm |

This functionality is made available on an XMPro Object's corresponding page, by selecting the _"export"_ option. When an XMPro Object is exported, only the latest version will be exported. Thus, if someone imports an XMPro Object, it will be assigned a new ID and contain only one version – the latest version that was exported.

Before the exported file is created and downloaded, you will be asked for a password to encrypt the file. The person that imports the Data Stream will have to enter the correct password in order to import it.

The App export has an advanced option that allows you to choose which files are included - by default files design time files are included and the uploads folder (runtime files) are excluded. When ticked, you can choose whether to include files that were added at runtime or exclude all files.

To export any XMPro Object, follow the steps below:

1. Navigate to the page of the XMPro Object you would like to export.
2. Click on _Export (_&#x46;or the Data Stream Designer, click on _Properties_ first, then click on _Export)._
3. Choose a strong password to encrypt the file. The person importing the file must enter the same password.
4. Click on _Ok_.
5. The exported file will appear in your downloads.

![Export Step 1](../images/import-export-clone-1.png)

![Export Step 2](../images/import-export-clone-2.png)

![Export Step 3](../images/import-export-clone-3.png)

> [!NOTE]
> To export a Widget, follow the steps in [Manage Widgets](apps/manage-widgets.md).

## Importing

All XMPro Objects (Agents, Applications, Data Streams, and Recommendations) can also be imported into other companies or instances of XMPro, to avoid needing to replicate a particular Data Stream or Application from scratch. Importing is done from a different location as exporting, which is on the page for the corresponding feature.

To import any XMPro Object, follow the steps below:

1. Navigate to the page of the XMPro Object you would like to import.
2. Click on _Import_.
3. Upload the corresponding import file for the XMPro Object.
4. Enter the password.
5. Click on _Upload._

![Import Step 1](../images/import-export-clone-4.png)

   6\. Configure any details.\
   7\. When finished, select _Save_.

![Import Step 2](../images/import-export-clone-5.png)

> [!NOTE]
> To import an App Page, follow the steps in [Import an App Page](apps/import-an-app-page.md).

> [!NOTE]
> To import a Widget, follow the steps in [Manage Widgets](apps/manage-widgets.md).

## Cloning

To clone any XMPro Object, follow the steps below:

1. Navigate to the page of the XMPro Object you would like to clone.
2. Click on _Clone_.

![Clone Step 1](../images/import-export-clone-6.png)

   3\. Give the cloned XMPro Object a new name.\
   4\. Select the version of the app you would like to clone.\
   5\. Click on _Ok_.

![Clone Step 2](../images/import-export-clone-7.png)

The XMPro Object will be cloned and you will be able to see it in the list of Applications, Data Streams, or Recommendations, etc.

![Clone Step 3](../images/import-export-clone-8.png)
