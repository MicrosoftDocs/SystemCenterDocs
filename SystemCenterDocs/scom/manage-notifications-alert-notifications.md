---
title: Subscribing to Alert Notifications
description: This article highlights the section titles contained within this section of the Operations Manager 2016 documentation.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 4b0d664b-f806-4c3f-896b-aa0160ee4fb8
---

# Subscribing to alert notifications

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, when an alert is generated, Operations Manager can notify designated individuals by email, instant message (IM), or text message (SMS). Notifications can also run commands automatically when an alert is raised on a monitored system.  
  
A notification requires the following elements:  
  
-   A Run As account that provides credentials to the Notification Account Run As profile.  
  
-   A notification channel which defines the format for the notification and the method by which the notification is sent.  
  
-   A notification subscriber which defines the recipients and the schedule for sending notifications to the subscriber.  
  
-   A notification subscription which defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification.  
  
An Operations Manager administrator must define the notification channels and if authentication is required, configure the Run As account for notifications. An Operations Manager administrator, advanced operator, or operator can create a subscriber and a subscription.  
  
## Subscribing to alert notifications topics  
  
-   [How to create and configure the Notification Action account](manage-notifications-create-configure.md)  
  
-   [How to enable an email notification channel](manage-notifications-create-email-channel.md)  
  
-   [How to enable an instant message notification channel](manage-notifications-create-im-channel.md)  
  
-   [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md)  
  
-   [How to enable a command notification channel](../om/manage/how-to-enable-a-command-notification-channel.md)  
  
-   [How to create notification subscribers](../om/manage/how-to-create-notification-subscribers.md)  
  
-   [How to create notification subscriptions](../om/manage/how-to-create-notification-subscriptions.md)  
  
-   [How to customize message content for Notifications](../om/manage/how-to-customize-message-content-for-notifications.md)  
  
-   [How to subscribe to notifications from an alert](../om/manage/how-to-subscribe-to-notifications-from-an-alert.md)  
  
