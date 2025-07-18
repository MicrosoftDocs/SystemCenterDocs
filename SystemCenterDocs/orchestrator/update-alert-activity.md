---
title: Update Alert Activity
description: The Update Alert activity updated an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer.
ms.custom: UpdateFrequency3
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: ba537978-bae7-4188-8c49-c380c7fc4adc
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Update Alert Activity

The Update Alert activity updated an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer. This activity can change the information in an alert based on the results from automated diagnostics performed by a runbook.

The following tables list the required properties, optional properties, and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Update Alerts Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Connection | The name of the Netcool/OMNIbus ObjectServer connection. | String   | Yes   |
| Identifier | The name of the alert to update.   | String   | No   |

## Update Alert Optional Properties

This activity has the following optional properties:
- Acknowledged
- Agent
- AlertGroup
- AlertKey
- BSM\_Identity
- Class
- Customer
- EventId
- ExpireTime
- ExtendedAttr
- FirstOccurrence
- Flash
- Grade
- LastOccurrence
- LocalNodeAlias
- LocalPriObj
- LocalRootObj
- LocalSecObj
- Location
- Manager
- NmosCauseType
- NmosDomainName
- NmosEntityId
- NmosEventMap
- NmosManagedStatus
- NmosObjInst
- NmosSerial
- Node
- NodeAlias
- OldRow
- OwnerGID
- OwnerUID
- PhysicalCard
- PhysicalPort
- PhysicalSlot
- Poll
- ProbeSubSecondId
- ProcessReq
- RemoteNodeAlias
- RemotePriObj
- RemoteRootObj
- RemoteSecObj
- ServerName
- ServerSerial
- Service
- Severity
- Summary
- SuppressEscl
- TaskList
- Type
- URL
- X733CorrNotif
- X733EventType
- X733ProbableCause
- X733SpecificProb

## Update Alert Published Data

This activity publishes the following alerts:
- Acknowledged
- Agent
- AlertGroup
- AlertKey
- BSM\_Identity
- Class
- Customer
- EventId
- ExpireTime
- ExtendedAttr
- FirstOccurrence
- FirstOccurrence Local Time
- Flash
- Grade
- Identifier
- InternalLast
- InternalLast Local Time
- LastOccurrence
- LastOccurrence Local Time
- LocalNodeAlias
- LocalPriObj
- LocalRootObj
- LocalSecObj
- Location
- Manager
- NmosCauseType
- NmosDomainName
- NmosEntityId
- NmosEventMap
- NmosManagedStatus
- NmosObjInst
- NmosSerial
- Node
- NodeAlias
- OldRow
- OwnerGID
- OwnerUID
- PhysicalCard
- PhysicalPort
- PhysicalSlot
- Poll
- ProbeSubSecondId
- ProcessReq
- RemoteNodeAlias
- RemotePriObj
- RemoteRootObj
- RemoteSecObj
- Serial
- ServerName
- ServerSerial
- Service
- Severity
- StateChange
- StateChange Local Time
- Summary
- SuppressEscl
- Tally
- TaskList
- Type
- URL
- X733CorrNotif
- x733EventType
- x733ProbableCause
- x733SpecificPro

## Configure the Update Alert Activity

To configure the Update Alert Activity, follow these steps:

1.  From the **Activities** pane, drag an **Update Alert** activity to the active runbook.

2.  Double-click the **Update Alert** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Details** tab as follows:

    1.  In the **Connection** section, select the ellipsis button **(...)**, and then select the IBM Tivoli Netcool/OMNIbus ObjectServer connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is lookup-enabled, you can select the ellipsis (...) button next to the text box to browse for a value.
        To add optional properties, select **Select Fields**. You must enter at least one optional property.

4.  In the **Fields** section, enter a value for each of the required properties and the applicable optional properties. If the property is lookup-enabled, you can browse for a value.

5.  Select **Finish**.
