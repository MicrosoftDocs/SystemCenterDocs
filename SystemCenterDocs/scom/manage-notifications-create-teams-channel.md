---
title: How to enable Microsoft Teams notification channel
description: This article describes how to enable Microsoft Teams notification channel for Operations Manager.
author: v-pgaddala
ms.author: v-pgaddala
manager: evansma
ms.date: 02/01/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid: 
---

# How to enable Microsoft Teams notification channel

Earlier, System Center - Operations Manager supported integration with *Skype for Business* that allowed the users to receive alerts from Operations Manager. All *Skype for Business* customers were encouraged to start using Microsoft Teams as their communications and collaboration service - Skype for Business was retired on July 31, 2021.

In line with the lifecycle, we now support Operations Manager alerts on Teams.  Integration of Teams with Operations Manager enhances productivity as you can receive the Operations Manager alerts to Teams directly where you collaborate the most.

With System Center 2022, Microsoft Teams has been added to the existing basic Notification channel of Operations Manager. You can specify conditions to allow only certain types of alerts.

To configure alert notifications for Operations Manager, you must enable a notification channel. This topic describes how to configure a  notification channel that will send alert notifications to subscribers by using Microsoft Teams.

For detailed information about notification channels, see [Subscribing to alert notifications](/scom/manage-notifications-alert-notifications).

You can configure Operations Manager with Teams to send alerts through Operations console UI by providing the following details:
- Teams tenant information
- Azure SPN details
- Teams channel where you want to receive the alerts

> [!NOTE] 
> Integration of Operations Manager with Teams is supported for customers who use GCC, GCC High and DoD Clouds.

Before you begin, gather the following information:

- Teams tenant
- Teams
- Teams channel created. For more information, see [Overview of Teams and channels in Microsoft Teams](/microsoftteams/teams-channels-overview).
- Create an application in Azure or M365 Portal by following instructions on [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2). 
- For the newly created App, give the following Graph API permission: **ChannelMessage.Send**.

  :::image type="graph api permission" source="media/teams-notifications/graph-api-permissions.png" alt-text="screenshot showing graph api permissions.":::

## Operations Manager

For detailed information about Channel, Subscriber and Subscription in Teams, see [Subscribing to Alert Notifications](/scom/manage-notifications-alert-notifications).

| Parameters | Microsoft Teams |
|---|---|
| Notifications Channel | Provide Azure Endpoints, Azure / M365 Authentication details such as Application ID and Tenant ID, format of notifications that will be sent to Microsoft Teams. |
| Notifications Subscriber | Provide notification schedule and Microsoft Teams Channel details to which notifications will be sent. |
| Notifications Subscription | Set criteria & scope on alerts that will be sent as notifications to Microsoft Teams. Subscription defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification. |

## Integrate Operations Manager with Microsoft Teams

To integrate Operations Manager with Teams, configure a Teams channel, add a subscriber, and a subscription.

## To create and enable the Microsoft Teams notification channel

Follow these steps to enable Teams notification channel

1. Log on to the computer that will host the System Center-Operations Manager.

2. On the console, under **Notifications**, right-click **Channels**, select **New channel** > **Microsoft Teams…** . **Microsoft Teams Notification Channel** wizard opens. 

   :::image type="Microsoft Teams channel" source="media/teams-notifications/channels-wizard.png" alt-text="screenshot showing Microsoft Teams channel.":::

3. Under **Description**, enter the **Channel name**, **Description (optional)** and click **Next**. 

   :::image type="Microsoft Teams channel notification" source="media/teams-notifications/microsoft-teams-notification-channel.png" alt-text="screenshot showing Microsoft Teams notification channel wizard.":::
 
4. Under **Authentication**, enter **Tenant Id**, **Client Id** of your AAD App and click **Next**. 

5. Under **Endpoints**, **Authorization URL** and **Graph API URL for your Cloud** are set by default (if you are not a public cloud user, refer [National cloud deployments](/graph/deployments) for correct endpoints).

6. Click **Next**.

