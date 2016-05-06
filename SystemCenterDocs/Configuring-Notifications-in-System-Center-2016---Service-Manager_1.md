---
title: Configuring Notifications in System Center 2016 - Service Manager_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d65315b1-e815-429e-a3c8-e186b7cf3bdc
robots: noindex,nofollow
---
# Configuring Notifications in System Center 2016 - Service Manager_1
You may want to be notified by email when incidents or other changes in [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)]. By using [!INCLUDE[smshort12](./Token/smshort12_md.md)], you can make sure that notifications are generated for almost any kind of change. For example, you can configure notifications to be sent to a messaging analyst when changes occur to a work item or configuration item that pertains to email problems.

Before notifications are sent, first configure each notification channel, such as the settings for Simple Mail Transfer Protocol \(SMTP\). Notification messages are sent based on a notification template. Therefore, you must create a notification template. You can then use the Notification Subscription Wizard to subscribe a group of users to a notification that will be sent whenever the changes that you specify occur. Finally, you can verify that a notification is sent by manually generating the change.

You must complete these steps in the order shown. For example, before you can configure a notification, the SMTP channel must be enabled.

> [!NOTE]
> You must add the [!INCLUDE[smshort12](./Token/smshort12_md.md)] workflow account to the [!INCLUDE[smshort12](./Token/smshort12_md.md)] Administrators user role for notifications to function properly. See the topic “How to Add a Member to a User Role” in the [Administrator’s Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=178233).

## Configuring Notifications Topics

-   [How to Configure Notification Channels_1](./How-to-Configure-Notification-Channels_1.md)

    Describes how to set up a notification channel.

-   [How to Create Notification Templates](./How-to-Create-Notification-Templates.md)

    Describes how to set up a notification template.

-   [How to Subscribe to Notifications](./How-to-Subscribe-to-Notifications.md)

    Describes how to subscribe to a notification for yourself or for others.

-   [How to Verify a Notification Configuration](./How-to-Verify-a-Notification-Configuration.md)

    Describes how to verify that notification configuration is set up correctly.

-   [About Substitution Strings in Notification Templates](./About-Substitution-Strings-in-Notification-Templates.md)

    Describes how you can use substitution strings to insert information into notification templates.

-   [How to Automatically Notify Groups of Users](./How-to-Automatically-Notify-Groups-of-Users.md)

    Describes how to create a messaging\-enabled group and a workflow to notify stakeholders when an incident is created.

## Other Resources for This Component

-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)

-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)

-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)

-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)


