# File Uploader

A File uploader is a Block that allows the user to upload files in an application. The File can be uploaded, downloaded, or deleted. This can be useful if you want to share certain files with users who have access to your App.

## File Uploader Properties

### Appearance

#### Common Properties

Properties that are common to most Blocks include _visibility, styling mode_, _tooltip_, and _icon;_

[See the Common Properties article for more details on common appearance properties.](../common-properties.md#appearance)

#### Label

The text that shows up next to the button.

![Label](../../images/blocks-toolbox/image-638.png)

#### Select Button Text

The text that shows on top of the Button.

![Select Button Text](../../images/blocks-toolbox/button.png)

#### Upload Failed Message

The text of the message that is shown to the user when a file upload fails.

### Behavior

#### Common Properties

The _disabled_ property is common to most Blocks;

[See the Common Properties article for more details on common behavior properties.](../common-properties.md#behavior)

#### Allowed File Extensions

This allows you to specify the types of files that are allowed to be uploaded. If left blank, any file type can be uploaded. If a file extension is listed, (for example, a .png file), the File Uploader will not allow you to upload any other file except those with a .png extension.

![Allowed File Extensions](../../images/blocks-toolbox/image-527.png)

You can add file type extensions in the following way:

![Adding File Extensions](../../images/blocks-toolbox/allowed-ext-1.gif)

#### Max File Size (MB)

This determines the maximum file size that can be uploaded. If you attempt to upload a file that exceeds the max size, it will not be uploaded.

![Max File Size](../../images/blocks-toolbox/file-size.png)

#### Multiple Upload

This allows you to upload multiple files. All selected files are zipped and then uploaded to the application.

![Multiple Upload](../../images/blocks-toolbox/image-1251.png)

#### File Name Prefix

This option is available when Multiple Upload is enabled. It allows you to add a prefix to the zip file created by Multiple Upload.

![File Name Prefix](../../images/blocks-toolbox/image-1220.png)

#### Allow Delete

This allows the user to delete the uploaded file.

![Allow Delete](../../images/blocks-toolbox/allow-delete-2.png)

### Value

#### Common Properties

The _value_ property is common to most Blocks;

[See the Common Properties article for more details on common value properties.](../common-properties.md#value)

### Validation

#### Common Properties

Properties that are common to most Blocks include: _groups to validate_;

[See the Common Properties article for more details on common validation properties.](../common-properties.md#validation)

### Action

#### Common Properties

Properties that are common to most Blocks include: _navigate to_ and _show confirmation dialog_;

[See the Common Properties article for more details on common action properties.](../common-properties.md#action)
