---
title: Deploy Program activity
description: Describes the configurable properties for the Deploy Program activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 62285d61-2831-46bb-8a6b-b0de2b69476d
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---

# Deploy Program activity for Configuration Manager Integration Pack

The Deploy Program activity is used to assign legacy application
deployments (packages and programs) to a Collection. This activity
requires an existing Configuration Manager package and program.

To deploy an application (using the new Configuration Manager
application model), use the **Deploy Application** activity. To deploy a
task sequence, use the **Deploy Task Sequence** activity. To deploy
software updates in an update group, use the **Deploy Software Update**
activity. To get status on deployments you’ve created, use the **Get
Deployment Status** activity.


## Properties and published data

The following tables list the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Deploy Program properties

- Deployment Name: The desired name for the new deployment that will be shown in the Configuration Manager console

- Package: The display name or ID of an existing package.

    >[!NOTE]
    >When you use the browse feature to look up a package name, or enter a package name manually or from published data, you must set the **Package Value Type** property to **Name** or the activity will fail.

- Package Value Type: Specifies whether the value in the **Package** property is a name or an application ID. Options are:
    -   **ID** (default): the value is a package ID
    -   **Name**: the value is a package name

- Collection: The display name or ID of an existing collection.
    >[!NOTE]
    >When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.

- Collection Value Type: Specifies whether the value in the **Collection** property is a name or a collection ID. Options are:
    -   **ID** (default): the value is a collection ID
    -   **Name**: the value is a collection name

- Purpose: The deployment intent or purpose. Options are:
    -   **Required** (default): the application is mandatory to be installed or uninstalled
    -   **Available**: the application is made available but not mandatory
    >[!NOTE]
    >When this property is set to **Required**, a mandatory schedule must be defined on the **Schedule** tab or the activity will fail.

- Rerun behavior: Specifies whether the program will be rerun on the client computer if it has previously been run before the scheduled mandatory time. Options are:
    -   **Always rerun program** (default): The program will always be rerun on the client when the advertisement is scheduled, even if the program has already been successfully run. This is particularly useful when using recurring advertisements in which the program is routinely updated, as with some virus detection software.
    -   **Never rerun program**: The program will not be rerun on the client if the program has previously been run on the client, even if the program originally failed or the program files have been changed.
    -   **Rerun if failed previous attempt**: The program will be rerun when the advertisement is scheduled only if it failed on the previous run attempt. This is particularly useful when assigning a mandatory advertisement, so that it will rerun according to the assignment schedule if it has not successfully done so.
    -   **Rerun if succeeded on previous attempt**: The program will be rerun only if it has previously run successfully on the client. This is useful when using recurring advertisements in which the program is routinely updated, and in which each update requires the previous update to have been successfully installed.

- Distribution Point: The name of a distribution point to where the content for this deployment will be distributed. The name is typically in a UNC format, such as: “\\\\server1.contoso.com”
    >[!NOTE]
    >If there are no default distribution point groups associated with the collection, and the content is not already distributed, this property or the **Distribution Point Group** property must have a value or the activity will fail.

- Distribution Point Group: The name of a distribution point group to where the content for this deployment will be distributed.
    >[!WARNING]
    >If there are no default distribution point groups associated with the collection, and the content is not already distributed, this property or the **Distribution Point** property must have a value or the activity will fail.

- Enable peer caching: True or False (Default = True) Select this option to reduce load on the network by allowing clients to download content from other clients on the network that have already downloaded and cached the content. This option utilizes Windows BranchCache and can be used on computers running Windows Vista SP2 and later.

