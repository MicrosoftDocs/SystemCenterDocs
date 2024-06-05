---
title: Enable Microsoft Teams notification channel
description: This article describes how to enable Microsoft Teams notification channel for Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 05/22/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid:
MonikerRange: 'sc-om-2022'
---

# Enable Microsoft Teams notification channel in Operations Manager

This article describes how to configure a notification channel that will send alert notifications to subscribers by using Microsoft Teams.

Earlier, System Center - Operations Manager supported integration with *Skype for Business* that allowed the users to receive alerts from Operations Manager. All *Skype for Business* customers were encouraged to start using Microsoft Teams as their communications and collaboration service as Skype for Business was retired on July 31, 2021.

In line with the lifecycle, we now support Operations Manager alerts on Microsoft Teams (Teams). Integration of Teams with Operations Manager enhances productivity, as you can receive the Operations Manager alerts to Teams directly where you collaborate the most.

With System Center 2022, Microsoft Teams has been added to the existing basic Notification channels of Operations Manager. You can specify conditions for the channel to allow only certain types of alerts.

To configure alert notifications for Operations Manager, you must enable a notification channel. For detailed information about notification channels, see [Subscribing to alert notifications](./manage-notifications-alert-notifications.md).

> [!NOTE]
> Integration of Operations Manager with Teams is supported for customers who use GCC, GCC High, and DoD Clouds.

Before you begin, make sure that you have the following items:

- Teams tenant information.
- Run As account. Delegated API type is used in Teams integration and the Run As account credentials will be used to authenticate.
  Run As account should be
  - A valid Microsoft Entra ID account (example: `user@domain`).
  - Licensed to use Microsoft Teams.
  - A member of target Microsoft Teams channel.
  - Not enabled for multifactor authentication.

  For more information, see [How to create and configure the Notification action account](./manage-notifications-create-configure.md).
- Link to the Teams channel created. For more information about Teams channels, see [Overview of Teams and channels in Microsoft Teams](/microsoftteams/teams-channels-overview).
- Details of the newly created application in Azure. Instructions to register an application available at [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).
- For the newly created App, ensure the Graph API permission is given as **ChannelMessage.Send** and **Grant admin consent for Contoso** is selected.

  :::image type="content" source="media/teams-notifications/graph-api-permissions.png" alt-text="Screenshot that shows graph API permissions.":::

- On the **Microsoft Entra ID admin center** > **Advanced settings**, ensure **Allow public client flows** is set to **Yes**.

  :::image type="content" source="media/teams-notifications/advance-settings.png" alt-text="Screenshot that shows advance settings.":::

## Operations Manager notification channel - key descriptions

For detailed information about Channel, Subscriber and Subscription, see [Subscribing to Alert Notifications](./manage-notifications-alert-notifications.md).

| Parameters | Microsoft Teams |
|---|---|
| Notifications Channel | Provide Azure endpoints, Azure / Microsoft 365 authentication details such as application ID and tenant ID, format of notifications that will be sent to Microsoft Teams. |
| Notifications Subscriber | Provide notification schedule and Microsoft Teams channel details to which notifications will be sent. |
| Notifications Subscription | Set criteria & scope on alerts that will be sent as notifications to Microsoft Teams. Subscription defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification. |

## Integrate Operations Manager with Microsoft Teams

To integrate Operations Manager with Teams, configure a Teams channel, add a subscriber, and a subscription.

## Create and enable the Microsoft Teams notification channel

1. Sign in to the computer where the Operations Manager Console is installed.

1. On the console, under **Notifications**, right-click **Channels**, select **New channel** > **Microsoft Teams*. **Microsoft Teams Notification Channel** wizard opens.

1. Under **Description**, enter the **Channel name**, **Description (optional)** and select **Next**.

   :::image type="content" source="media/teams-notifications/microsoft-teams-notification-channel.png" alt-text="Screenshot that shows Microsoft Teams notification channel wizard.":::

1. Under **Authentication**, enter **Tenant Id**, **Client Id** of your Microsoft Entra ID App, and select **Next**.

   :::image type="content" source="media/teams-notifications/authentication.png" alt-text="Screenshot that shows authentication.":::

