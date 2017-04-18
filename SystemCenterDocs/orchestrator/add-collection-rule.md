---
title: Add Collection Rule Activity
description: This topic provides instructions for configuring the Add Collection Rule activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 03/08/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60a8bd5f-fde6-4a8a-8470-4462b5331644
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Add Collection Rule Activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator


The Add Collection Rule activity is used to define the membership of a
collection by adding collection membership rules to the collection.
Membership rules determine the resources that are included in the
collection when it updates. You can use membership rules to add a
specific resource or a set of resources from a query. The collection
membership can also include or exclude other collections. Membership
rules can add only those resources that are members of the limiting
collection.

The activity allows you to use comma-separated values for direct,
included collection and excluded collection rules to quickly define
multiple collection rules of a single rule type without having to run
the activity multiple times.

To use this activity, a collection must already exist, which can be
created by the **Create Collection** activity. Membership rules can be
removed from the collection by using the **Delete Collection Rule**
activity. To force re-evaluation of the collection’s membership after
adding or removing collection rules, use the **Update Collection
Membership** activity.

For the procedure to configure this object, see: Configuring the Add
Collection Rule Activity

**Properties and Published Data**

The following tables list the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

**Add Collection Rule Properties**

You can specify the following rule properties:

- Collection: The display name or ID of an existing collection.
- Collection Value Type: Indicates whether the value in the Collection property is a name of a collection ID.
- Rule Name: The name for the rule that will be shown in the Configuration Manager console for the collection’s membership rules.
- Rule Type: The type of membership rule to be added. Options are:
  * Direct Rule - a single user or computer
  * Query Rule - a SQL query string or a predefined query saved on a Configuration Manager sever.
  * Include Collection - a collection whose members will be included.
  * Exclude Collection - a collection whose members will be excluded. 
- Rule Definition: The allowed values for a rule are determined by the type of rule.   
  * Direct rules can specify a user or device ID. Device ID's can be the NetBios name or the IP address. The user name can be the name displayed in the Configuration Manager console. User names can be the name displayed in the Configuration Manager console (i.e. “contoso\Admin (Administrator)” ), or the UniqueUserName value specified in the SMS_R_User class in WMI (i.e. “contoso\admin”) 
  * Query Rule – a valid WQL query string or the Query ID of an existing Configuration Manager Query
  * Include Collection – the name or Collection ID of a collection of the same type (user or device) as the collection specified above.
  * Exclude Collection – the name or Collection ID of a collection of the same type (user or device) as the collection specified above.


> [!Note]
> When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.

**Add Collection Rule Published Data**

  **Element**| **Description**|
  ------------|-----------------|
  Connection| Specifies the name of the connection to the Configuration Manager server.|
  Collection ID| Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).|

**Configuring the Add Collection Rule Activity**

**To configure the Add Collection Rule activity**

1.  From the **Activities** pane, drag a **Add Collection Rule**
    activity to the active runbook.

2.  Double-click the **Add Collection Rule** activity icon. The
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

4.  For information about the settings on the **General** and **Run Behavior** tabs, see [Configuration Manager Activities](../orch/manage/configuration-manager-activities.md).

5.  Click **Finish**.


