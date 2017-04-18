---
title: Delete Collection Activity
description: This topic provides guidance on how to configure the Delete Collection activity for System Center 2016 Configuration Manager.
ms.custom: na
ms.date: 03/08/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 728e1e07-f776-4080-8ee2-188affb15224
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Delete collection activity for System Center 2016 Configuration Manager

Applies To: System Center 2016 - Orchestrator

The Delete Collection activity is used to remove an existing collection
from a Configuration Manager site and optionally delete the members of
that collection from the Configuration Manager database. You cannot
delete a collection that is referenced by another collection (such as
limiting a collection or one used in included/excluded collection
rules).

For the procedure to configure this object, see: [*Configuring the
Delete Collection
Activity*](https://technet.microsoft.com/en-us/library/hh967528.aspx#BKMK_ProcDelCol).

## Properties and published data

The following list describes the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Delete collection properties

- Collection: The display name or ID of an existing collection.
                                 
- Collection Value Type: Specifies whether the value in the Collection property is a collection name or a collection ID. Options are:
                                 
  -   **ID** (default): the value is a collection ID
                                 
  -   **Name**: the value is a collection name
                                 

- Delete members from database:   True or False (Default = False). When set to True, deletes all of the resources in the collection from the site database.

## Advanced tab properties

By default, the Delete Collection activity will not remove a collection
with the following properties:

- The collection has assigned deployments (including auto-deployments)

- The collection is used in any update deployment templates

- The collection has custom client settings assignments

- The collection has custom antimalware settings assignments

- The collection is a property of a query

These defaults act as a safeguard against accidentally deleting
collections that are being actively used. You can override these
defaults by setting the appropriate values to **False**.

- Has assigned deployments (including auto-deployments):   True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any assigned deployments, including legacy programs, applications, software updates, task sequences, or auto-deployments for software updates).
- Is used in any deployment templates: True or False (Default = True) When set to **True**, causes the activity to fail if the collection is the target assigned to a software update deployment template
- Has custom client settings assignments: True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any custom client configuration settings defined
- Has antimalware policy assignments: True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any antimalware policies assigned
- Is used in any queries: True or False (Default = True) When set to **True**, causes the activity to fail if the collection is used as a limiting collection for any saved queries

## Delete collection published data

The following values are published in addition to the input values
above:


- Connection:      Specifies the name of the connection to the Configuration Manager server
- Collection ID:   Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).

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

4.  Configuring the **Advanced** tab:

  - The options in the **Delete Conditions** section represent a check that will be made against the collection to determine if the condition is true.
  - If an option is set to **True** and the condition is true, the
    collection will not be deleted and the activity will fail.
  - To ignore the existence of a specific condition, set that property
    to **False**.

5.  Click **Finish**.


