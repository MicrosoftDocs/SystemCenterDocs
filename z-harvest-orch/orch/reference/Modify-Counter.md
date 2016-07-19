---
title: Modify Counter
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a2c706ca-506b-4d9d-96e6-f17ac48e8fc1
author:bwren
manager:cfreemanwa
---
# Modify Counter
The Modify Counter increments and decrements a counter, as well as resets it to its default value. It also sets it to a value you specify. Wherever you need to update the value of a counter, use the Modify Counter activity to update its value.  
  
The current value of a counter is specific for every runbook that uses that counter. The first time a counter is used, the default value that has been specified in the counters configuration will be used. You can only modify the value of counters in a runbook using the Modify Counter activity.  
  
## Configuring the Modify Counter Activity  
Before you configure the Modify Counter activity, you need to determine the following:  
  
-   The counter you are updating.  
  
-   The type of update that will be made.  
  
Use the following information to configure the Modify Counter activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Counter**|Click the ellipsis **\(...\)** button to select the **Counter** that you are retrieving.|  
|**Action**|Select how you want the value of the counter to be changed:<br /><br />**Increment**: add the **Step** value to the value of the counter.<br /><br />**Decrement**: subtract the **Step** value from the value of the counter.<br /><br />**Set**: set the value of the counter to the **Step** value.<br /><br />**Reset**: reset the value of the counter to the default value.|  
|**Value**|The value used by the **Increment**, **Decrement**, or **Set** action.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Counter Value|The value of the counter|  
  
