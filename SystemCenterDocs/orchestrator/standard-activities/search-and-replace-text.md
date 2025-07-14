---
title: Search and Replace Text
description: This article describes the functionality of Search and Replace Text Activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 481ef283-c99f-4379-933a-1db86c3aceb2
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Search and Replace Text

The Search and Replace Text activity searches for and replaces text that you specify in a text file.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configure the Search and Replace Text Activity

 Before you configure the Search and Replace Text activity, you need to determine the following:  

- The file name you want to search in.  

- The encoding that the file you want to search in uses.  

- The text you want to search for.  

- The replacement text.

Use the following information to configure the Search and Replace Text activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to read the text from, or select the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Select the ellipsis button **(...)** to open the **File Encoding** dialog and select the format that the file is encoded in from the **File Encoding** dropdown list. Verify that you select the correct encoding format: if the file uses a different encoding format, the activity fails.|  
|**Search text**|Enter the text that you're searching for in the file.|  
|**Case sensitive**|Select this option to search only for lines where the case of the words matches the text from the **Search text** field exactly.|  
|**Use regular expressions**|Select this option to use regular expressions in your search. |  
|**Replacement text**|Enter the text that you want to replace the search text with.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Case sensitive|Indicates whether the Case sensitive checkbox was checked or not.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|File name|The name of the file that was searched for text.|  
|Line number of match|The line number where the matching text was found.|  
|Modified line|The entire line of text as it was written after the replace operations occurred.|  
|Number of lines matched|The number of lines where matching text was found.|  
|Number of matches|The number of matching items that were found.|  
|Original line|The entire line of text as it was written before the replace operation occurred.|  
|Replace text|The text that was used to replace the search text.|  
|Search text|The search string that was used for the search.|  
|Use Regex|Indicates whether the Use regular expressions checkbox was checked or not.|
