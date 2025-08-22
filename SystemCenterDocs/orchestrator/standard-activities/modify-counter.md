---
title: Modify Counter
description: This article describes the functionality of Modify Counter activity.
ms.custom: UpdateFrequency3, engagement-fy23
<<<<<<< HEAD
ms.date: 04/28/2025
=======
ms.date: 11/01/2024
ms.update-cycle: 1095-days
>>>>>>> fe8b130b12ff3b632c2c07e8e6062c735d2df30c
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: a2c706ca-506b-4d9d-96e6-f17ac48e8fc1
caps.latest.revision: 11
author: jyothisuri
ms.author: jsuri
---
# Modify Counter

This article describes the functionality of Modify Counter activity. The Modify Counter increments and decrements a counter, and resets it to its default value. It also sets it to a value you specify. Wherever you need to update the value of a counter, use the Modify Counter activity to update its value.  

 The current value of a counter is specific for every runbook that uses that counter. The first time a counter is used, the default value that has been specified in the counters configuration will be used. You can only modify the value of counters in a runbook using the Modify Counter activity.  

## Configure the Modify Counter Activity

 Before you configure the Modify Counter activity, you need to determine the following:  

- The counter you're updating.  

- The type of update that will be made.  

Use the following information to configure the Modify Counter activity: 

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Counter**|Select the ellipsis **(...)** to select the **Counter** that you're retrieving.|  
|**Action**|Select how you want the value of the counter to be changed:<br /><br /> **Increment**: add the **Step** value to the value of the counter.<br /><br /> **Decrement**: subtract the **Step** value from the value of the counter.<br /><br /> **Set**: set the value of the counter to the **Step** value.<br /><br /> **Reset**: reset the value of the counter to the default value.|  
|**Value**|The value used by the **Increment**, **Decrement**, or **Set** action.|  

### Published Data

 The following table lists the published data items:  

|Item|Description|  
|----------|-----------------|  
|Counter Value|The value of the counter.|
