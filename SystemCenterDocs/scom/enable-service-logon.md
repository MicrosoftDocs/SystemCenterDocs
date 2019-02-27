---
ms.assetid: 19659b4f-05d3-4f33-9dd4-689b2a9fc21b
title: Enable Service Log on by default for System Center Operations Manager
description: This article provides information about how to enable service log on by default for System Center 2019 - Operations Manager.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2019'
---

# Enable Service Log on for run as accounts

Security best practice is to disable  Interactive and remote Interactive log on permissions for service accounts. Security teams, across organizations have strict controls to enforce this best practice to prevent credential theft and associated attacks.

System Center 2019 - Operations Manager supports hardening of service accounts and requires no Interactive or  Remote Interactive log on rights for service accounts.

Earlier version of Operations Managers has *Allow log on locally* as the default log on type. Operations Manager 2019 uses *Service Log on* as the log on type, by default. This leads to the following changes:

-	Health Service uses log on type **Service** by default. In Operations Manager 1807 and prior versions, health service used **Interactive** as log on type.
-	Operations Manager action accounts and service accounts now have **Log on as a Service** permission.     
-	Action accounts and Run As accounts must have **Log on as a Service** permission to execute MonitoringHost.exe.
    [Learn more](plan-security-accounts.md)

## Changes to Operations Manager action accounts
 The following accounts are granted **Log on as a Service** permission during the Operations Manager 2019 installation, and during upgrade from previous versions:

 -	Management Server Action account
 -	System Center configuration service and System Center data access service accounts  
 -	Agent Installation account
 -	Data Warehouse Writer account
 -	Data Reader accounts
    ![local security setting](./media/enable-service-logon/om2019-local-security-setting.png)

After this change, **Run As accounts**, which are created by Operations Manager administrators for the management packs (MPs), require **Log on as a Service** permission.

### View log on type for management servers and agents

You can view the log on type for management servers and agents from Operations Manager console.

To view the log on type for management servers, go to
**Administration** > **Operations Manager Products**> **Management servers**.

![Log on type for management servers](./media/enable-service-logon/logon-type-management-servers.png)

To view the log on type for agents, go to
**Administration** > **Operations Manager Products**> **Agents**.

![Log on type for management servers](./media/enable-service-logon/logon-type-agents.png)

> [!NOTE]

> Log on type for the agent/gateway, which is not yet upgraded  display *Service* as log on type, irrespective of the agent's current log on type. Once the agent is upgraded, the current log on type will be displayed.

## Enable service log on permission for Run As accounts

Follow these steps:

1. Log on with administrator privileges to the computer from which you want to provide *Log on as Service* permission to a Run As account.
2. Go to **Administrative Tools** and click **Local Security Policy**.
3. Expand **Local Policy** and click **User Rights Assignment**.
4. In the right pane, right-click **Log on as a service** and select **Properties**.
5. Click **Add User or Group** option to add the new user.
6. In the **Select Users or Groups** dialogue, find the user you wish to add and click **OK**.
7. Click **OK** in the **Log on as a service Properties** to save the changes.

    ![Select users](./media/enable-service-logon/om2019-select-users.png)

> [!NOTE]

> If you are upgrading to Operations Manager 2019 from a previous version or installing a new Operations Manager 2019 environment, follow the steps above to provide **Log on as a service** permission to Run As accounts.

## Change log on type for a health service

If you need to change the log on type of Operations Manager health service to Interactive, use the local group policy on the agent computer as shown below:

> [!NOTE]
> A monitor-based alert is generated for this event.

![Monitoring action account log on types](./media/enable-service-logon/om2019-monitoring-action-account-logon-type.png)

## Coexistence with Operations Manager 2016 agent
Helath service in Operations Manager 2016 uses *Interactive* as log on type. Operations Manager uses *Log on as a service* as default. However, Operations Manager 2019 and 2016 can interoperate without any issues as log on type of health service has no impact on the interoperability.  

Following scenarios are impacted:.
 - Push install from Operations Manager console requires admin privilege and *Log on as a service* permission.
 - Operations Manager MS action account required admin privilege on management server for Service Manager monitoring.


## Troubleshooting

If any of the Run as accounts do have the required **Log on as a Service** permission, a critical monitor-based alert appears. This alert displays the  details of the Run as account, which does not have **Log on as a Service** permission.

![alert properties](./media/enable-service-logon/om2019-alert-properties.png)

In the event viewer, on the agent computer, see the information under event ID 7002 for details about all the **Run as account** that requires **Log on as a Service** permission.

|Parameter|Message|
|--------------------|---------------|
|Alert Name|Run As account does not have requested log on type.|
|Alert Description|The Run As account must have the requested log on type.|
|Alert Context |Health Service could not log on as the  Run As Account  for management group (group name) because it has not been granted the *Log on as a service* permission.|
|Monitor|(add monitor name)|

Provide **Log on as a Service** permission to the applicable Run As accounts, which are identified in the event 7002.

Once you provide the **Log on as a Service** permission, event ID 7028 appears and the monitor changes to healthy state.

![number of events](./media/enable-service-logon/om-2019-number-of-events.png)
