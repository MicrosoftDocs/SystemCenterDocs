---
title: "Generate Random Text | Microsoft Docs"
ms.custom: ""
ms.date: "05/13/2016"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: d20f8d7c-c7d7-4e2a-95c3-3c514514733d
caps.latest.revision: 12
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Generate Random Text

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The Generate Random Text activity generates random strings of text.  

## Configuring the Generate Random Text Activity  
 Before you configure the Generate Random Text activity, you need to determine the random text string attributes you want to generate.  

 Use the following information to configure the Generate Random Text activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Text Length**|Type the number of characters that you want the string to include, for example, 45.|  
|**Text Contents**|Select the options for the items that you want the Generate Random Text activity to include in the random text string. In the Minimum Quantity field for each option that you select, type the minimum number of these characters that you want to include in the string. The total of all Minimum Quantity fields must not be more than the number you typed in the Text Length field.<br /><br /> **Lower-Case Characters**<br /><br /> **Upper-Case Characters**<br /><br /> **Numbers**<br /><br /> **Symbols**|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Random text|The string of random text that this activity creates.|  
|Random text length|The length of the text that was generated.|
