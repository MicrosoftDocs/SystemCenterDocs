---
title: Search and Replace Text
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 481ef283-c99f-4379-933a-1db86c3aceb2
---
# Search and Replace Text
The Search and Replace Text activity searches for and replaces text that you specify in a text file.

This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.

## Configuring the Search and Replace Text Activity
Before you configure the Search and Replace Text activity, you need to determine the following:

-   The file name you want to search in.

-   The encoding that the file you want to search in uses.

-   The text you want to search for.

-   The replacement text

Use the following information to configure the Search and Replace Text activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the path and name of the file that you want to read the text from, or click the ellipsis button **\(...\)** and browse for it.|
|**File encoding**|Click the ellipsis button **\(...\)** to open the **File Encoding** dialog box and select the format that the file is encoded in from the **File Encoding** drop\-down list. Verify that you select the correct encoding format: if the file uses a different encoding format, the activity fails.|
|**Search text**|Type the text that you are searching for in the file.|
|**Case sensitive**|Select this option to search only for lines where the case of the words matches the text from the **Search text** field exactly.|
|**Use regular expressions**|Select this option to use regular expressions in your search. [!INCLUDE[crdefault](../Token/crdefault_md.md)][Using Regular Expressions](assetId:///5f8da032-06a9-4ba0-acc1-29144a08dfca).|
|**Replacement text**|Type the text that you want to replace the search text with.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Case sensitive|Indicates whether the Case sensitive check box was checked or not.|
|File encoding|The file encoding format that you selected in the File encoding field.|
|File name|The name of the file that was searched for text.|
|Line number of match|The line number where matching text was found.|
|Modified line|The entire line of text as it was written after the replace operations occurred.|
|Number of lines matched|The number of lines where matching text was found.|
|Number of matches|The number of matching items that were found.|
|Original line|The entire line of text as it was written before the replace operation occurred.|
|Replace text|The text that was used to replace the search text.|
|Search text|The search string that was used for the search.|
|Use Regex|Indicates whether the Use regular expressions check box was checked or not.|

