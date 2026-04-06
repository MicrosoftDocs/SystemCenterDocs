---
title: Compare Values
description: This article compares two text values or two numerical values and then determines whether or not they are equal.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
caps.latest.revision: 12
author: Jeronika-MS
ms.author: v-gajeronika
---
# Compare Values

The Compare Values activity compares two text values or two numerical values and then determines whether or not they're equal. This activity can also be used to test error messages or numbers against known issues and automatically route the runbook to the appropriate activity.  

## Configure the Compare Values Activity

 Before you configure the Compare Values activity, you need to determine what type of values you want to compare.  

 Use the following information to configure the Compare Values activity.  

### General Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Name**|Type a descriptive name for the activity.|  
|**Description**|Type a detailed description of the actions of the activity.|  
|**Type**|Select the **Type** from the dropdown list that matches the server you want to monitor. The options include the following:<br /><br /> -   Compare Strings<br />-   Compare Numeric Values<br /><br /> Configuration instructions for each **Details** tab **Type** are listed in the following tables.|  

### Details Tab Compare Strings

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Test**|Type the first text, select how you want the first to be compared to the second text, and then type the second text. From the dropdown menu, when selecting the **matches the pattern** or **does not match pattern** comparisons, use the wildcards ? and * to specify the pattern.|  
|**Case sensitive test**|Select to cause the comparison to be case sensitive.|  

### Details Tab Compare Numeric Values

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Test that**|Type the first number, select how you want the first to be compared to the second number, and then type the second number.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|String to compare|The first string that was entered for the comparison. This published data is only available when **Compare Strings** is selected on the **General** tab.|  
|String to compare to|The second string that was entered for the comparison. This published data is only available when **Compare Strings** is selected on the **General** tab.|  
|Case sensitive comparison|Determines whether the comparison was case sensitive. This value can be either true or false.|  
|Value to compare|The first value that was entered for the comparison. This published data is only available when **Compare Numeric Values** is selected on the **General** tab.|  
|Value to compare to|The second value that was entered for the comparison. This published data is only available when **Compare Numeric Values** is selected on the **General** tab.|  
|Comparison result|The result of the comparison. This value will be true if the two strings or numeric values match and false otherwise.|
