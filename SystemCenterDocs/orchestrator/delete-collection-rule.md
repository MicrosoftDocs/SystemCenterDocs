---
title: Delete Collection Rule Activity
description: Describes the configuration properties for the delete collection rule activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 03/09/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 728e1e07-f776-4080-8ee2-188affb15224
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---

# Delete collection rule activity

The Delete Collection Rule activity is used to redefine the membership
of a collection by removing collection membership rules from the
collection. Membership rules determine the resources that are included
in the collection when it updates.

To use this activity, a collection must already exist, which can be
created by the **Create Collection** activity. Membership rules can be
added to the collection by using the **Add Collection Rule** activity.
To force re-evaluation of the collection’s membership after adding or
removing collection rules, use the **Update Collection Membership**
activity.

## Properties and published data

The following list describes the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Delete collection properties

- Collection: The display name or ID of an existing collection.                       

- Collection Value Type: Specifies whether the value in the Collection property is a collection name or a collection ID. Options are:

  - **ID** (default): the value is a collection ID

  - **Name**: the value is a collection name


- Membership Rule: The name for the rule that is shown in the Configuration Manager console for the collection’s membership rules

- Membership Rule Type: The type of the membership rule to be deleted. Options are:

  - **Direct Rule**: a single user or computer resource

  - **Query Rule**: a WQL query string or a predefined query saved on the Configuration Manager server

  - **Include Collection**: a collection whose members will be included in this collection’s membership

  - **Exclude Collection**: a collection whose members will be excluded in this collection’s membership


## Delete collection published data

The following values are published in addition to the input values
above:
  Connection      Specifies the name of the connection to the Configuration Manager server
  Collection ID   Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).

## To configure the delete collection activity

1.  From the **Activities** pane, drag a **Delete Collection** activity
    to the active runbook.

2.  Double-click the **Delete Collection** activity icon. The
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

4.  For information about the settings on the **General** and **Run
    Behavior** tabs.

5.  Click **Finish**.
