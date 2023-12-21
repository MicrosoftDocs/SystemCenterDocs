---
title: Get Host Datastores Activity
description: The Get Host Datastores activity is used in a runbook to retrieve a list of datastores available for a specified host managed by the VMware vSphere server.
ms.custom: UpdateFrequency3
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 260c93bf-de76-438a-92fe-1e3dcff4ed49
author: jyothisuri
ms.author: jsuri
manager: mkluck
monikerRange: '<=sc-orch-2019'
ms.date: 04/27/2023
---

# Get Host Datastores Activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Get Host Datastores activity is used in a runbook to retrieve a list of datastores available for a specified host managed by the VMware vSphere server. This can be used to check capacity of the system when automatically adding a new VM to the managed host.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

## Get Host Datastores Activity Required Properties

| Element | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Host   | The path of the managed host controlled by the VMware vCenter server. | String   | Yes   |


## Get Host Datastores Activity Optional Properties

No optional properties are provided for this activity.

## Get Host Datastores Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Datastore | A list of all available data stores that are connected to the specified host | String   |
| Host   | Identifier of the host   | String   |

## Configuring the Get Host Datastores Activity

The following procedure describes the steps required to configure a Get Host Datastores activity.

### To configure the Get Host Datastores Activity

1.  From the **Activities** pane, drag a **Get Host Datastores** activity to the active runbook.
2.  Double-click the **Get Host Datastores** activity icon. The **Properties** dialog opens.
3.  Configure the settings in the **Properties** tab as follows:
    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.
4.  Select **Finish**.
