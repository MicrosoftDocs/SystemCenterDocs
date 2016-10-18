---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
title:  Configuring Service Manager Notifications
ms.technology:  service-manager
ms.assetid:  a74d2677-96ac-44ac-8f45-12d2e24b0275
---

# Configuring Service Manager Notifications

>Applies To: System Center 2016 - Service Manager

You may want to be notified by email when incidents or other changes in Service Manager. By using Service Manager, you can make sure that notifications are generated for almost any kind of change. For example, you can configure notifications to be sent to a messaging analyst when changes occur to a work item or configuration item that pertains to email problems.

Before notifications are sent, first configure each notification channel, such as the settings for Simple Mail Transfer Protocol (SMTP). Notification messages are sent based on a notification template. Therefore, you must create a notification template. You can then use the Notification Subscription Wizard to subscribe a group of users to a notification that will be sent whenever the changes that you specify occur. Finally, you can verify that a notification is sent by manually generating the change.

You must complete these steps in the order shown. For example, before you can configure a notification, the SMTP channel must be enabled.

> [!NOTE]
> You must add the Service Manager workflow account to the Service Manager Administrators user role for notifications to function properly.
