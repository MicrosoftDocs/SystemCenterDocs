---
ms.assetid: 8ab415e9-b004-42eb-b12e-51d24f3f3de9
title: Console-level changes for gMSA in System Center Operations Manager
description: This article describes the console-level changes that are required to use group Managed Service Accounts (gMSAs) in Operations Manager.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.service: system-center
monikerRange: '>=sc-om-2019'
ms.subservice: operations-manager
ms.topic: concept-article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Console-level changes for group Managed Service Accounts (gMSAs)

This article describes the console-level changes that are required to use group Managed Service Accounts (gMSAs).

::: moniker range="sc-om-2019"

>[!NOTE]
>This article applies to Operations Manager 2019 Update Rollup 1 (UR1) and later.

::: moniker-end

## Change the credentials for Action accounts

In the Operations Manager console, go to **Administration** \> **Run-as configuration** \> **accounts**. Do the following actions for the accounts specified.

### Default Action account

The following images show the default **Action** account.

![Screenshot of Default Action account.](media/gmsa/default-action-account.png)

![Screenshot of Default Action monitoring host.](media/gmsa/default-action-monitoring-host.png)

Change the credentials of the default **Action** account to **gMSA**.

![Screenshot of Provide Default Action account credentials.](media/gmsa/act-gmsa.png)

![Screenshot of Default Action change credentials.](media/gmsa/default-action-change-credentials.png)

 Validate that *MonitoringHost.exe* runs as gMSA.

![Screenshot of Default Action gMSA.](media/gmsa/default-action-gmsa.png)

### Default Action account Run As profile

 Change the default **Action** account Run As profile to use the **gMSA** Run As default **Action** accounts.

 ![Screenshot of Default Action Run As account.](media/gmsa/defaul-action-run-as-account.png)

## Microsoft Monitoring Agent

To alter the agent **Action** account in the Microsoft Monitoring Agent, change the credentials from the target agent computer, as shown.

![Screenshot of Microsoft Monitoring Agent.](media/gmsa/monitoring-agent-properties.png)

### Create Run As accounts

When you create a new Run As account, enter the gMSA in the **User name** box followed by **$**. Don't enter a password. Continue to create the Run As account.

![Screenshot of Run As accounts.](media/gmsa/run-account-credentials.png)

### Discovery and push installation of the agent

When a gMSA is provided during the discovery process, leave the **Password** box blank when you add **$** at the end of the user name. The agent should install without issues on the target computers.

## Known issue and resolution

Post migration to gMSA, you might encounter an error when you export a report in Word, PowerPoint, or Excel format. This error is observed for SQL Server Reporting Services on SQL Server 2017.

This error appears to be a persistent issue with SQL Server Reporting Services in SQL Server 2017. To resolve it, follow these steps.

  1. Grant admin access to the **Execution** account on the report server.
  1. Restart SQL Server Reporting Services, and wait for 5 minutes.
  1. Try to export the reports again.
