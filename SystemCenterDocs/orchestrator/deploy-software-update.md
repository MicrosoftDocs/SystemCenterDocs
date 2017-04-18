---
title: Deploy Software Update activity
description: Describes the configurable properties for the Deploy Software Update activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 15/03/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7300764-da0a-40de-ad3e-26ec34c0bf1c
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Deploy Software Update activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Deploy Software Update activity is used in a runbook to create a
Software Deployment (advertisement) to deploy software updates to a
collection of computers. This activity requires that the updates have
been downloaded and that the following items exist on the Configuration
Manager Site:

-   Deployment Template
-   Deployment Package

## Properties and published data

The following tables list the properties and published data for this
activity.

## Deploy Software Update properties

- Deployment Name: The desired name for the new deployment that will be shown in the Configuration Manager console
- Deployment Description: An optional description (comment) for the new deployment
- Deployment Template: The display name or ID of an existing deployment template. The template allows you to pre-define many settings for a deployment without having to manually specify them in the activity.

    This property is optional if you choose instead to manually define the settings by using all of the optional properties.
>[!NOTE]
>When you use the browse feature to look up a template name, or enter a template name manually or from published data, you must set the **Deployment Template Value Type** property to **Name** or the activity will fail.
- Deployment Template Value Type   Specifies whether the value in the **Deployment Template** property is a name or a template ID. Options are:
    -   **ID** (default): the value is a template ID
    -   **Name**: the value is a template name
- Update / Update Group: The display name or ID of an existing software update group or individual software update.
    >[!NOTE]
    >The browse feature will allow you to select a software update group by name. Individual software updates are not shown in the browser.
- Update Value Type: Specifies whether the value in the **Update / Update Group** property is a name or an ID. Options are:
    -  **Update Group Name** (default): the value is an update group name
    -  **Update Group ID**: the value is an ID
    - **Update Name**: the value is the name of an individual update
    - **Update ID**: the value is the CI\_ID of an individual update
- Purpose: The deployment intent or purpose. Options are:
    -   **Required** (default): the application is mandatory to be installed or uninstalled
    -   **Available**: the application is made available but not mandatory

 >[!NOTE]
 >When this property is set to **Required**, a mandatory schedule must be defined on the **Schedule** tab or the activity will fail.
- User Notification: Determines how the end user sees the deployment and its notifications. Options are:
    -   **Show all notifications** (default): The deployment is listed in the Software Center and all notifications are displayed to the user.
    -   **Show only restart notifications**: The deployment is not listed in the Software Center, but notifications about a required reboot are displayed to the user.
    -   **Hide all notifications**: The deployment is not listed in the Software Center, and notifications about a required reboot are not displayed to the user.

 >[!NOTE]
 >If you set this property to **Hide all notifications** and the **Purpose** property is set to **Available**, this property will automatically be reset to **Show only restart notifications** because Configuration Manager disallows that setting.
- Collection: The display name or ID of an existing collection.
>[!NOTE]
>When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to Name or the activity will fail.
- Collection Value Type: Specifies whether the value in the Collection property is a name or a collection ID. Options are:
    -   **ID** (default): the value is a collection ID
    -   **Name**: the value is a collection name

## Deploy Software Update optional properties
- Allow peer client distribution: True or False (Default = True) Select this option to reduce load on the network by allowing clients to download content from other clients on the network that have already downloaded and cached the content. This option utilizes Windows BranchCache and can be used on computers running Windows Vista SP2 and later.
- Allow Software Install Outside of Maintenance Windows: True or False (Default = False) Allows the application to install even if the installation would occur outside of a maintenance window
- Allow System Restart Outside of Maintenance Windows: True or False (Default = False) Allows the advertised program to restart the client even if the restart would occur outside of a maintenance window
- Detail Level: Specified the level of information reported in state messages about the deployment. Options are:
    -   **Normal** (default): returns all state messages related to the deployment
    -   **Minimal**: Returns only enforcement success and critical error messages.
- Send Wake-up Packets: True or False (Default = False) Specifies whether the Configuration Manager server will send a Wake On LAN packet to the computer prior to the advertised program.
    >[!NOTE]
    >This setting applies only if the **Purpose** is set to **Required**.
