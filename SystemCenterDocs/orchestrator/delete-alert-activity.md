---
title: Delete Alert Activity
description: The Delete Alert activity deletes an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: f36431cf-1c54-4ae3-9aa5-ee41d39c7631
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
---
# Delete Alert Activity

The Delete Alert activity deletes an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer. This can be used to delete an alert that has been replaced by a newer one.

The following tables list the required properties, optional properties, and published data for this activity.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the selected class when the activity is defined.

### Delete Alert Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Identifier | The name of the deleted alert. | String   | No   |

### Delete Alert Optional Properties

No optional properties are provided for this activity.

### Delete Alert Published Data

This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro

## Configure the Delete Alert Activity

To configure the Delete Alert Activity, follow these steps:

1. From the **Activities** pane, select and drag a **Delete Alert** activity to the active runbook.

2. Double-click the **Delete Alert** activity icon. <br>The **Properties** dialog box opens.

3. Configure the settings in the **Details** tab as follows:

    1. In the **Connection** section, select the IBM Tivoli Netcool/OMNIbus ObjectServer connection that you want to use for this activity and select **OK**.
    2. In the **Properties** section, enter the name of the alert in the Identifier box.

4. Select **Finish**.
