---
ms.assetid: 8ab415e9-b004-42eb-b12e-51d24f3f3de9
title: Console-level changes for gMSA in System Center Operations Manager
description: This article describes the console-level changes that are required to use group Managed Service Accounts (gMSAs) in Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.date: 02/03/2026
ms.service: system-center
monikerRange: '>=sc-om-2019'
ms.subservice: operations-manager
ms.topic: concept-article
ms.custom:
  - UpdateFrequency2
  - engagement-fy24
  - sfi-image-nochange
---

# Console-level changes for group Managed Service Accounts (gMSAs)

This article describes the console-level changes that you need to use group Managed Service Accounts (gMSAs).

::: moniker range="sc-om-2019"

>[!NOTE]
>This article applies to Operations Manager 2019 Update Rollup 1 (UR1) and later.

::: moniker-end

## Change the credentials for Action accounts

In the Operations Manager console, go to **Administration** \> **Run-as configuration** \> **accounts**. Perform the following actions for the specified accounts.

### Default Action account

The following images show the default **Action** account.

:::image type="content" source="media/gmsa/default-action-account.png" alt-text="Screenshot of Default Action account.":::

:::image type="content" source="media/gmsa/default-action-monitoring-host.png" alt-text="Screenshot of Default Action monitoring host.":::

Change the credentials of the default **Action** account to **gMSA**.

:::image type="content" source="media/gmsa/act-gmsa.png" alt-text="Screenshot of Provide Default Action account credentials.":::

:::image type="content" source="media/gmsa/default-action-change-credentials.png" alt-text="Screenshot of Default Action change credentials.":::

 Validate that *MonitoringHost.exe* runs as gMSA.

:::image type="content" source="media/gmsa/default-action-gmsa.png" alt-text="Screenshot of Default Action gMSA.":::

### Default Action account Run As profile

 Change the default **Action** account Run As profile to use the **gMSA** Run As default **Action** accounts.

 :::image type="content" source="media/gmsa/defaul-action-run-as-account.png" alt-text="Screenshot of Default Action Run As account.":::

## Microsoft Monitoring Agent

To change the agent **Action** account in the Microsoft Monitoring Agent, update the credentials from the target agent computer, as shown.

:::image type="content" source="media/gmsa/monitoring-agent-properties.png" alt-text="Screenshot of Microsoft Monitoring Agent.":::

### Create Run As accounts

When you create a new Run As account, enter the gMSA in the **User name** box followed by **$**. Don't enter a password. Continue to create the Run As account.

:::image type="content" source="media/gmsa/run-account-credentials.png" alt-text="Screenshot of Run As accounts.":::

### Discovery and push installation of the agent

When you provide a gMSA during the discovery process, leave the **Password** box blank when you add **$** at the end of the user name. The agent should install without problems on the target computers.

## Known issue and resolution

After migration to gMSA, you might encounter an error when you export a report in Word, PowerPoint, or Excel format. SQL Server Reporting Services on SQL Server 2017 shows this error.

This error is a persistent problem with SQL Server Reporting Services in SQL Server 2017. To resolve it, follow these steps.

  1. Grant admin access to the **Execution** account on the report server.
  1. Restart SQL Server Reporting Services, and wait for five minutes.
  1. Try to export the reports again.