- Slow boundary deployment option: Specifies the options available when the client is within a slow or unreliable network boundary. Options are:
    -   **Do not run program** (default): The program will not be run when a client is connected within a slow or unreliable network boundary.
    -   **Download content and run locally**: the client will download the content from the Distribution Point before attempting to run the program.
- Allow unprotected distribution point: True or False (Default = False) Specifies whether Configuration Manager will permit a client to use an unprotected distribution point if content is not immediately available on its protected distribution point, or if it forces a client to use the protected local distribution point if it is within the boundaries for that point.
- Suppress Restart on Servers: True or False (Default = False) When set to **True**, prevents the automatic restart of servers after update installation
- Suppress Restart on Workstations: True or False (Default = False) When set to **True**, prevents the automatic restart of workstations after update installation
- Comment: An optional comment associated with the deployment
- Fast (LAN) boundary deployment option: Specifies how a program is run when the client is connected within a fast (LAN) network boundary. Options are:
    -   **Download content and run locally** (default): The client will download the content from the Distribution Point before attempting to run the program
    -   **Run program from Distribution Point**: The client will run the program from the Distribution Point without downloading it first.

## Schedule Tab properties
- Schedule Evaluation – Time Based On: Defines how the time values below are interpreted. Options are:
    -   **Client Local Time** (default): the times specified below represent the local time on the client
    -   **UTC**: The times specified below are UTC times.
- Software available time - Availability: Determines whether the date/time value below is used to specify the availability of the deployment. Options are:
    -   **As soon as possible** (default): The date/time value below is ignored and availability is set to the current date/time.
    -   **Schedule time**: The time specified below is used as the deployment’s availability time.
- Software available time – Specific Time   The specific date/time when the deployment will be made available to clients.
- Installation Deadline – deadline: Determines whether the date/time value below is used to specify the installation deadline of the deployment. Options are:
    -   **As soon as possible** (default): The date/time value below is ignored and the deadline is set to the current date/time.
    -   **Schedule time**: The time specified below is used as the deployment’s deadline time.
- Installation Deadline – Specific Time: The specific date/time of the installation deadline for the deployment.

## Alerts Tab properties
- Generate Alerts: True or False (Default = False) When set to **True**, an alert definition will be created for the deployment according to the settings below. When set to **False**, alert settings in this group are ignored.
- When compliance % is below: When compliance with this deployment is below this percentage, an alert will be generated in Configuration Manager. Valid values: 1 - 99
- Offset from deadline time: Alerts will be generated only after this period of time has elapsed from the deployment’s installation deadline time.
- Disable Operations Manager alerts during installation: True or False (Default = False) When set to **True**, the computer will be put into Maintenance Mode in Operations Manager before installation of the deployment.
    >[!NOTE]
    >Requires Operations Manager connection with Configuration Manager
- Create Operations Manager alerts if installation fails: True or False (Default = False) When set to **True**, if the deployment fails, alerts will be created in Operations Manager.
    >[!NOTE]
    >Requires Operations Manager connection with Configuration Manager

## Deploy Software Update published data

The following values are published in addition to the input values
above:

|Element|Description|
|---|---|
|Connection|Specifies the name of the connection to the Configuration Manager server|
|Collection ID|Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property)|

## Configuring the Deploy Software Update activity

1.  From the **Activities** pane, drag a **Deploy Software Update**
    activity to the active runbook.

2.  Double-click the **Deploy Software Update** activity icon. The
    **Properties** dialog box opens.

3.  Configuring the **Details** tab:

    1.  In the **Connection** section, click the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Click **OK**.

    2.  In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        click the ellipsis **(…)** button next to the text box to browse
        for a value.\
        \
        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.

4.  Configuring the **Schedule** tab:

    The **Schedule** tab allows you to define when the deployment becomes available or when it expires, as well as mandatory assignment schedules. Mandatory assignment schedules cause Configuration Manager to automatically run the program at a specific time or according to a specific event, such as user Logon/Logoff. The settings on this tab are optional.

    >[!NOTE]
    >When a deployment is set to **Required**, then a mandatory schedule must be defined for the deployment or the activity will fail.

1.  Configuring the **Alerts** tab:

    The **Alerts** tab allows you to define compliance and installation alert features for a deployment. The settings on this tab are optional. To configure the settings on this tab, enter the appropriate values as described in the properties list above.

2.  Click **Finish**.
