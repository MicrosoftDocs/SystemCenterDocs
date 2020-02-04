---
ms.assetid: 8ab415e9-b004-42eb-b12e-51d24f3f3de9
title: Console level changes for gMSA in System Center Operations Manager
description: This article details the console level changes that are required to use group managed service accounts (gMSA), a new feature supported in Operations Manager 2019 UR1.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---


# Console level changes
This article details the console level changes that are required to use group Managed Service Accounts (gMSA).

>[!NOTE]
>This article is applicable for System Center 2019 UR1 - Operations Manager.

## Change the credentials for Action accounts

In Operations Manager console, navigate to **Administration** \> **Run-as configuration** \> **accounts** and do the following for the accounts specified:

### Default Action account

The following images show the default Action account:

![Default action account](media/gmsa/default-action-account.png)

![Default action monitoring host](media/gmsa/default-action-monitoring-host.png)

Change the credentials of the default Action account to gMSA.

![Default action account](media/gmsa/act-gmsa.png)

![Default action change credentials](media/gmsa/default-action-change-credentials.png)

 Validate that *monitoringhost.exe* runs as gMSA.

![Default action gMSA](media/gmsa/default-action-gmsa.png)

### Default Action account run as profile

 Change the Default Action account run as profile to use the gMSA run as as default action accounts.

 ![Default action run as account](media/gmsa/defaul-action-run-as-account.png)

## Microsoft Monitoring Agent
To alter the agent action account in the Microsoft Monitoring Agent (MMA), change the credentials from the target agent computer, as shown below:

![Microsoft Monitoring Agent](media/gmsa/monitoring-agent-properties.png)

### Create run as accounts
While creating a new run as account, enter the gMSA in the *username* field followed by a '$' sign. Do not enter a password, continue to create the run as account.

![Run as accounts](media/gmsa/run-account-credentials.png)

### Discovery and Push install of the agent

When a gMSA is provided during the discovery process, leave  the password field blank when you suffix '$' at the end of the user name. The agent should install without issues on the target computers.

## Known issue and resolution

Post migration to gMSA, you might encounter an error while exporting a report in Word, PowerPoint, or Excel format. This is specifically observed for SQL Server Reporting services on SQL Server 2017.

This error appears to be a persistent issue with SSRS in SQL Server 2017 and can be resolved by following these steps:

  1. Grant admin access to the *Execution* account on the report server
  2. Restart the Reporting Service and wait for 5 minutes
  3. Try to export the reports again
