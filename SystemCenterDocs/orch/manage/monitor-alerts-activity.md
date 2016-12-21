---
title: Monitor Alerts Activity
description: The Monitor Alerts activity launches a runbook when an IBM Tivoli Netcool/OMNIbus alert matches the specified criteria.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 313a1a9f-f534-441b-be59-08ad98ff241f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Monitor Alerts Activity
=======================

Applies To: System Center 2016 - Orchestrator

The Monitor Alerts activity launches a runbook when an IBM Tivoli Netcool/OMNIbus alert matches the specified criteria. You can use the Monitor Alerts activity to launch a diagnostic and corrective runbook that responds to critical alerts in your network.

The Monitor Alerts activity uses filters to determine which properties of an alert launch the runbook.

The following tables list the triggers, filters and published data for the Monitor Alerts activity. This activity publishes all of the data from the selected filters.

### Monitor Alerts Triggers

| Element   | Description   | Value Type |
| Connection   | The name of the Netcool/OMNIbus ObjectServer connection.   | String   |
|:---|:---|:---|
| New Alerts   | The option to start the runbook when the activity detects a new alert.   | Boolean   |
| Updated Alerts | The option to start the runbook when the activity detects an update to an existing alert. | Boolean   |

### Monitor Alerts Filters

| Element | Description   | Value Type |
| Filters | A list of all configured filters. To edit or remove a filter, select the item and click Edit or Remove, respectively. |   |
|:---|:---|:---|

### Monitor Alerts Published Data

|   |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertCount<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro |

Configuring the Monitor Alerts Activity
---------------------------------------

The following procedure describes the steps required to configure a Monitor Alerts activity.

#### To configure the Monitor Alerts activity

1.  From the **Activities** pane, click and drag a **Monitor Alerts** activity to the active runbook.

2.  Double-click the **Monitor Alerts** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Details** tab as follows:

    1.  In the **ObjectServer** section, click the ellipsis button **(...)**, select the IBM Tivoli Netcool/OMNIbus server **Connection** that you want to use for this activity, and click **OK**.
    2.  In the **Triggers** section, select the type(s) of alerts, **New** and/or **Updated** that are applicable to this runbook. Each alert of the specified trigger type is compared to the values of the filter(s) to determine if they meet the criteria before triggering the runbook.
    3.  In the **Filters** section, enter a filter. Click **Add**. In the **Name** box, click the down arrow and select a property from the list.
    4.  In the **Relation** box, click the down arrow and select a filter type.
    5.  In the **Value** box, enter the value you want to use. Click **OK** to save the filter settings.
    6.  Add additional filters as needed, and then click **Finish**.

    You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow. <br>For more information about using filters, see Filter Behavior.