1. Under **Endpoints**, **Authorization URL** and **Graph API URL for your Cloud** are set by default. Select **Next**. (See [National cloud deployments](/graph/deployments) for correct endpoints, if you aren't a public cloud user).

   :::image type="content" source="media/teams-notifications/endpoints.png" alt-text="Screenshot that shows fendpoints.":::

1. Under **Format**, in the **Teams Message** box, you've a default alert format using Adaptive Cards to deliver rich alerts. Select **Finish**.

   :::image type="content" source="media/teams-notifications/format.png" alt-text="Screenshot that shows format.":::

1. See [Adaptive Cards overview](/adaptive-cards/) to customize the Teams message as required. Also, see [Adaptive Cards](/microsoftteams/platform/task-modules-and-cards/cards/cards-reference#adaptive-card) to know additional information about Adaptive cards.

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

## Add a subscriber to the notification channel

1. Sign in to the computer where the Operations Manager Console is installed. On the console, under **Notifications**, right-click **Subscribers** and select **Microsoft Teams**.

   The Notification Subscriber Wizard opens.

1. Under **Description**, for **Subscriber Name**, enter a subscriber name, and then select **Next**.

   :::image type="subscriber description" source="media/teams-notifications/subscriber-description.png" alt-text="Screenshot that shows adding a  subscriber description.":::

1. Under **Schedule**, select any of the following options based on your requirement, and then select **Next**.

   - **Always send notifications**: Sends notifications all the time.
   - **Notify only during the specified times**: Sends notifications only at specific times.

   :::image type="content" source="media/teams-notifications/subscriber-schedule.png" alt-text="Screenshot that shows subscriber notification schedule options.":::

1. If you select the **Notify only during the specified times** checkbox, the **Specify Schedule** pane opens. Select values for **Date range**, **Weekly recurrence**, **On the selected days of the week**, and **Time zone** based on your requirements.

   :::image type="content" source="media/teams-notifications/notification-schedule.png" alt-text="Screenshot that shows notification schedule options.":::

1. Under **Addresses**, select **Add**.

   :::image type="content" source="media/teams-notifications/subscriber-address.png" alt-text="Screenshot that shows adding a subscriber address.":::

   The Subscribers Address wizard opens.

1. Under **General**, for **Address name**, enter an address name to identify the subscriber.

   :::image type="content" source="media/teams-notifications/subscriber-address-name.png" alt-text="Screenshot that shows the subscriber address name.":::

1. Under **Channel**, for **Channel Type**, enter **Microsoft Teams**.

   :::image type="content" source="media/teams-notifications/channel-type.png" alt-text="Screenshot that shows selecting the channel type.":::

1. Right-click the channel where you want to send the notifications and select **Get link to channel**. Copy the URL, and then enter the URL in **Delivery address for the selected channel:**.

   :::image type="content" source="media/teams-notifications/channel-link.png" alt-text="Screenshot that shows the channel link address.":::

1. Under **Schedule**, enter values for **Date range**, **Weekly recurrence**, **On the selected days of the week**, and **Time zone** based on your requirements. Select **Finish**.

   :::image type="content" source="media/teams-notifications/schedule.png" alt-text="Screenshot that shows a notificationschedule.":::  

## Configure a notification subscription

1. Sign in to the computer where the Operations Manager Console is installed.

1. On the console, under **Notifications**, right-click **Subscriptions** and select **New subscription**.

   :::image type="content" source="media/teams-notifications/subscription-wizard.png" alt-text="Screenshot that shows the notification subscription wizard.":::

   The Create Notification Subscription wizard opens.

1. Under **Description**, enter **Subscription name** and select **Next**.

   :::image type="content" source="media/teams-notifications/create-notification-subscription.png" alt-text="Screenshot that shows create notification subscription.":::

1. Set the **Scope** and **Criteria** to define the type of alerts you want notifications for.

   :::image type="content" source="media/teams-notifications/scope.png" alt-text="Screenshot that shows scope.":::

   :::image type="content" source="media/teams-notifications/criteria.png" alt-text="Screenshot that shows criteria.":::

1. Under **Subscribers**, select **Search**, select the subscriber, and select **Next**.

   :::image type="content" source="media/teams-notifications/subscriber-search.png" alt-text="Screenshot that shows subscriber search.":::

1. Under **Channels**, select **Search**, select the desired notification channel, and select **Next**.

   :::image type="content" source="media/teams-notifications/channel-search.png" alt-text="Screenshot that shows channel search.":::

1. Under **Summary**, review the summary, and select **Finish**.

## Related content

- To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md).

- To create a command channel notification, see [How to enable a command notification channel](manage-notifications-create-command-channel.md).

- To create a text message (SMS) notification channel, see [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md).
