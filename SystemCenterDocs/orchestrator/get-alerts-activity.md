---
title: Get Alerts Activity
description: The Get Alerts activity retrieves an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer and replicates it to a trouble ticketing system.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e2becb8c-2960-44a3-8644-fd696c48f133
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Get Alerts Activity

Applies To: System Center 2016 - Orchestrator

The Get Alerts activity retrieves an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer and replicates it to a trouble ticketing system.

The following tables list the required properties, optional properties, and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Get Alerts Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Connection | The name of the Netcool/OMNIbus ObjectServer connection that you want to use. | String   | Yes   |
| Filters   | A list of all configured filters.   | String   | No   |

### Get Alerts Optional Properties
This activity has no optional properties.

### Get Alerts Published Data
This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertCount<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro

## Configuring the Get Alerts Activity

The following procedure describes the steps required to configure a Get Alerts activity.

### To configure the Get Alerts Activity

1.  From the **Activities** pane, click and drag a **Get Alerts** activity to the active runbook.
2.  Double-click the **Get Alerts** activity icon. The **Properties** dialog box opens.
3.  Configure the settings in the **Details** tab as follows:
    1.  In the **Connection** section, click the ellipsis button **(...)**, and then select the IBM Tivoli Netcool/OMNIbus ObjectServer connection that you want to use for this activity. Click **OK**.
    2.  In the **Filters** section, enter a filter. Click **Add**. In the **Name** box, click the down arrow and select a property from the list.
    3.  In the **Relation** box, click the down arrow and select a filter type.
    4.  In the **Value** box, enter the value you want to use. Click **OK** to save the filter settings.
    5.  Add additional filters as needed, and then click **Finish**.

You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow. 
