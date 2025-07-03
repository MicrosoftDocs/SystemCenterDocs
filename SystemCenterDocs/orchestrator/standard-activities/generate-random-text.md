---
title: Generate Random Text
description: This article describes the functionality of Generate Random Text activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: d20f8d7c-c7d7-4e2a-95c3-3c514514733d
caps.latest.revision: 12
author: jyothisuri
ms.author: jsuri
---
# Generate Random Text

The Generate Random Text activity generates random strings of text.  

## Configure the Generate Random Text Activity

 Before you configure the Generate Random Text activity, you need to determine the random text string attributes you want to generate.  

 Use the following information to configure the Generate Random Text activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Text Length**|Enter the number of characters that you want the string to include; for example, 45.|  
|**Text Contents**|Select the options for the items that you want the Generate Random Text activity to include in the random text string. In the Minimum Quantity field for each option that you select, enter the minimum number of these characters that you want to include in the string. The total of all Minimum Quantity fields must not be more than the number you entered in the Text Length field.<br /><br /> **Lower-Case Characters**<br /><br /> **Upper-Case Characters**<br /><br /> **Numbers**<br /><br /> **Symbols**|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Random text|The string of random text that this activity creates.|  
|Random text length|The length of the text that was generated.|
