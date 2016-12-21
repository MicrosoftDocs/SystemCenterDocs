---
title: Update Alert Activity
description: The Update Alert activity updated an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba537978-bae7-4188-8c49-c380c7fc4adc
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Update Alert Activity
=====================

Applies To: System Center 2016 - Orchestrator

The Update Alert activity updated an alert on the IBM Tivoli Netcool/OMNIbus ObjectServer. This activity can change the information in an alert based on results from automated diagnostics performed by a runbook.

The following tables list the required properties, optional properties, and published data for this activity.

The activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Update Alerts Required Properties

| Element   | Description   | Valid Values | Look up |
| Connection | The name of the Netcool/OMNIbus ObjectServer connection. | String   | Yes   |
|:---|:---|:---|:---|
| Identifier | The name of the alert to update.   | String   | No   |

### Update Alert Optional Properties

|   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| This activity has the following optional properties:<br>Acknowledged<br>Agent<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>Flash<br>Grade<br>LastOccurrence<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>Summary<br>SuppressEscl<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>X733EventType<br>X733ProbableCause<br>X733SpecificProb |

### Update Alert Published Data

|   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| This activity publishes the following alerts:<br>Acknowledged<br>Agent<br>AlertGroup<br>AlertKey<br>BSM\_Identity<br>Class<br>Customer<br>EventId<br>ExpireTime<br>ExtendedAttr<br>FirstOccurrence<br>FirstOccurrence Local Time<br>Flash<br>Grade<br>Identifier<br>InternalLast<br>InternalLast Local Time<br>LastOccurrence<br>LastOccurrence Local Time<br>LocalNodeAlias<br>LocalPriObj<br>LocalRootObj<br>LocalSecObj<br>Location<br>Manager<br>NmosCauseType<br>NmosDomainName<br>NmosEntityId<br>NmosEventMap<br>NmosManagedStatus<br>NmosObjInst<br>NmosSerial<br>Node<br>NodeAlias<br>OldRow<br>OwnerGID<br>OwnerUID<br>PhysicalCard<br>PhysicalPort<br>PhysicalSlot<br>Poll<br>ProbeSubSecondId<br>ProcessReq<br>RemoteNodeAlias<br>RemotePriObj<br>RemoteRootObj<br>RemoteSecObj<br>Serial<br>ServerName<br>ServerSerial<br>Service<br>Severity<br>StateChange<br>StateChange Local Time<br>Summary<br>SuppressEscl<br>Tally<br>TaskList<br>Type<br>URL<br>X733CorrNotif<br>x733EventType<br>x733ProbableCause<br>x733SpecificPro |

Configuring the Update Alert Activity
-------------------------------------

The following procedure describes the steps required to configure an Update Alert activity.

#### To configure the Update Alert Activity

1.  From the **Activities** pane, drag an **Update Alert** activity to the active runbook.

2.  Double-click the **Update Alert** activity icon. The **Properties** dialog box opens.

3.  Configure the settings in the **Details** tab as follows:

    1.  In the **Connection** section, click the ellipsis button **(...)**, and then select the IBM Tivoli Netcool/OMNIbus ObjectServer connection that you want to use for this activity. Click **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can click the ellipsis (...) button next to the text box to browse for a value.
        To add optional properties, click **Select Fields**. You must enter at least one optional property.

4.  In the **Fields** section, enter a value for each of the required properties and the applicable optional properties. If the property is lookup-enabled, you can browse for a value.

5.  Click **Finish**.


