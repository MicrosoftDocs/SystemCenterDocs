---
title: Customize VM Activity
description: The Customize VM activity is used in a runbook to customize a virtual machine using a designated script.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e414a7-8505-432c-9da1-052ab78cdace
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 05/16/2024
---
# Customize VM Activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Customize VM activity is used in a runbook to customize a virtual machine using a designated script. This allows the runbook to perform advanced customization using a pre-made Customization Spec.

The following tables list the required and optional properties and published data for this activity.

The activity publishes all the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

### Customize VM Activity Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Customization Spec | The customization spec that will be used to customize the virtual machine. | String   | No   |
| VM Path   | The path to the virtual machine being customized.   | String   | Yes   |

### Customize VM Activity Optional Properties

No optional properties are provided for this activity.

### Customize VM Activity Published Data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Customization Spec | The customization specification used to customize the virtual machine. | String   |
| VM Path   | The path to the virtual machine that was customized.   | String   |

## Configuring the Customize VM Activity

The following procedure describes the steps required to configure a Customize VM activity.

#### To configure the Customize VM Activity

1.  From the **Activities** pane, drag a **Customize VM** activity to the active runbook.

2.  Double-click the **Customize VM** activity icon. The **Properties** dialog opens.

3.  Configure the settings in the **Properties** tab as follows:

    1.  In the **Configuration** section, select the ellipsis button **(...)**, and then select the VMware vSphere server connection that you want to use for this activity. Select **OK**.
    2.  In the **Properties** section, enter a value for each of the required properties and the applicable optional properties. If the property is Lookup-enabled, you can select the ellipsis **(...)** button next to the text box to browse for a value.
        You can also use published data to automatically populate the value of the property from the data output by a previous activity in the workflow.

4.  Select **Finish**.