7. Under **Format**, **Teams Message**, you have a default alert format using Adaptive Cards to deliver rich alerts. See [Adaptive Cards Overview](/adaptive-cards/) to customize the Teams message as required. Also see [Adaptive Cards](/microsoftteams/platform/task-modules-and-cards/cards/cards-reference#adaptive-card) to know additional information about Adaptive cards.

The following table highlights the variables to use for various properties of the alert or links to the HTML content.

   | Alert property of the link | Variable |  
   |-------------|---|-------------|  
   |Alert Source  |$Data[Default='Not Present']/Context/DataItem/ManagedEntityPath$\$Data[Default='Not Present']/Context/DataItem/ManagedEntityDisplayName$ |
   | Alert Name  |$Data[Default='Not Present']/Context/DataItem/AlertName$ |
   |Alert Description   |$Data[Default='Not Present']/Context/DataItem/AlertDescription$  |
   | Alert Severity   |$Data[Default='Not Present']/Context/DataItem/Severity$   |
   | Alert Priority  | $Data[Default='Not Present']/Context/DataItem/Priority$  |
   | Alert Category   |$Data[Default='Not Present']/Context/DataItem/Category$  |
   | Alert Owner    | $Data[Default='Not Present']/Context/DataItem/AlertOwner$ |
   | Alert Resolved By    |$Data[Default='Not Present']/Context/DataItem/ResolvedBy$  |
   | Alert Raised Time   |$Data[Default='Not Present']/Context/DataItem/TimeRaisedLocal$  |
   | Alert Last Modified Time | $Data[Default='Not Present']/Context/DataItem/LastModifiedLocal$  |
   | Alert Last Modified By | $Data[Default='Not Present']/Context/DataItem/LastModifiedBy$ |
   | Custom FieldN (N varies from 1 to 10) | $Data[Default='Not Present']/Context/DataItem/CustomN$   |
   | WebConsole Alert Link | $Target/Property[Type=\"Notification!Microsoft.SystemCenter.AlertNotificationSubscriptionServer\"]/WebConsoleUrl$/#/monitoring/drilldown/alert/$UrlEncodeData/Context/DataItem/AlertId$ |
   | WebConsole Alert Source Link | $Target/Property[Type=\"Notification!Microsoft.SystemCenter.AlertNotificationSubscriptionServer\"]/WebConsoleUrl$/#/monitoring/drilldown/object/$UrlEncodeData/Context/DataItem/ManagedEntity$ |

## To add subscriber to the notification channel

1. Log on to the computer that will host the System Center-Operations Manager. On the console, under **Notifications**, right-click **Subscribers**,  select **Microsoft Teams**. **Notification Subscriber Wizard** opens. Under **Description**, enter **Subscriber Name** and click **Next**.
   
   :::image type="subscriber description" source="media/teams-notifications/subscriber-description.png" alt-text="screenshot showing subscriber description.":::

2. Under **Schedule**, select any of the following option based on your requirement and click **Next**.
   - **Always send notifications**
   - **Notify only during the specified times**

   :::image type="subscriber schedule" source="media/teams-notifications/subscriber-schedule.png" alt-text="screenshot showing subscriber schedule.":::
 
3. Under **Addresses**, click **Add**. **Subscribers Address** wizard opens. 

4. Under **General**, enter **Address name** to identify the subscriber.

5. Under **Channel**, enter **Channel Type** as Teams. Obtain the Address by clicking the options pertaining to a Teams Channel and getting the URL.

   :::image type="subscriber address" source="media/teams-notifications/subscriber-address.png" alt-text="screenshot showing subscriber address.":::

6. Under **Schedule**, specify **Date range**, **Weekly recurrence**, **On the selected days of the week**, **Time zone** as required and click **Finish**.
 
## To configure a Notification subscription

1. Log on to the computer that will host the System Center-Operations Manager.

2. On the console, under **Notifications**, right-click **Subscriptions**, click **New subscription...** . Create **Notification Subscription** wizard opens.

   :::image type="subscription wizard" source="media/teams-notifications/subscription-wizard.png" alt-text="screenshot showing subscription wizard.":::

3. Under **Description**, enter **Subscription name** and click **Next**.
 
4. Under **Subscribers**, Click **Search**, select the subscriber and click **Next**.

   :::image type="subscriber search" source="media/teams-notifications/subscriber-search.png" alt-text="screenshot showing subscriber search.":::
 
5. Under **Channels**, Click **Search**, select the Channel and click **Next**.

   :::image type="channel search" source="media/teams-notifications/channel-search.png" alt-text="screenshot showing channel search.":::

6. Under **Summary**, review the summary and click **Finish**.

## Error scenarios

   - Teams tenant is down
   - Incorrect Teams tenant ID used during channel configuration
   - Incorrect Teams channel ID used during subscriber configuration
   - Operations Manager channel used to connect to Teams tenant is down
