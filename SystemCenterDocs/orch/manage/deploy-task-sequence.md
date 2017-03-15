---
title: Deploy Task Sequence activity
description: Describes the configurable properties for the Deploy Task Sequence activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d79a77be-37ae-4831-b7f9-42f2528c589f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Deploy Task Sequence activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Deploy Task Sequence activity creates a new Configuration
Manager Task Sequence Deployment that assigns an existing task sequence
to a collection. This enables you to deploy an operating system and
software applications to one or more destination computers.

To deploy an application (using the new Configuration Manager
application model), use the **Deploy Application** activity. To deploy a
program, use the **Deploy Program** activity. To deploy software updates
in an update group, use the **Deploy Software Update** activity. To get
status on deployments you’ve created, use the **Get Deployment Status**
activity.

## Properties and published data

The following tables list the properties and published data for this
activity.

## Deploy Task Sequence properties
- Deployment Name: The desired name for the new deployment that will be shown in the Configuration Manager console
- Task Sequence: The display name or ID of an existing task sequence.
    >[!NOTE]
    >When you use the browse feature to look up a task sequence name, or enter a task sequence name manually or from published data, you must set the **Task Sequence Value Type** property to **Name** or the activity will fail.
- Task Sequence Value Type: Specifies whether the value in the **Task Sequence** property is a name or a task sequence ID. Options are:
    -   **ID** (default): the value is a task seqence ID
    -   **Name**: the value is a task Sequence name
- Collection: The display name or ID of an existing collection.
    >[!NOTE]
    >When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.
- Collection Value Type: Specifies whether the value in the **Collection** property is a name or a collection ID. Options are:
    -   **ID** (default): the value is a collection ID
    -   **Name**: the value is a collection name
- Purpose: The deployment intent or purpose. Options are:
    -   **Required** (default): the task sequence is mandatory to be installed or uninstalled
    -   **Available**: the task sequence is made available but not mandatory
- Rerun behavior: Specifies whether the task sequence will be rerun on the client computer if it has previously been run before the scheduled mandatory time. Options are:
    -   **Always rerun program** (default): The task sequence will always be rerun on the client when the advertisement is scheduled, even if the task sequence has already been successfully run. This is particularly useful when using recurring advertisements in which the program is routinely updated, as with some virus detection software.
    -   **Never rerun program**: The task sequence will not be rerun on the client if the task sequence has previously been run on the client, even if the task sequence originally failed or the program files have been changed.
    -   **Rerun if failed previous attempt**: The task sequence will be rerun when the advertisement is scheduled only if it failed on the previous run attempt. This is particularly useful when assigning a mandatory advertisement, so that it will rerun according to the assignment schedule if it has not successfully done so.
    -   **Rerun if succeeded on previous attempt**: The task sequence will be rerun only if it has previously run successfully on the client. This is useful when using recurring advertisements in which the program is routinely updated, and in which each update requires the previous update to have been successfully installed.
- Show the Task Sequence Progress: True or False (Default = False) Specifies whether or not users see a progress dialog for the task sequence.
- Content Download: Specifies how the content will be obtained for this task sequence. Options are:
    -   **Download locally when needed** (default): download all of the necessary installation files as needed to complete the task sequence
    -   **Download all content before starting**: download all of the necessary installation files locally before initiating the installation. All of the files will be downloaded and stored in the client cache prior to running the task sequence.

## Deploy Task Sequence optional properties

- Allow running independently of assignments: True or False (Default = False) Specifies whether or not users may run the program independently, regardless of its assignment status
- Allow Software Install Outside of Maintenance Windows: True or False (Default = False) Allows the application to install even if the installation would occur outside of a maintenance window
- Allow System Restart Outside of Maintenance Windows: True or False (Default = False) Allows the advertised program to restart the client even if the restart would occur outside of a maintenance window
- Allow Task Sequence to Run on Internet Clients: True or False (Default = False) Allows the task sequence to run even if the client is connecting via the Internet.
- Allow unprotected distribution point: True or False (Default = False) Specifies whether Configuration Manager will permit a client to use an unprotected distribution point if content is not immediately available on its protected distribution point, or if it forces a client to use the protected local distribution point if it is within the boundaries for that point.
- Available to Boot Media and PXE: True or False (Default = False) Enables the use of an Operating System Deployment Task Sequence that starts from a CD, from USB, or from PXE.
- Comment: An optional comment associated with the deployment
- Send Wake-up Packets : True or False (Default = False) Specifies whether the Configuration Manager server will send a Wake On LAN packet to the computer prior to the advertised program.
    >[!NOTE]
    >This setting applies only if the **Purpose** is set to **Required**.
