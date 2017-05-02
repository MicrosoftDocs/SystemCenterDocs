---
title: Get Deployment Status activity
description: Describes the configurable properties for the Get Deployment Status activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ff8803a3-174b-4239-ae68-58e6c1bb1667
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get Deployment Status activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Get Deployment Status activity is used to retrieve the status of an
application, program, task sequence, or software update deployment
assigned to a computer or collection to determine if a software
deployment action has completed.

To deploy an application (using the new Configuration Manager
application model), use the **Deploy Application** activity. To deploy a
task sequence, use the **Deploy Task Sequence** activity. To deploy
software updates in an update group, use the **Deploy Software Update**
activity. To deploy a legacy application, use the **Deploy Program**
activity

## Get Deployment Status properties

- Deployment Type: The type of deployment for which you want to retrieve information. Options are:
    - Application
    - Program
    - Task Sequence
    - Software Update
- Filters: Filters available are dependent on the type of deployment selected. Filters modify the query sent to Configuration Manager so that the data returned to Orchestrator is already limited to desired results. This improves performance over returning all data and filtering at the Orchestrator server.
    
To add new filter criteria:

  1. Click **Add** and select the property on which to filter. 
  2. Select a **Relation** and then enter a value for the filter.
  
    The type of relation value available will depend on the data type of the property selected.

## Get Deployment Status published data

The following values are published in addition to the input values
above:

|Element|Description|
|---|---|
|Connection|Specifies the name of the connection to the Configuration Manager server|
|Result Count|The number of values returned by the query|

The following list describes the Published Data for the available
Deployment Types.

## Program or task sequence
- AdvertisementID                   ID of the advertisement (deployment)
- LastAcceptanceMessageID           Last acceptance status message ID
- LastAcceptanceMessageIDName       Short description of the last acceptance status message
- LastAcceptanceMessageIDSeverity
    - Error: 3221225472
    - Warning: 2147483648
    - Informational: 1073741824
- LastAcceptanceState               Numeric category of the last acceptance status message
- LastAcceptanceStateName           Short description of the acceptance category
- LastAcceptanceStatusTime          Date and time, in Universal Coordinated Time (UTC), when the last acceptance message was generated
- LastExecutionContext              User context (account) under which the program ran
- LastExecutionResult               Last string returned by a status Management Information Format (MIF) file (messages 10007 and 10009) or an error return code (10006)
- LastState                         Numeric category of the last delivery status message
- LastStateName                     Short description of the delivery category, including:
    - Accepted â€“ No Further Status
    - Succeeded
    - Failed
    - Waiting
    - No Status
- LastStatusMessageID               Last delivery status message ID
- LastStatusMessageIDName           Short description of the last delivery status message.
- LastStatusMessageIDSeverity
    - Error: 3221225472
    - Warning: 2147483648
    - Informational: 1073741824
- LastStatusTime                    Date and time, in Universal Coordinated Time (UTC), when the last delivery message was generated
- ResourceID                        Resource ID of the device

## Application

- AppCI                       Application CI
- AppName                     The name of the application
- AppStatusType               App status type
- AssignmentID                ID of the advertisement (deployment)
- AssignmentUniqueID          GUID of the application
- CollectionID                ID of the collection this resource belongs to
- CollectionName              The name of the collection
- ComplianceState             The compliance state for the configuration item.
- DTCI                        The ID of the Deployment Type used in this deployment
- DTModelID                   The ID of the Deployment Type Model
- DTName                      The name of the Deployment Type used for this deployment
- DTResultID                  Deployment Type Result ID
- DeploymentIntent            0 = Required, 1 = Available
- EnforcementState            The enforcement state. Possible values are:
    - Enforcement State Unknown
    - Enforcement Started
    - Enforcement waiting for content
    - Waiting for another installation to complete
    - Waiting for maintenance window before installing
    - Restart required before installing
    - General failure
    - Pending installation
    - Installing update
    - Pending system restart
    - Successfully installed update
    - Failed to install update
    - Downloading update
    - Downloaded update
    - Failed to download update
- ExtendedInfoDescriptionID   Extended information description ID
- ExtendedInfoID              Extended information ID
- IsMachineAssignedToUser     True or False. True if the machine is assigned to a user.
- IsMachineChangesPersisted   True or False. True if the virtual machine changes are persisted.
- IsVM                        True or False. True if this is a virtual machine.
- MachineID                   Resource ID of the device
- MachineName                 Name of the device
- PolicyModelID               Policy model ID
- Revision                    Revision number of the deployment
- StartTime                   Deployment time
- StatusType                  Status type:
    - Success
    - In Progress
    - Unknown
    - Error
- Technology                  The deployment technology type, such as:
    - Windows Installer
    - App-V
    - Script
    - Nokia
- UpdateState                 Update State
- UserName                    User name
- VMHostName                  If the device is a virtual machine, the name of the host for the VM

## Software update

|Element|Description|
|---|---|
|AssignmentID|ID of the advertisement (deployment)|
|AssignmentName|Name of the advertisement (deployment)|
|AssignmentUniqueID|GUID of the application|
|CollectionID|ID of the collection this resource belongs to|
|CollectionName|The name of the collection|
|DeviceName|Name of the device where the update is targeted|
|IsCompliant|True or False|
|IsMachineAssignedToUser|True or False. True if the machine is assigned to a user.|
|IsMachineChangesPersisted|True or False. True if the virtual machine changes are persisted.|
|IsVM|True or False. True if this is a virtual machine.|
|LastComplianceMessageDesc|Last Compliance Message Description|
|LastComplianceMessageID|Last Compliance Message ID|
|LastComplianceMessageTime|Last Compliance Message Time|
|LastEnforcementErrorCode|Last Enforcement Error Code|
|LastEnforcementErrorID |Last Enforcement Error ID|
|LastEnforcementErrorTime|Last Enforcement Error Time|
|LastEnforcementMessageDesc|Last Enforcement Message Description|
|LastEnforcementMessageID|Last Enforcement Message ID|
|LastEnforcementMessageTime|Last Enforcement Message Time|
|Resource ID |Resource ID of the device|
|StatusDescription|Status description|
|StatusEnforcementState|Additional enforcement state for progress and error status (0 for others).|
|StatusErrorCode |Additional error code for error status (0 for others)|
|StatusTime |Status time|
|StatusType |Status type|
|UserID |User ID|
|VMHostName|If the device is a virtual machine, the name of the host for the VM|

## Configuring the Get Deployment Status activity

1.  From the **Activities** pane, drag a **Get Deployment Status**
    activity to the active runbook.
2.  Double-click the **Get Deployment Status** activity icon. The
    **Properties** dialog box opens.
3.  Configuring the **Details** tab:
    1.  In the **Connection** section, click the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Click **OK**.
    2.  In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        click the ellipsis **(â€¦)** button next to the text box to browse
        for a value.

        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.
4.  Click **Finish**.
