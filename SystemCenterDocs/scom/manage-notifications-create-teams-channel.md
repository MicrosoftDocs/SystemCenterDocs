---
title: How to enable Microsoft Teams notification channel
description: This article describes how to enable Microsoft Teams notification channel for Operations Manager.
author: Farha-Bano
ms.author: v-farhabano
manager: mkluck
ms.date: 07/20/2023
ms.custom: UpdateFrequency2, engagement-fy23
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
ms.assetid:
MonikerRange: 'sc-om-2022'
---

# How to enable Microsoft Teams notification channel in Operations Manager

This article describes how to configure a notification channel that will send alert notifications to subscribers by using Microsoft Teams.

Earlier, System Center - Operations Manager supported integration with *Skype for Business* that allowed the users to receive alerts from Operations Manager. All *Skype for Business* customers were encouraged to start using Microsoft Teams as their communications and collaboration service as Skype for Business was retired on July 31, 2021.

In line with the lifecycle, we now support Operations Manager alerts on Microsoft Teams (Teams). Integration of Teams with Operations Manager enhances productivity, as you can receive the Operations Manager alerts to Teams directly where you collaborate the most.

With System Center 2022, Microsoft Teams has been added to the existing basic Notification channels of Operations Manager. You can specify conditions for the channel to allow only certain types of alerts.

To configure alert notifications for Operations Manager, you must enable a notification channel. For detailed information about notification channels, see [Subscribing to alert notifications](/system-center/scom/manage-notifications-alert-notifications).

> [!NOTE]
> Integration of Operations Manager with Teams is supported for customers who use GCC, GCC High, and DoD Clouds.

Before you begin, ensure you've the following:

- Teams tenant information.
- Run As account. Delegated API type is used in Teams integration and the Run As account credentials will be used to authenticate.
  Run As account should be
   - A valid Azure Active Directory (Azure AD) account (sample: user@domain)
   - Licensed to use Microsoft Teams
   - A member of target Microsoft Teams channel
   - Not enabled for multifactor authentication (MFA)
   
  For more information, see [How to create and configure the Notification action account](/system-center/scom/manage-notifications-create-configure).
- Link to the Teams channel created. For more information about Teams channels, see [Overview of Teams and channels in Microsoft Teams](/microsoftteams/teams-channels-overview).
- Details of the newly created application in Azure. Instructions to register an application available at [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).
- For the newly created App, ensure the Graph API permission is given as **ChannelMessage.Send** and **Grant admin consent for Contoso** is selected.

  :::image type="graph api permission" source="media/teams-notifications/graph-api-permissions.png" alt-text="screenshot showing graph api permissions.":::

- On the **Azure Active Directory admin center** > **Advanced settings**, ensure **Allow public client flows** is set to **Yes**.

  :::image type="advance settings" source="media/teams-notifications/advance-settings.png" alt-text="screenshot showing advance settings.":::

## Operations Manager notification channel - key descriptions

For detailed information about Channel, Subscriber and Subscription, see [Subscribing to Alert Notifications](/system-center/scom/manage-notifications-alert-notifications).

| Parameters | Microsoft Teams |
|---|---|
| Notifications Channel | Provide Azure endpoints, Azure / Microsoft 365 authentication details such as application ID and tenant ID, format of notifications that will be sent to Microsoft Teams. |
| Notifications Subscriber | Provide notification schedule and Microsoft Teams channel details to which notifications will be sent. |
| Notifications Subscription | Set criteria & scope on alerts that will be sent as notifications to Microsoft Teams. Subscription defines the criteria for sending a notification, the channel to be used, and the subscribers to receive the notification. |

## Integrate Operations Manager with Microsoft Teams

To integrate Operations Manager with Teams, configure a Teams channel, add a subscriber, and a subscription.

## Create and enable the Microsoft Teams notification channel

Follow these steps:

1. Sign in to the computer where the Operations Manager Console is installed.

2. On the console, under **Notifications**, right-click **Channels**, select **New channel** > **Microsoft Teams…**. **Microsoft Teams Notification Channel** wizard opens.

3. Under **Description**, enter the **Channel name**, **Description (optional)** and select **Next**.

   :::image type="Microsoft Teams channel notification" source="media/teams-notifications/microsoft-teams-notification-channel.png" alt-text="screenshot showing Microsoft Teams notification channel wizard.":::

4. Under **Authentication**, enter **Tenant Id**, **Client Id** of your Azure Active Directory (Azure AD) App, and select **Next**.

   :::image type="authentication" source="media/teams-notifications/authentication.png" alt-text="screenshot showing authentication.":::

