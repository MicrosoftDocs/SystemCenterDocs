---
title: Enable service logon
description: This article provides information about how to enable service logon as log on type.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 5eb94e4f-72b8-46ec-8417-5d776cc6288f
monikerRange: '>=sc-sm-2019'
ms.custom: engagement-fy23, engagement-fy24
---

# Enable Service Logon

Security best practice is to disable interactive and remote interactive sessions for service accounts. Security teams across organizations have strict controls to enforce this best practice to prevent credential theft and associated attacks.

System Center - Service Manager (SM) supports hardening of service accounts, and don't require granting the *Allow log on locally* user right for several accounts, required in support of SM.

You must provide service logon permission to the following accounts that are used by SM management server and data warehouse management server.

**Service Manager Services Account**:
This account is used for System Center Data Access Service and System Center Management Configuration service.

This account requires service logon permission.  

**Service Manager Workflow account**
This account is used to run the *MonitoringHost.exe* process (runs all the Workflows). This account requires service logon permission.

>[!NOTE]
>We recommend that you provide service logon permission to the accounts used by various SM connectors (AD, OM, SCO, CM, VMM, exchange connectors).
>Service reporting account and analysis services accounts don't require service logon permission.

## Enable service logon as log on type

You can grant service logon permission through a domain policy or a local group policy.

To enable using domain policy, contact your administrators. To use local group policy, see the section on [enable service through a local group policy](#enable-service-log-on-through-a-local-group-policy)

## Identify the accounts that need service logon permission

If required accounts aren't provided with service logon permission, then *monitoringhost.exe* doesn't run under those accounts. Which means, some of the workflows such as SLA/SLO wouldn't run. In such case, the following error event is logged in the Operations Manager event log:

<em>The Health Service couldn't log on the RunAs account XXXXXXX for management group XXXX because it hasn't been granted the *Log on as a service</em>

Here's a sample error:

:::image type="content" source="./media/enable-service-logon-sm/identify-logon-type.png" alt-text="Screenshot of identify accounts that need service logon permission.":::

## Enable service log on through a local group policy

Follow these steps:

1. Sign in with administrator privileges to the computer from which you want to provide **Log on as Service** permission to accounts.
2. Go to **Administrative Tools** and select **Local Security Policy**.
3. Expand **Local Policy** and select **User Rights Assignment**. In the right pane, right-click **Log on as a service** and select **Properties**.
4. Select **Add User** or **Group** option to add the new user.
5. In the **Select Users** or **Groups** dialog, find the user you wish to add and select **OK**.
6. Select **OK** in the **Log on as a service Properties** to save the changes.

    :::image type="content" source="./media/enable-service-logon-sm/enable-service-logon-inline.png" alt-text="Screenshot showing enable service logon permission." lightbox="./media/enable-service-logon-sm/enable-service-logon-expanded.png":::

## Change logon type from a default value

Default logon type is *Service log on*.
After new installation of  SM or an upgrade, logon type will be Service log on, by default.

You can change the default logon type by using the following steps:

1. Sign in with administrator privileges to the computer from which you want to provide **Log on as Service** permission to accounts.
2. Run gpedit.msc
3. Under **Computer Configuration**, expand **Administrative Templates**.
4. Select **System Center – Operations Manager**.
5. Right-click **Monitoring Action Account Logon Type**, select **Edit**, and select **Enabled**.
6. Choose **Logon Type** from the dropdown menu.

    :::image type="content" source="./media/enable-service-logon-sm/change-logon-type-inline.png" alt-text="Screenshot showing change service logon permission." lightbox="./media/enable-service-logon-sm/change-logon-type-expanded.png":::
