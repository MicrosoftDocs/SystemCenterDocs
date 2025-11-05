---
title: Return Data 
description: This article describes the Return Data activity that allows you to return data from the current runbook to a runbook that invoked the runbook.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/05/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 60cdc2df-a0fe-49a8-aebf-ee1e2f9c60b9
caps.latest.revision: 16
author: Jeronika-MS
ms.author: v-gajeronika
---
# Return Data

The Return Data activity allows you to return data from the current runbook to a runbook that invoked the runbook. You configure the runbook data by configuring the data parameters in the Runbook Properties dialog.  

## Configure the Return Data activity

Use the following information to configure the Return Data activity.  

1. On the **Test Properties** page, select **Returned Data** > **Add** and enter the desired name.

   :::image type="content" source="./media/return-data/test-properties.png" alt-text="Screenshot of test properties page.":::

2. On the **Return Data Properties** page, under **Details**, right-click the added return data to subscribe to published date or variable.

   :::image type="content" source="./media/return-data/return-data-properties.png" alt-text="Screenshot of return data properties page.":::

### Published Data

 The available published data items depend on the defined data elements.  

## Related content

- [Invoke Runbook](invoke-runbook.md).
- [Initialize Data](initialize-data.md).
