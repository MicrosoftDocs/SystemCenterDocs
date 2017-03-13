---
title: Step 10 - Optionally create a notification template and subscription
description: Describes the tenth step of the Service Manager Authoring Tool Woodgrove Bank customization scenario to optionally create a notification template and subscription.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edc8f5eb-6b39-42d0-b572-2b12164afdf9
---

# Step 10 of the customization scenario - Optionally create a notification template and subscription

>Applies To: System Center 2016 - Service Manager

If System Center - Service Manager is configured with a Simple Mail Transfer Protocol \(SMTP\) server, as part of the Woodgrove Bank customization scenario, Ken can configure an email notification that will be sent to him when a new computer is added to the compliance group. This is an optional step.  

 The following procedure provides only the high\-level steps for creating the **Computer Added to AppLocker Policy Notification Template** email notification template and subscription in the Service Manager console. For the complete procedure for creating a notification template, see [How to Create Notification Templates](admin-how-to-create-notification-templates.md).  

### To create an email notification template and subscription  

1.  In the Service Manager console, create a new notification email template. In the **Administration** pane, click **Notifications**, and then click **Templates**. In the **Tasks** pane, select **Create E\-mail Template**, and then complete the Create E\-Mail Notification Template Wizard.  

2.  On the **General** page, specify the **Name** to be **AppLocker Policy Notification Template**, and specify the **Class** as **Automated Activity: Add Computer to AD Group**. Specify **Management pack** to be **Woodgrove Automated Activity - Add Computer To Group**.  

3.  On the **Template Design** page, in the **Subject** box, type **Computer**, and then click **Insert**. In the **Property Picker** dialog box, select **ComputerName**. Add the following text to the **Subject** box: **was added to the AppLocker Policy Group**. Add any text in the **MessageBody** box, and save the template.  

4.  In the **Administration** pane, click **Notifications**, and then click **Subscriptions**. In the **Tasks** pane, click **Create Subscription**, and then complete the Create E\-Mail Notification Subscription Wizard.  

5.  In the **Name** box, type **Computer Added to AppLocker Policy Notification**.  

6.  In the **Class** box, type **Automated Activity: Add Computer to AD Group**.  

7.  Specify **Notification condition** to be **When an object of the selected type is updated**.  

8.  Specify **Management pack** to be **Woodgrove Automated Activity - Add Computer To Group**.  

9. On the **Additional Criteria** page, add criteria in which **Status** equals **Completed**.  

10. On the **Template** page, specify **E\-mail template** to be the previously created template, **Computer added to AppLocker Policy Notification**.  

11. On the **Recipient**  page, add recipients from your organization.  
