---
title: Verify a notification configuration
description: Describes how to you can verify a notification configuration in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 9395bb54-3aab-48e3-9b9f-8b874d213fe3
---

# Verify a notification configuration in Service Manager

>Applies To: System Center 2016 - Service Manager

You can use the following procedure to verify that you have correctly configured notifications. Generate the type of change that activates the notification subscription that was previously created. When you do this, the subscription generates and then sends a notification. Receipt of the notification verifies success. For example, create a test incident that generates an email notification. The notification informs the recipient that an incident was opened.

If you are verifying a recurring notification subscription, you must wait for the time interval that you set previously to elapse until the notification is sent. When the notification is received, the configuration of the notification is verified.

### To verify a notification configuration

1.  In the Service Manager console, click **Work Items**.

2.  In the **Work Items** pane, expand **Work Items**, expand **Incident Management**, and then click **All Open Incidents**.

3.  In the **Tasks** pane, under **Incident Management**, click **Create Incident**.

4.  In the **Incident *Number* New** form, enter the required information in the **Affected user**, **Title**, **Classification Category**, **Impact**, and **Urgency** boxes.

5.  In the **Classification Category** list, select **E-mail Problems**, and then click **OK**.

6.  Verify that an email notification that contains the information you entered in the template is received. The email title should contain the incident ID number.
