---
title: Deploy application activity
description: Describes the configurable properties for the Deploy Application activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1197648-35b2-4366-886e-1c93dca4f1cf
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Deploy application activity

Applies To: System Center 2016 - Orchestrator

The Deploy Application activity is used to create new application
deployments and assign them to collections. This activity uses the new
Configuration Manager application model and relies on applications
rather than packages and programs.

To deploy a legacy application (package/program), use the **Deploy
Program** activity. To deploy a task sequence, use the **Deploy Task
Sequence** activity. To deploy software updates in an update group, use
the **Deploy Software Update** activity. To get status on deployments
you’ve created, use the **Get Deployment Status** activity.

## Properties and published data

The following tables list the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Deploy application properties

- Deployment Name: The desired name for the new deployment that will be shown in the Configuration Manager console

- Application: The display name or ID of an existing application.
                             
- Application Value Type: Specifies whether the value in the **Application** property is a name or an application ID. Options are:
                             
  - **ID** (default): the value is an application ID
  - **Name**: the value is an application name

- Collection: The display name or ID of an existing collection.
                             
- Collection Value Type: Specifies whether the value in the **Collection** property is a name or a collection ID. Options are:
                             
  - **ID** (default): the value is a collection ID
                             
  -   **Name**: the value is a collection name             

- Purpose: The deployment intent or purpose. Options are:
  - **Required** (default): the application is mandatory to be installed or uninstalled
                             
  - **Available**: the application is made available but not mandatory
                             

- Action: The action to be performed with the application. Options are:
                             
  - **Install** (default): the application will be installed on the device
  -   **Uninstall**: the application will be uninstalled from the device

- User Notification: Determines how the user sees the application and its notifications. Options are:
  - **Show all notifications** (default): the application is listed in the Software Center and all notifications are displayed to the user.
  - **Show only restart notifications**: the application is not listed in the Software Center, but notifications about a required reboot are displayed to the user.
                             
  - **Hide all notifications**: the application is not listed in the Software Center, and notifications about a required reboot are not displayed to the user.
 
>[!Note] 
> If you set this property to **Hide all notifications** and the Purpose property is set to **Available**, this property will automatically be reset to **Show only restart notifications** because Configuration Manager disallows that setting.

- Distribution Point: The name of a distribution point to where the content for this deployment will be distributed. The name is typically in a UNC format, such as: “\\\\server1.contoso.com”

> [!Note]                             
> If there are no default distribution point groups associated with the collection, and the content is not already distributed, this property or the **Distribution Point Group** property must have a value or the activity will fail.

- Distribution Point Group: The name of a distribution point group to where the content for this deployment will be distributed.
                             
> [!Warning]
> If there are no default distribution point groups associated with the collection, and the content is not already distributed, this property or the **Distribution Point** property must have a value or the activity will fail.

## Deploy application optional properties
  
- Schedule Activity: By default, the deployment is made immediately available. If you wish to define a future date or time to make this deployment available, set date and time manually.

- Installation Deadline: The date/time to use for the installation deadline for this deployment.
                                                          
> [!Note]
> If you set **Purpose** to **Required**, this property defaults to **As soon as possible** unless set to a specific date/time.
                                                          

- Allow Software Install Outside of Maintenance Windows:  True or False (Default = False) Allows the application to install even if the installation would occur outside of a maintenance window

- Allow System Restart Outside of Maintenance Windows:  True or False (Default = False) Allows the advertised program to restart the client even if the restart would occur outside of a maintenance window

- Comment: An optional comment associated with the deployment

- Send Wake-up Packets: True or False (Default = False) Specifies whether the Configuration Manager server will send a Wake On LAN packet to the computer prior to the advertised program.
                                                          
> [!Note]
> This setting applies only if the **Purpose** is set to **Required**.
                                                          

Require administrator approval: True or False (Default = False) Specifies whether the administrator will receive an alert and must approve before the installation occurs.
                                                          
> [!Warning]
> This setting applies only if the **Purpose** is set to **Available** and the collection specified is a user collection.
                                                          

- Use default distribution point groups: True or False (Default = False) If distribution point groups are already associated with this collection, the content associated with this deployment will automatically be distributed to those distribution point groups without having to specify individual distribution points or groups.
  
## Deploy application published data

The following values are published in addition to the input values above:
  
- Connection:  Specifies the name of the connection to the Configuration Manager server
- Collection ID: Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).

## To configure the deploy application activity

1.  From the **Activities** pane, drag a **Deploy Application** activity
    to the active runbook.

2.  Double-click the **Deploy Application** activity icon. The
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

4.  Click **Finish**.