5. Under **Endpoints**, **Authorization URL** and **Graph API URL for your Cloud** are set by default. Select **Next**. (See [National cloud deployments](/graph/deployments) for correct endpoints, if you aren't a public cloud user).

   :::image type="endpoints" source="media/teams-notifications/endpoints.png" alt-text="screenshot showing endpoints.":::

6. Under **Format**, in the **Teams Message** box, you've a default alert format using Adaptive Cards to deliver rich alerts. Select **Finish**.

   :::image type="format" source="media/teams-notifications/format.png" alt-text="screenshot showing format.":::

7. See [Adaptive Cards Overview](/adaptive-cards/) to customize the Teams message as required. Also, see [Adaptive Cards](/microsoftteams/platform/task-modules-and-cards/cards/cards-reference#adaptive-card) to know additional information about Adaptive cards.

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

Follow these steps:

1. Sign in to the computer where the Operations Manager Console is installed. On the console, under **Notifications**, right-click **Subscribers**, and select **Microsoft Teams**. **Notification Subscriber Wizard** opens.

2. Under **Description**, enter **Subscriber Name** and select **Next**.

   :::image type="subscriber description" source="media/teams-notifications/subscriber-description.png" alt-text="screenshot showing subscriber description.":::

3. Under **Schedule**, select any of the following options based on your requirement and select **Next**.
   - **Always send notifications** - Allows you to send the notifications all the time.
   - **Notify only during the specified times** - Allows you to send the notification only on specified times.

   :::image type="subscriber schedule" source="media/teams-notifications/subscriber-schedule.png" alt-text="screenshot showing subscriber schedule.":::

4. If you select **Notify only during the specified times** option, **Specify Schedule** page opens. Select the **Date range**, **Weekly recurrence**, **On the selected days of the week**, and **Time zone** based on your requirement.

   :::image type="notification schedule" source="media/teams-notifications/notification-schedule.png" alt-text="screenshot showing notification schedule.":::

4. Under **Addresses**, select **Add**. **Subscribers Address** wizard opens.

   :::image type="subcriber address" source="media/teams-notifications/subscriber-address.png" alt-text="screenshot showing subscriber address.":::

5. Under **General**, enter **Address name** to identify the subscriber.

   :::image type="subscriber address name" source="media/teams-notifications/subscriber-address-name.png" alt-text="screenshot showing subscriber address name.":::

6. Under **Channel**, enter **Channel Type** as Microsoft Teams.

   :::image type="channel type" source="media/teams-notifications/channel-type.png" alt-text="screenshot showing channel type.":::

7. In the Microsoft Teams, right-click the channel where you want to send the notifications, select **Get link to channel** and copy the URL and enter the URL in the **Delivery address for the selected channel:** field.

   :::image type="channel link" source="media/teams-notifications/channel-link.png" alt-text="screenshot showing channel link address.":::

8. Under **Schedule**, specify **Date range**, **Weekly recurrence**, **On the selected days of the week**, **Time zone** as required, and select **Finish**.

   :::image type="schedule" source="media/teams-notifications/schedule.png" alt-text="screenshot showing schedule.":::  

## Configure a notification subscription

Follow these steps:

1. Sign in to the computer where the Operations Manager Console is installed.

2. On the console, under **Notifications**, right-click **Subscriptions**, select **New subscription...**. Create **Notification Subscription** wizard opens.

   :::image type="subscription wizard" source="media/teams-notifications/subscription-wizard.png" alt-text="screenshot showing subscription wizard.":::

3. Under **Description**, enter **Subscription name** and select **Next**.

   :::image type="create notification subscription" source="media/teams-notifications/create-notification-subscription.png" alt-text="screenshot showing create notification subscription.":::

4. Set the **Scope** and **Criteria** to define the type of alerts you want notifications for.

   :::image type="scope" source="media/teams-notifications/scope.png" alt-text="screenshot showing scope.":::

   :::image type="criteria" source="media/teams-notifications/criteria.png" alt-text="screenshot showing criteria.":::

5. Under **Subscribers**, select **Search**, select the subscriber, and select **Next**.

   :::image type="subscriber search" source="media/teams-notifications/subscriber-search.png" alt-text="screenshot showing subscriber search.":::

6. Under **Channels**, select **Search**, select the desired notification channel, and select **Next**.

   :::image type="channel search" source="media/teams-notifications/channel-search.png" alt-text="screenshot showing channel search.":::

7. Under **Summary**, review the summary, and select **Finish**.

## Next steps

* To create an email notification channel, see [How to enable an email notification channel](manage-notifications-create-email-channel.md).

* To create a command channel notification, see [How to enable a command notification channel](manage-notifications-create-command-channel.md).

* To create a text message (SMS) notification channel, see [How to enable a text message (SMS) notification channel](manage-notifications-create-txt-channel.md).
