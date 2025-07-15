---
title: REST activities
description: The following configuration instructions apply to all activities in this integration pack. It lists event notifications.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 8dfe35b3-d3bf-4b34-889d-703b51672ca0
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# REST activities

The following configuration instructions apply to all the activities in this integration pack. Links to this section are included in the configuration instructions for each activity.

## Activity properties

Each activity has a set of required or optional properties that define the configuration of that activity. This includes how it connects to other activities or how the activity performs its actions. You can view or modify activity properties when the activity is placed in the runbook window.

#### Configure the properties for an activity

1.  Double-click the activity. Alternatively, you can right-click the activity, and select **Properties**.

2.  To save your configuration entries, select **Finish**.

In the activity properties dialog, several tabs along the left side provide access to general and specific settings for the activity. The number of available tabs for object properties differs between different activities.

## General tab

This tab contains the **Name** and **Description** properties for the activity. By default, the **Name** of the activity is the same as its activity type, and the **Description** is blank. You can modify these properties to create more descriptive names or provide detailed descriptions of the actions of the activity.

## Properties tab

This tab contains properties that are specific to the activity.

## Run Behavior tab

This tab contains the properties that determine how the activity handles multi-value published data and what notifications will be sent if the activity fails or runs for an excessive period of time.

### Multi-value published data behavior

This doesn't apply to the Invoke REST Service activity.

## Event notifications

Some activities are expected to take a limited amount of time to complete. If they don't complete within that time, they may be stalled or there may be another issue preventing them from completing. You can define the number of seconds to wait for the completion of the action. After this period, a platform event will be sent and the issue will be reported. You can also choose whether to generate a platform event if the activity returns a failure.

#### To be notified when the activity takes longer than a specified time to run or fails to run

1.  In the **Event Notifications** box, enter the **number of seconds** of run time before a notification is generated.

2.  Select **Report if activity fails to run** to generate run failure notifications.

## Published data

Published data is the foundation of a working runbook. It's the data produced as a result of the actions of an activity. This data is published to an internal data bus that's unique for each runbook. Subsequent activities in the runbook can subscribe to this data and use it in their configuration. Link conditions also use this information to add decision-making capabilities to runbooks.

An activity can only subscribe to data from the activities that are linked before it in the runbook. You can use published data to automatically populate the property values needed by activities.

#### Use published data

1.  Right-click the property value box, select **Subscribe**, and select **Published Data**.

2.  Select the **Activity** dropdown box and select the activity from which you want to obtain the data. To view additional data elements common to all runbooks, select **Show Common Published Data**.

3.  Select the published data element that you want to use, and select **OK**.

For a list of data elements published by each activity, see the **Published Data** tables in the activity section. For information about the common published data items, see [Common Published Data](/previous-versions/system-center/system-center-2012-R2/hh403821(v=sc.12)#CommonPublishedData).

## Activities

This integration pack adds the **REST** category to the **Activity** pane in the Runbook Designer. This category contains the following activities:

-   [Invoke REST Service](invoke-rest-service.md)