## Deploy Program optional properties
- Allow running independently of assignments: True or False (Default = False) Specifies whether or not users may run the program independently, regardless of its assignment status
- Allow Software Install Outside of Maintenance Windows: True or False (Default = False) Allows the application to install even if the installation would occur outside of a maintenance window
- Allow System Restart Outside of Maintenance Windows: True or False (Default = False) Allows the advertised program to restart the client even if the restart would occur outside of a maintenance window
- Allow unprotected distribution point: True or False (Default = False) Specifies whether Configuration Manager will permit a client to use an unprotected distribution point if content is not immediately available on its protected distribution point, or if it forces a client to use the protected local distribution point if it is within the boundaries for that point.
- Comment: An optional comment associated with the deployment
- Fast (LAN) boundary deployment option: Specifies how a program is run when the client is connected within a fast (LAN) network boundary. Options are:
    -   **Download content and run locally** (default): the client will download the content from the Distribution Point before attempting to run the program.
    -   **Run program from Distribution Point**: The client will run the program from the Distribution Point without downloading it first.

- Send Wake-up Packets: True or False (Default = False) Specifies whether the Configuration Manager server will send a Wake On LAN packet to the computer prior to the advertised program.
    >[!NOTE]
    >This setting applies only if the **Purpose** is set to **Required**.

- Slow boundary deployment option: Specifies the options available when the client is within a slow or unreliable network boundary. Options are:
    -   **Do not run program** (default): The program will not be run when a client is connected within a slow or unreliable network boundary.
    -   **Download content and run locally**: the client will download the content from the Distribution Point before attempting to run the program.

- Use default distribution point groups: True or False (Default = True) If distribution point groups are already associated with this collection, the content associated with this deployment will automatically be distributed to those distribution point groups without having to specify individual distribution points or groups.

## Schedule Tab properties

- Schedule when this deployment will become available: True or False (Default = False) By default, the deployment is made immediately available. If you wish to define a future date or time to make this deployment available, then set this property to **True** and set the associated date/time below.
- Deployment Availability Time: The date/time when this deployment will be made available.
    >[!NOTE]
    >If you set **Schedule when this deployment will become available** to **True**, this property is set to the current time unless set otherwise.

- Schedule when this deployment will expire: True or False (Default = False) By default, the deployment does not expire. If you wish to define an expiration, then set this property to **True** and set the associated date/time below.
- Deployment expiration: The date/time to use for the installation deadline for this deployment.
    >[!NOTE]
    >If you set **Schedule when this deployment will expire** to **True**, this property is set to the current time unless set otherwise.

- Mandatory Assignments Options:
  - **Use the following schedule options**:
    - **None**: Specifies that the operation does not occur.
    - **Weekly**: Specifies that the operation recurs every N weeks. If this option is selected, you must specify the day of the week on which the operation will occur.
    - **Monthly**: Specifies that the operation recurs every N months. If this option is selected, you must specify the day of the month on which the operation will occur.
    - **Custom interval**: varies depending on the recurrence pattern selected): Specifies the frequency with which the operation will recur. You may set this in terms of minutes, hours, or days.
  - **Assign immediately after this event**: Enables the selector for event-based assignment. Options are:
      - **As soon as possible**: Specifies that the program will automatically run as soon as it reaches the client and all program requirements are met. This value is specified by default.
      - **Logon**: Specifies that the program will automatically run the next time a user logs on to the client.
      - **Logoff**: Specifies that the program will automatically run the next time a user logs off the client.


## Deploy Program published data

The following values are published in addition to the input values
above:

|Element|Description|
|---|---|
|Connection|Specifies the name of the connection to the Configuration Manager server|
|Collection ID|Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property)|

## Configuring the Deploy Program activity

1.  From the **Activities** pane, drag a **Deploy Program** activity to
    the active runbook.

2.  Double-click the **Deploy Program** activity icon. The
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

    The Schedule tab allows you to define when the deployment becomes available or when it expires, as well as mandatory assignment schedules. Mandatory assignment schedules cause Configuration Manager to automatically run the program at a specific time or according to a specific event, such as user Logon/Logoff. The settings on this tab are optional.
    >[!NOTE]
    >When a deployment is set to **Required**, then a mandatory schedule must be defined for the deployment or the activity will fail.

5.  For information about the settings on the **General** and **Run
    Behavior** tabs, see [*Common Configuration Instructions for all
    Activities*](https://technet.microsoft.com/en-us/library/3950dc80-c200-4144-bc83-7c07fe986745#BKMK_CommonCMConfigInstructions).

6.  Click **Finish**.
