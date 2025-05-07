---
title: Initialize Data
description: This article describes the functionality of Initialize Data activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 02/28/2025
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1cae147-b286-421d-b344-c73216ea9977
caps.latest.revision: 13
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# Initialize Data

This article describes the functionality of Initialize Data activity. The Initialize Data activity is a starting point for runbooks that require parameters from an Invoke Runbook activity. The Initialize Data activity is invoked by an [Invoke Runbook](invoke-runbook.md) activity. You can use the Initialize Data activity to launch generic runbooks that only perform specific actions. For example, use the Initialize Data activity to specify the files to back up in a runbook that performs backup operations. To return data to the invoking runbook, end the runbook’s workflow with a [Return Data](return-data.md) activity.  

## Configure the Initialize Data activity

 Before you configure the Initialize Data activity, you need to know the parameters that you want to use within your runbook.  

 Use the following information to configure the Initialize Data activity.  

### Published Data

 Each parameter that you've configured is available as published data to the other activities in the runbook while the runbook is running. To pass data back to the invoking runbook, use the [Return Data](return-data.md) activity.  

## Related content

 - [Invoke Runbook](invoke-runbook.md).
 - [Return Data](return-data.md).
