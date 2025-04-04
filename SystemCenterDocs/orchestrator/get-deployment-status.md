---
title: Get Deployment Status activity.
description: Describes the configurable properties for the Get Deployment Status activity for Configuration Manager Integration Pack.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 04/03/2025
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff8803a3-174b-4239-ae68-58e6c1bb1667
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Get Deployment Status activity for Configuration Manager Integration Pack

The Get Deployment Status activity is used to retrieve the status of an
application, program, task sequence, or software update deployment
assigned to a computer or collection to determine if a software
deployment action has completed.

To deploy an application (using the new Configuration Manager
application model), use the **Deploy Application** activity. To deploy a
task sequence, use the **Deploy Task Sequence** activity. To deploy
software updates in an update group, use the **Deploy Software Update**
activity. To deploy a legacy application, use the **Deploy Program**
activity.

## Get Deployment Status properties

The Get Deployment Status properties are as follows:

- Deployment Type: The type of deployment for which you want to retrieve information.
The options are:
    - Application
    - Program
    - Task Sequence
    - Software Update
- Filters: Filters available are dependent on the type of deployment selected. Filters modify the query sent to Configuration Manager so that the data returned to Orchestrator is already limited to desired results. This improves performance over returning all data and filtering at the Orchestrator server.

To add new filter criteria, follow these steps:

1. Select **Add** and select the property on which to filter.
2. Select a **Relation** and then enter a value for the filter.

   The type of relation value available will depend on the data type of the property selected.

## Get Deployment Status published data

The following values are published in addition to the input values above:

|Element|Description|
|---|---|
|Connection|Specifies the name of the connection to the Configuration Manager server. |
|Result Count|The number of values returned by the query. |

The following list describes the Published Data for the available
Deployment types.

## [Program or task sequence](#tab/program-or-task-sequence)

|Element|Description|
|---|---|
|AdvertisementID|ID of the advertisement (deployment). |
|LastAcceptanceMessageID|Last acceptance status message ID. |
|LastAcceptanceMessageIDName|Short description of the last acceptance status message.|
|LastAcceptanceMessageIDSeverity|<ul><li> Error: 3221225472  <li> Warning: 2147483648  <li> Informational: 1073741824 </ul>|
|LastAcceptanceState|Numeric category of the last acceptance status message.|
|LastAcceptanceStateName|Short description of the acceptance category.|
|LastAcceptanceStatus|TimeDate and time, in Universal Coordinated Time (UTC), when the last acceptance message was generated.|
|LastExecutionContext|User context (account) under which the program ran.|
|LastExecutionResult|Last string returned by a status Management Information Format (MIF) file (messages 10007 and 10009) or an error return code (10006).|
|LastState|Numeric category of the last delivery status message.|
|LastStateName|Short description of the delivery category, including: <ul><li> Accepted â€“ No Further Status <li> Succeeded <li> Failed <li> Waiting <li> No Status </ul>|
|LastStatusMessageID|Last delivery status message ID.|
|LastStatusMessageIDName|Short description of the last delivery status message.|
|LastStatusMessageIDSeverity|<ul><li> Error: 3221225472<br>  <li> Warning: 2147483648<br>  <li> Informational: 1073741824 </ul>|
|LastStatusTime|Date and time, in Universal Coordinated Time (UTC), when the last delivery message was generated.|
|ResourceID|Resource ID of the device.|
                      

## [Application](#tab/application)

|Element|Description|
|---|---|
|AppCI|Application CI.|
|AppName|Name of the application.|
|AppStatusType|App status type.|
|Assignment ID|ID of the advertisement (deployment).|
|AssignmentUniqueID|GUID of the application.|
|CollectionID|ID of the collection this resource belongs to.|
|CollectionName|Name of the collection.|
|ComplianceState|Compliance state for the configuration item.|
|DTCI|ID of the Deployment Type used in this deployment.|
|DTModelID|ID of the Deployment Type Model.|
|DTName|Name of the Deployment Type used for this deployment.|
|DTResultID|Deployment Type Result ID.|
|DeploymentIntent|0 = Required, 1 = Available.|
|EnforcementState|Enforcement state. Possible values are: <ul><li> Enforcement State Unknown <li> Enforcement Started <li> Enforcement waiting for content <li> Waiting for another installation to complete <li> Waiting for maintenance window before installing <li> Restart required before installing <li> General failure <li> Pending installation <li> Installing update <li> Pending system restart <li> Successfully installed update <li> Failed to install update <li> Downloading update <li> Downloaded update <li> Failed to download update </ul>|
|ExtendedInfoDescriptionID|Extended information description ID.|
|ExtendedInfoID|Extended information ID.|
|IsMachineAssignedToUser|True or False. True if the machine is assigned to a user.|
|IsMachineChangesPersisted|True or False. True if the virtual machine changes are persisted.|
|IsVM|True or False. True if this is a virtual machine.|
|MachineID|Resource ID of the device.|
|MachineName|Name of the device.|
|PolicyModelID|Policy model ID.|
|Revision|Revision number of the deployment.|
|StartTime|Time of the deployment.|
|StatusType|Status type: <ul><li> Success <li> In Progress <li> Unknown <li> Error </ul>|
|Technology|The deployment technology type, such as: <ul><li> Windows Installer <li> App-V <li> Script <li> Nokia </ul>|
|UpdateState|Status of the update.|
|UserName|Name of the user.|
|VMHostName|If the device is a virtual machine, the name of the host for the VM.|


## [Software update](#tab/software-update)

|Element|Description|
|---|---|
|AssignmentID|ID of the advertisement (deployment).|
|AssignmentName|Name of the advertisement (deployment).|
|AssignmentUniqueID|GUID of the application.|
|CollectionID|ID of the collection this resource belongs to.|
|CollectionName|Name of the collection.|
|DeviceName|Name of the device where the update is targeted.|
|IsCompliant|True or False.|
|IsMachineAssignedToUser|True or False. True if the machine is assigned to a user.|
|IsMachineChangesPersisted|True or False. True if the virtual machine changes are persisted.|
|IsVM|True or False. True if this is a virtual machine.|
|LastComplianceMessageDesc|Last compliance message description.|
|LastComplianceMessageID|Last compliance message ID.|
|LastComplianceMessageTime|Last compliance message time.|
|LastEnforcementErrorCode|Last enforcement error code.|
|LastEnforcementErrorID |Last enforcement error ID.|
|LastEnforcementErrorTime|Last enforcement error time.|
|LastEnforcementMessageDesc|Last enforcement message description.|
|LastEnforcementMessageID|Last enforcement message ID.|
|LastEnforcementMessageTime|Last enforcement message time.|
|Resource ID|Resource ID of the device.|
|StatusDescription|Description of the status.|
|StatusEnforcementState|Additional enforcement state for progress and error status (0 for others).|
|StatusErrorCode|Additional error code for error status (0 for others).|
|StatusTime|Time of the status.|
|StatusType|Type of status.|
|UserID |ID of the user.|
|VMHostName|If the device is a virtual machine, the name of the host for the VM.|

---

## Configure the Get Deployment Status activity

To configure the Get Deployment Status activity, follow these steps:

1. From the **Activities** pane, drag a **Get Deployment Status**
    activity to the active runbook.
2. Double-click the **Get Deployment Status** activity icon. The
    **Properties** dialog opens.
3. Configuring the **Details** tab:
    1. In the **Connection** section, select the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Select **OK**.
    2. In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        select the ellipsis button **(...)** next to the text box to browse
        for a value.

        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.

4. Select **Finish**.
