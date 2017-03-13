---
title: Create Collection Activity
description: This topic provides guidance on how to configure the Create Collection activity for System Center 2016 Configuration Manager.
ms.custom: na
ms.date: 03/08/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9df3561-cd3d-440c-afce-f47e3d0d933d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Create collection activity for System Center 2016 Configuration Manager

Applies To: System Center 2016 - Orchestrator

The Create Collection activity is used in a runbook to create a new
Configuration Manager user or device collection. Collections are the
primary means of defining targets for Configuration Manager actions such
as application or software update deployments.

Once a collection is created, its membership must be defined by adding
collection membership rules using the **Add Collection Rule** activity.
Membership rules can be removed from the collection by using the
**Delete Collection Rule** activity. To force re-evaluation of the
collection’s membership after adding or removing collection rules, use
the **Update Collection Membership** activity.

## Properties and published data

The following list describes the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Create collection properties

  
- Collection Name: The desired display name of the collection to be created.

- Collection Type: Specifies the type of collection to create. Options are:
                    
  - **Device** (default): the collection will contain device resources
                                   
  - **User**: the collection will contain user resources
                
- Limiting Collection: The display name or ID of an existing collection that will limit the membership of the new collection. 

When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.

- Limiting Collection Value Type:   Specifies whether the value in the Limiting Collection property is a name or a collection ID. Options are:

  - **ID** (default): the value is a collection ID
                                   
  - **Name**: the value is a collection name

- Comment: Optional descriptive text about the collection

- Use Incremental Updates: True or False (Default = True) Incremental updates periodically evaluate new resources and then add resources to this collection without full updates being required.
  
## Create collection published data

- Collection ID:   Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).
- Connection: Specifies the name of the connection to the Configuration Manager server

## To configure the create collection activity

1.  From the **Activities** pane, drag a **Create Collection** activity
    to the active runbook.

2.  Double-click the **Create Collection** activity icon. The
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

## Schedule tab properties

- Update this collection on a schedule:   True or False (Default = False). Set to **True** to update the collection at the specified intervals. Set to **False** to prevent the collection from being updated after it is created.

- Start: Defines a date and timestamp and how the time values are interpreted. Options are:
                                         
  - **Client Local Time** (default): the times specified represent the local time on the client.
  - **UTC**: The times specified are UTC times.
                                         

- Recurrence Pattern: Determines how often the collection should be updated. Options are:

  - **None** (default): The collection is updated only once, at the date and time specified in **Start**.
  - **Weekly**: The collection is updated on the specified day of the week at the interval of the specified number of weeks.
  - **Monthly**: The collection is updated at the interval of the specified number of months on:
    - **Day**: the specified day of the month.
    - **The Last Day of the Month**: 
    - Specified day of the week within the month.
                                         
  - **Custom Interval**: The collection is updated at the interval of the specified number of minutes, hours, or days.
