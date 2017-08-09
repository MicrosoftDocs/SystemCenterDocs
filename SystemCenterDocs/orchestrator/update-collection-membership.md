---
title: Update Collection Membership activity
description: Describes the configurable properties for the Update Collection Membership activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 32836679-a36c-4d97-8bd4-384502d10f21
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---

# Update Collection Membership activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Update Collection Membership activity is used to initiate collection
evaluation. It ensures that the membership of a collection is current
before other activities are performed on the collection or its members.

## Update Collection Membership properties

- Collection: The display name or ID of an existing collection.
    >[!NOTE]
    >When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.
- Collection Value Type: Specifies whether the value in the **Collection** property is a name or a collection ID. Options are:
    -   **ID** (default): the value is a collection ID
    -   **Name**: the value is a collection name
- Wait for Refresh Completion: True or False. If set to **True**, the activity will not complete and move to the next activity in the workflow until Configuration Manager signals that the update has been completed.
- Polling Interval (seconds): Minimum = 5. Specifies the number of seconds between queries to Configuration Manager to determine if the update is complete.

## Update Collection Membership published data

The following values are published in addition to the input values
above:

|Element|Description|
|---|---|
|Connection|Specifies the name of the connection to the Configuration Manager server|
|Collection ID|Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property).|

## Configuring the Update Collection Membership activity

1.  From the **Activities** pane, drag an **Update Collection
    Membership** activity to the active runbook.

2.  Double-click the **Update Collection Membership** activity icon. The
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

4.  Click **Finish**.
