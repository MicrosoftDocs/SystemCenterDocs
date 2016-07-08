---
title: How to Configure Notifications when Developers Reassign Work Items to IT Operations in System Center 2012 SP1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5672838-9706-4c14-ba29-7e6359250e01
author:mgoedtel
manager:cfreemanwa
---
# How to Configure Notifications when Developers Reassign Work Items to IT Operations in System Center 2012 SP1
[!INCLUDE[sc2012sp1notetopic](../../om/manage/includes/sc2012sp1notetopic_md.md)]  
  
As an Information Technology \(IT\) operator, you need to know when developers request additional information or assign work items back to IT. Receiving notifications when developers make requests helps you respond faster. You can subscribe to get notifications when alerts are set to specific states. For example, you might want to receive notifications when work items are resolved or closed or when an alert is set to Resolved and ready for IT operations. You can configure instant messaging, text messages, email, or custom notifications. For more information about using notifications, see [Subscribing to Alert Notifications](http://go.microsoft.com/fwlink/?LinkId=273057).  
  
Use the following procedure to configure notifications when developers assign work items to IT operations.  
  
### To configure notifications when developers assign work items to IT operations  
  
1.  In the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] console, click **Administration**, expand **Notifications**, and then click **Subscriptions**.  
  
2.  In the **Tasks** pane, click **New**.  
  
3.  In the Notification Subscription Wizard, enter a new subscription name, and then click **Next**.  
  
4.  On the **Criteria** page, in the **Conditions** section, select **with specific resolution state**. In the **Criteria description** section, click the **specific** link. For more information, see [How to Specify Which Alerts Generate Notifications \(Conditions\)](http://go.microsoft.com/fwlink/?LinkId=273051).  
  
5.  In the **Resolution State**, select the resolution state for which you want to receive notifications. For example, if you want to receive notifications when developers request additional information from IT operations, select **Awaiting evidence**. Click **OK**, and then click **Next**.  
  
6.  On the **Subscribers** page, to specify recipients of new notifications, click **New**. For details about using the Notification Subscriber Wizard, see [How to Create Notification Subscribers](http://go.microsoft.com/fwlink/?LinkId=273058).  
  
7.  On the **Channels** page, to configure a new notification channel, such as email, instant message \(IM\), or text message, click **New**. Or, to search for a previously configured subscription channel, click **Add**. For details about using the Notification Channel Configuration Wizard, see [How to Create Notification Subscriptions](http://go.microsoft.com/fwlink/?LinkId=273060).  
  
8.  Click **Next**, and then click **Finish**.  
  
