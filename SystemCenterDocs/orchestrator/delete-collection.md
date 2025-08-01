---
title: Delete Collection Activity
description: This article provides guidance on how to configure the Delete Collection activity for System Center Configuration Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 728e1e07-f776-4080-8ee2-188affb15224
author: jyothisuri
ms.author: jsuri
---

# Delete collection activity for System Center Configuration Manager

The Delete Collection activity is used to remove an existing collection
from a Configuration Manager site and optionally delete the members of
that collection from the Configuration Manager database. You can't
delete a collection that is referenced by another collection (such as
limiting a collection or one used in included/excluded collection
rules).

For the procedure to configure this object, see: [Configuring the Delete Collection Activity](/previous-versions/system-center/packs/hh967528(v=technet.10)#BKMK_ProcDelCol).

## Properties and published data

The following list describes the properties and published data for this
activity. The activity publishes all the data from the required and
optional properties into published data.

## Delete collection properties

- Collection: The display name or ID of an existing collection.

- Collection Value Type: Specifies whether the value in the Collection property is a collection name or a collection ID. Options are:

  - **ID** (default): the value is a collection ID

  - **Name**: the value is a collection name

- Delete members from database: True or False (Default = False). When set to True, deletes all the resources in the collection from the site database.

## Advanced tab properties

By default, the Delete Collection activity won't remove a collection
with the following properties:

- The collection has assigned deployments (including autodeployments)

- The collection is used in any update deployment templates

- The collection has custom client settings assignments

- The collection has custom antimalware settings assignments

- The collection is a property of a query

These defaults act as a safeguard against accidentally deleting
collections that are being actively used. You can override these
defaults by setting the appropriate values to **False**.

- Has assigned deployments (including autodeployments): True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any assigned deployments, including legacy programs, applications, software updates, task sequences, or autodeployments for software updates).
- Is used in any deployment templates: True or False (Default = True) When set to **True**, causes the activity to fail if the collection is the target assigned to a software update deployment template.
- Has custom client settings assignments: True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any custom client configuration settings defined.
- Has antimalware policy assignments: True or False (Default = True) When set to **True**, causes the activity to fail if the collection has any antimalware policies assigned.
- Is used in any queries: True or False (Default = True) When set to **True**, causes the activity to fail if the collection is used as a limiting collection for any saved queries.

## Delete collection published data

The following values are published in addition to the input values
above:

- Connection: Specifies the name of the connection to the Configuration Manager server.
- Collection ID: Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).

## Configure the delete collection activity

1. From the **Activities** pane, drag a **Delete Collection** activity
   to the active runbook.

2. Double-click the **Delete Collection** activity icon. The
   **Properties** dialog opens.

3. Configuring the **Details** tab:

   1. In the **Connection** section, select the ellipsis button
      **(...)**, and then select the Configuration Manager server
      connection that you want to use for this activity. Select **OK**.

   2. In the **Fields** section, enter a value for each of the
      required properties. If the property is Lookup-enabled, you can
      select the ellipsis button **(…)** next to the text box to browse
      for a value.\
      \
      You can also use published data to automatically populate the
      value of the property from the data output by a previous
      activity in the runbook.

4. Configuring the **Advanced** tab:

     - The options in the **Delete Conditions** section represent a check that will be made against the collection to determine if the condition is true.
     - If an option is set to **True** and the condition is true, the
       collection won't be deleted and the activity will fail.
     - To ignore the existence of a specific condition, set that property
       to **False**.

5. Select **Finish**.
