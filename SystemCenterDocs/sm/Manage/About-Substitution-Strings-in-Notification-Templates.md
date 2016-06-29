---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  About Substitution Strings in Notification Templates
ms.technology:  service-manager
ms.assetid:  84aa8509-89ed-471c-b716-7724c0a3cd8a
---

# About Substitution Strings in Notification Templates

>Applies To: System Center 2016 Technical Preview - Service Manager

Substitution strings are special tokens or system variables that are used in notification templates in Service Manager. These strings retrieve properties from an instance that is related to the instance for which the template was created. The strings then display the value in the notification email. Notification templates in Service Manager include substitution strings. Although you should avoid modifying the predefined templates, you can duplicate them and then modify the duplicates.

For example, the end user notification template includes a substitution string in the message body that represents the user's first name. If you want to add the user's last name, you can easily do so by using the **Insert** button, which is available when you edit a notification template, and then browsing the available strings that are available for the class of template that you are modifying. In this example, you would browse and then select **Affected User** and then select **Last Name** to insert the string into the template. Later, when the notification is sent to the user, his or her first and last name is included in the message as a salutation.

While this example is very simple, Service Manager includes substitution strings for almost every property that you might need to create notifications that can inform end users and other Service Manager users with very timely and relevant information. You can easily view the substitution strings that are available in Service Manager by opening an existing notification template and then, in the template design area, clicking the **Insert** button to view the classes and properties.
