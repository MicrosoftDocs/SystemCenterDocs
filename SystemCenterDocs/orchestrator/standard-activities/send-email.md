---
title: Send Email 
description: This article describes about Send Email activity that sends an email message using the standard SMTP protocol or an Exchange server.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/05/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 81c60f52-199b-46c7-83c9-3d38ae70b108
caps.latest.revision: 16
author: Jeronika-MS
ms.author: v-gajeronika
---

# Send Email

The Send Email activity sends an email message using the standard SMTP protocol or an Exchange server. You can use this activity to notify an administrator of problems that have occurred with a system. 

> [!IMPORTANT]
> If you put more than 1 MB of text directly into the message body, the activity can fail during initialization. To avoid this issue, enter no more than 1 MB of text directly into the message body or save the text to a file, and provide the file name as the message you want to send.  

In this article, you'll learn about the Send Email activity.

## Configure the Send Email Activity

Before you configure the Send Email activity, you'll need to determine the following:  

- Your SMTP server information.

- The recipient who will receive the email message.  

- The email message you want to send.  

Use the following information to configure the Send Email activity:  

### Details  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Subject**|Enter the subject of the email.|  
|**Recipients**|The list displays the email addresses that the email will be sent to. To add a recipient, select **Add** to open the **Recipients Properties** dialog, specify the **Email address** and from the **Recipient type** box, select **To**, **Cc**, or **Bcc**, and then select **OK**.<br /><br /> To remove a recipient, select the recipient in the **Recipients** and select **Remove**. To edit a recipient, double-click the recipient in the **Recipients** box.|  
|**Message**|Select how you want the message to be entered for this email:<br /><br /> **Text**: Enter the message body. To use HTML formatting, you'll need to select **HTML** as the **Format** on the **Advanced** tab.<br /><br /> **File**: Enter the name of the file that contains the message body. To browse for the file name, select the ellipsis **(...)** next to the **Message** box.|  
|**Attachments**|The list displays the attachments that will be sent with the email. To add an attachment, select **Add** to open the **Attachment Properties** dialog, specify the path of the attachment or select the ellipsis **(...)** next to the **File** box, and then select **OK**.<br /><br /> To remove an attachment, select the attachment in the **Attachments** box, and select **Remove**. To edit an attachment, double-click the attachment in the **Attachments** box.|  
|**Task fails if an attachment is missing**|Select this box to cause the Send Email activity to fail if any of the attachments can't be found when the email is being sent.|  

### Advanced

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Priority**|Select the priority of the email from the dropdown list.  You can select **Normal**, **Low**, or **High**.|  
|**Format**|Select the format that will be used for the message body. You can select **Rich Text**, **ASCII**, or **HTML**. **Note:** Some SPAM filters may not allow Rich Text or HTML email.|  
|**User Id**|If your SMTP server requires authentication, you'll need to enter the user ID that will be used to send the email.|  
|**Password**|The password that is associated with the User ID.|  
|**Domain**|The domain associated with the User ID.|  

### Connect

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Email address**|Enter the email address that will be inserted into the From: field of the email.|  
|**Computer**|Enter the name of the SMTP server. You can also use the ellipsis **(...)** button to browse for the server.|  
|**Port**|Select to change the port that will be used to connect to the SMTP server. The default port is 25.|  
|**Enable SSL**|Select to indicate that the SMTP connection requires SSL.|  

### Published Data

 The following table lists the published data items:  

|Item|Description|  
|----------|-----------------|  
|Subject of the email|The subject of the email that was sent.|  
|The email message Recipient|The address of the recipient of the email.|  
|Body of the email message|The body of the email.|  
|Name and path of the attached file|The full path of the file that was attached.|  
|Email account|The SMTP account that was used to send the email.|  
|Outgoing mail server (SMTP)|The name of the SMTP server used to send the email.|  
|Outgoing mail server port number|The port used to communicate with the SMTP server.|  
|Outgoing mail server SSL enabled|Indicates whether the mail server has SSL enabled.|

**Example**

1. In the **Runbook Designer**, right-click the Runbooks, select **New**, and then select **Runbook**.
2. Enter the name of the runbook, and select **Enter**.
3. In the **Activities** pane, select **Email** to expand the category, and then drag the Send email activity into the **Runbook Designer** Design workspace.
4. Double-click **Send email activity** to open the **Properties** window.
5. Configure the following Email Details:
   - **General**
     -  **Subject**: Enter the email subject.
   - **Details**
     - **To / CC / BCC**: Add the recipient email addresses.
     - **Message**: Type the email body text.
6. Configure SMTP Connection
7. Select **Finish** to save the settings.
