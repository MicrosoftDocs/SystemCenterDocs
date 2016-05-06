---
title: Send Email_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762a752e-24e5-4ab4-8e61-e77f7b689165
---
# Send Email_1
The Send Email activity sends an email message using the standard SMTP protocol or an Exchange server. You can use this activity to notify an administrator of problems that have occurred with a system.

> [!IMPORTANT]
> If you put more than 1 MB of text directly into the message body, the activity can fail during initialization. To avoid this issue, enter no more than 1 MB of text directly into the message body or save the text to a file, and provide the file name as the message you want to send.

## Configuring the Send Email Activity
Before you configure the Send Email activity, you will need to determine the following:

-   Your SMTP server information

-   The recipient who will receive the email message.

-   The email message you want to send.

Use the following information to configure the Send Email activity.

### Details

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Subject**|Type the subject of the email.|
|**Recipients**|The list displays the email addresses that the email will be sent to. To add a recipient, click **Add** to open the **Recipients Properties** dialog box, specify the **Email address** and from the **Recipient type** box, select **To**, **Cc**, or **Bcc**, and then click **OK**.<br /><br />To remove a recipient, select the recipient in the **Recipients** and click **Remove**. To edit a recipient, double\-click the recipient in the **Recipients** box.|
|**Message**|Select how you want the message to be entered for this email:<br /><br />**Text**: Type the message body. To use HTML formatting, you will need to select **HTML** as the **Format** on the **Advanced** tab.<br /><br />**File**: Type the name of the file that contains the message body. To browse for the file name, click the ellipsis **\(...\)** button next to the **Message** box.|
|**Attachments**|The list displays the attachments that will be sent with the email. To add an attachment, click **Add** to open the **Attachment Properties** dialog box, specify the path of the attachment or click the ellipsis **\(...\)** button next to the **File** box, and then click **OK**.<br /><br />To remove an attachment, select the attachment in the **Attachments** box, and click **Remove**. To edit an attachment, double\-click the attachment in the **Attachments** box.|
|**Task fails if an attachment is missing**|Select this box to cause the Send Email activity to fail if any of the attachments cannot be found when the email is being sent.|

### Advanced

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Priority**|Select the priority of the email from the drop\-down list.  You can select **Normal**, **Low**, or **High**.|
|**Format**|Select the format that will be used for the message body. You can select **Rich Text**, **ASCII**, or **HTML**. **Note:** Some SPAM filters may not allow Rich Text or HTML email.|
|**User Id**|If your SMTP server requires authentication, you will need to type the user ID that will be used to send the email.|
|**Password**|The password that is associated with the User ID.|
|**Domain**|The domain associated with the User ID.|

### Connect

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Email address**|Type the email address that will be inserted into the From: field of the email.|
|**Computer**|Type the name of the SMTP server. You can also use the ellipsis **\(...\)** button to browse for the server.|
|**Port**|Select to change the port that will be used to connect to the SMTP server. The default port is 25.|
|**Enable SSL**|Select to indicate that the SMTP connection requires SSL.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Subject of the email|The subject of the email that was sent.|
|The email message Recipient|The address of the recipient of the email.|
|Body of the email message|The body of the email.|
|Name and path of the attached file|The full path of the file that was attached.|
|Email account|The SMTP account that was used to send the email.|
|Outgoing mail server \(SMTP\)|The name of the SMTP server used to send the email.|
|Outgoing mail server port number|The port used to communicate with the SMTP server.|
|Outgoing mail server SSL enabled|Indicates whether the mail server has SSL enabled.|