- Use remote distribution point: True or False (Default = False) When no local distribution point is available, use a remote distribution point.

## Schedule Tab properties
- Schedule when this deployment will become available: True or False (Default = False) By default, the deployment is made immediately available. If you wish to define a future date or time to make this deployment available, then set this property to **True** and set the associated date/time below.
- Deployment Availability Time : The date/time when this deployment will be made available.
    >[!NOTE]
    >If you set **Schedule when this deployment will become available** to **True**, this property is set to the current time unless set otherwise.
- Schedule when this deployment will expire : True or False (Default = False) By default, the deployment does not expire. If you wish to define an expiration, then set this property to **True** and set the associated date/time below.
- Deployment expiration: The date/time to use for the installation deadline for this deployment.
    >[!NOTE]
    >If you set **Schedule when this deployment will expire** to **True**, this property is set to the current time unless set otherwise.
- Mandatory Assignments Options : 
  - **Use the following schedule options**:
    - **None**: Specifies that the operation does not occur.
    - **Weekly**: Specifies that the operation recurs every N weeks. If this option is selected, you must specify the day of the week on which the operation will occur.
    - **Monthly**: Specifies that the operation recurs every N months. If this option is selected, you must specify the day of the month on which the operation will occur.
    - **Custom interval**: varies depending on the recurrence pattern selected): Specifies the frequency with which the operation will recur. You may set this in terms of minutes, hours, or days.
  - **Assign immediately after this event**: Enables the selector for event-based assignment. Options are:
      - **As soon as possible**: Specifies that the program will automatically run as soon as it reaches the client and all program requirements are met. This value is specified by default.
      - **Logon**: Specifies that the program will automatically run the next time a user logs on to the client.
      - **Logoff**: Specifies that the program will automatically run the next time a user logs off the client.

## Alerts Tab properties

- Generate Alerts: True or False (Default = False) When set to **True**, an alert definition will be created for the deployment according to the settings below. When set to **False**, alert settings in this group are ignored.
- When Compliance % Below: When compliance with this deployment is below this percentage, an alert will be generated in Configuration Manager. Valid values: 1 - 99
- After Date and Time: Alerts will be generated only after this period of time has elapsed from the deployment’s installation deadline time.
- Also Generate a System Center Operations Manager Alert: True or False (Default = False).
    >[!NOTE]
    >Requires Operations Manager connection with Configuration Manager

## Deploy Task Sequence published data

The following values are published in addition to the input values
above:

|Element|Description|
|---|---|
|Connection |Specifies the name of the connection to the Configuration Manager server|
|Collection ID|Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).|

## Configuring the Deploy Task Sequence activity

1.  From the **Activities** pane, drag a **Deploy Task Sequence**
    activity to the active runbook.

2.  Double-click the **Deploy Task Sequence** activity icon. The
    **Properties** dialog box opens.

3.  Configuring the **Details** tab:

    1.  In the **Connection** section, click the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Click **OK**.

    2.  In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        click the ellipsis **(…)** button next to the text box to browse
        for a value.

        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.

4.  Configuring the **Schedule** tab:

    The Schedule tab allows you to define when the deployment becomes available or when it expires, as well as mandatory assignment schedules. Mandatory assignment schedules cause Configuration Manager to automatically run the program at a specific time or according to a specific event, such as user Logon/Logoff. The settings on this tab are optional.

    For more information about mandatory assignments, see [*Mandatory Assignment Schedules*](https://technet.microsoft.com/en-us/library/3950dc80-c200-4144-bc83-7c07fe986745#BKMK_Mandatory_Assignment).

    >[!NOTE]
    >When a deployment is set to **Required**, then a mandatory schedule must be defined for the deployment or the activity will fail.

5.  For information about the settings on the **General** and **Run
    Behavior** tabs, see [*Common Configuration Instructions for all
    Activities*](https://technet.microsoft.com/en-us/library/3950dc80-c200-4144-bc83-7c07fe986745#BKMK_CommonCMConfigInstructions).

6.  Click **Finish**.
