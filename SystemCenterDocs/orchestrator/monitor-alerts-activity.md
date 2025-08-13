---
title: Monitor Alerts activity
description: The Monitor Alerts activity launches a runbook when an IBM Tivoli Netcool/OMNIbus alert matches the specified criteria.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 313a1a9f-f534-441b-be59-08ad98ff241f
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Monitor Alerts activity

The Monitor Alerts activity launches a runbook when an IBM Tivoli Netcool/OMNIbus alert matches the specified criteria. You can use the Monitor Alerts activity to launch a diagnostic and corrective runbook that responds to critical alerts in your network.

The Monitor Alerts activity uses filters to determine which properties of an alert launch the runbook.

The following tables list the triggers, filters, and published data for the Monitor Alerts activity. This activity publishes all the data from the selected filters.

### Monitor Alerts triggers

| Element   | Description   | Value Type |
|:---|:---|:---|
| Connection   | The name of the Netcool/OMNIbus ObjectServer connection.   | String   |
| New Alerts   | The option to start the runbook when the activity detects a new alert.   | Boolean   |
| Updated Alerts | The option to start the runbook when the activity detects an update to an existing alert. | Boolean   |

### Monitor Alerts filters

| Element | Description   | Value Type |
|:---|:---|:---|
| Filters | A list of all configured filters. To edit or remove a filter, select the item, and select Edit or Remove, respectively. |   |

### Monitor Alerts published data

This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertCount<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro

## Configure the Monitor Alerts activity

The following procedure describes the steps required to configure a Monitor Alerts activity.

1. From the **Activities** pane, select and drag a **Monitor Alerts** activity to the active runbook.

2. Double-click the **Monitor Alerts** activity icon. The **Properties** dialog opens.

3. Configure the settings in the **Details** tab as follows:

    1. In the **ObjectServer** section, select the ellipsis button **(...)**, select the IBM Tivoli Netcool/OMNIbus server **Connection** that you want to use for this activity, and select **OK**.
    2. In the **Triggers** section, select the type(s) of alerts, **New** and/or **Updated** that are applicable to this runbook. Each alert of the specified trigger type is compared to the values of the filter(s) to determine if they meet the criteria before triggering the runbook.
    3. In the **Filters** section, enter a filter. Select **Add**. In the **Name** box, select the down arrow and select a property from the list.
    4. In the **Relation** box, select the down arrow and select a filter type.
    5. In the **Value** box, enter the value you want to use. Select **OK** to save the filter settings.
    6. Add additional filters as needed, and select **Finish**.

    You can also use the published data to automatically populate the value of the property from the data output by a previous activity in the workflow. <br>For more information about using filters, see Filter Behavior.
