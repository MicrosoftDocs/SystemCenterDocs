---
title: Create Alert Activity
description: The Create Alert activity is used in a runbook to create a new alert on the IBM Tivoli Netcool/OMNIbus ObjectServer that can be used to create an alert in IBM Tivoli Netcool/OMNIbus ObjectServer that originated from another system monitor product.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f857c6b3-28f5-4de9-8266-8b980e5dc069
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Alert Activity

Applies To: System Center 2016 - Orchestrator

The Create Alert activity is used in a runbook to create a new alert on the IBM Tivoli Netcool/OMNIbus ObjectServer that can be used to create an alert in IBM Tivoli Netcool/OMNIbus ObjectServer that originated from another system monitor product.

The following tables list the required properties, optional properties, and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Create Alert Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Identifier | The name of the alert. | String   | No   |

### Create Alert Optional Properties

This activity provides optional properties that are dependent on the fields defined on the ObjectServer.

### Create Alert Published Data

This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro

## Configuring the Create Alert Activity

The following procedure describes the steps required to configure a Create Alert activity.

#### To configure the Create Alert Activity

1.  From the **Activities** pane, click and drag a **Create Alert** activity to the active runbook.

2.  Double-click the **Create Alert** activity icon. <br>The **Properties** dialog box opens.

3.  Configure the settings in the **Details** tab as follows:

    1.  In the **Connection** section, select the IBM Tivoli Netcool/OMNIbus ObjectServer connection that you want to use for this activity and Click **OK**.
    2.  In the **Properties** section, enter the name of the alert in the Identifier box.
        You can add additional fields to this alert. The IBM Tivoli Netcool/OMNIbus ObjectServer reads this data when creating the alert.

4.  Click **Finish**.
