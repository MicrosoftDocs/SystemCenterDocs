---
title: Add Collection Rule Activity
description: This article provides instructions for configuring the Add Collection Rule activity for Configuration Manager Integration Pack.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 60a8bd5f-fde6-4a8a-8470-4462b5331644
author: jyothisuri
ms.author: jsuri
robots: noindex
---

# Add Collection Rule Activity for Configuration Manager Integration Pack

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

For the procedure to configure this object, see [Configuring the add collection rule activity](#configure-the-add-collection-rule-activity).

## Properties and Published Data

The following tables list the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

### Add Collection Rule Properties

You can specify the following rule properties:

- Collection: The display name or ID of an existing collection.
- Collection Value Type: Indicates whether the value in the Collection property is a name or a collection ID.
- Rule Name: The name for the rule that will be shown in the Configuration Manager console for the collection’s membership rules.
- Rule Type: The type of membership rule to be added. Options are:
  * Direct Rule - a single user or computer
  * Query Rule - a SQL query string or a predefined query saved on a Configuration Manager server.
  * Include Collection - a collection whose members will be included.
  * Exclude Collection - a collection whose members will be excluded.
- Rule Definition: The allowed values for a rule are determined by the type of rule.
  * Direct rules can specify a user or device ID. Device IDs can be the NetBios name or the IP address. The username can be the name displayed in the Configuration Manager console (that is, *contoso\Admin (Administrator)* ), or the UniqueUserName value specified in the SMS_R_User class in WMI (that is, *contoso\admin*)
  * Query Rule – a valid WQL query string or the Query ID of an existing Configuration Manager Query
  * Include Collection – the name or Collection ID of a collection of the same type (user or device) as the collection specified above.
  * Exclude Collection – the name or Collection ID of a collection of the same type (user or device) as the collection specified above.

> [!Note]
> When you use the browse feature to look up a collection name or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.

### Add Collection Rule Published Data

  |**Element**| **Description**|
  |------------|-----------------|
  |Connection| Specifies the name of the connection to the Configuration Manager server.|
  |Collection ID| Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).|

## Configure the Add Collection Rule Activity

To configure the Add Collection Rule activity:

1. From the **Activities** pane, drag a **Add Collection Rule**
   activity to the active runbook.

2. Double-click the **Add Collection Rule** activity icon. The
   **Properties** dialog opens.

3. Configuring the **Details** tab:

   1. In the **Connection** section, select the ellipsis button
      **(…)**, and then select the Configuration Manager server
      connection that you want to use for this activity. Select **OK**.

   2. In the **Fields** section, enter a value for each of the
      required properties. If the property is Lookup-enabled, you can
      select the ellipsis button **(…)** next to the text box to browse
      for a value.\
      \
      You can also use published data to automatically populate the
      value of the property from the data output by a previous
      activity in the runbook.

4. For information about the settings on the **General** and **Run Behavior** tabs, see [Configuration Manager Activities](configuration-manager-activities.md).

5. Select **Finish**.
