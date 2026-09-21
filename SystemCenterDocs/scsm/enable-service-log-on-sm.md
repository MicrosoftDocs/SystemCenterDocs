---
title: Enable Service Logon for Service Manager Accounts
description: Learn how to enable service logon as the log on type for Service Manager accounts, identify accounts that need permission, and change the logon type.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 09/03/2026
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.update-cycle: 180-days
ms.topic: how-to
ms.assetid: 5eb94e4f-72b8-46ec-8417-5d776cc6288f
monikerRange: '>=sc-sm-2019'
ms.custom: engagement-fy23, engagement-fy24
---

# Enable service logon

This article describes how to enable service logon permission for System Center - Service Manager accounts. Security best practice is to disable interactive and remote interactive sessions for service accounts. Security teams across organizations have strict controls to enforce this best practice to prevent credential theft and associated attacks.

System Center - Service Manager (SM) supports hardening of service accounts, and doesn't require granting the *Allow log on locally* user right for several accounts, required in support of SM.

You must provide service logon permission to the following accounts that are used by SM management server and data warehouse management server.

| Account | Purpose | Service logon permission |
|---|---|---|
| **Service Manager Services account** | System Center Data Access Service and System Center Management Configuration service | Required |
| **Service Manager Workflow account** | Runs the *MonitoringHost.exe* process (all workflows) | Required |
| **Service reporting and analysis services accounts** | Reporting and analysis | Not required |

>[!NOTE]
>We recommend that you provide service logon permission to the accounts used by various SM connectors (AD, OM, SCO, CM, VMM, exchange connectors).

## Enable service logon as log on type

You can grant service logon permission in two ways:

- **Domain policy**: Contact your domain administrators.
- **Local group policy**: See [Enable service logon through a local group policy](#enable-service-log-on-through-a-local-group-policy).

## Identify the accounts that need service logon permission

If you don't grant service logon permission to the required accounts, *monitoringhost.exe* doesn't run under those accounts. This condition prevents some workflows, such as SLA and SLO, from running. The Operations Manager event log records the following error event:

The Health Service couldn't log on the RunAs account XXXXXXX for management group XXXX because it hasn't been granted the *Log on as a service*.

Here's a sample error:

:::image type="content" source="./media/enable-service-logon-sm/identify-logon-type.png" alt-text="Screenshot of the Operations Manager event log error showing an account that needs service logon permission.":::

## Enable service log on through a local group policy

Follow these steps:

1. Sign in with administrator privileges to the computer from which you want to provide **Log on as Service** permission to accounts.
1. Go to **Administrative Tools** and select **Local Security Policy**.
1. Expand **Local Policy** and select **User Rights Assignment**. In the right pane, right-click **Log on as a service** and select **Properties**.
1. Select **Add User** or **Group** option to add the new user.
1. In the **Select Users** or **Groups** dialog, find the user you want to add and select **OK**.
1. Select **OK** in the **Log on as a service Properties** to save the changes.

    :::image type="content" source="./media/enable-service-logon-sm/enable-service-logon-inline.png" alt-text="Screenshot of the Log on as a service Properties dialog with a user added in Local Security Policy." lightbox="./media/enable-service-logon-sm/enable-service-logon-expanded.png":::

## Change logon type from a default value

The default logon type is *Service log on*.
After a new installation of  SM or an upgrade, the logon type is Service log on by default.

You can change the default logon type by using the following steps:

1. Sign in with administrator privileges to the computer from which you want to provide **Log on as Service** permission to accounts.
1. Run `gpedit.msc`.
1. Under **Computer Configuration**, expand **Administrative Templates**.
1. Select **System Center – Operations Manager**.
1. Right-click **Monitoring Action Account Logon Type**, select **Edit**, and select **Enabled**.
1. Choose **Logon Type** from the dropdown menu.

    :::image type="content" source="./media/enable-service-logon-sm/change-logon-type-inline.png" alt-text="Screenshot of the Monitoring Action Account Logon Type policy setting with the logon type dropdown menu." lightbox="./media/enable-service-logon-sm/change-logon-type-expanded.png":::
