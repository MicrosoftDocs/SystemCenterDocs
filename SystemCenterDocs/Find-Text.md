---
title: Find Text
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad3a8753-6f61-466c-9ff9-545bbe08c2c1
---
# Find Text
The Find Text activity finds lines in a text file. Use the Find Text activity to find according to a search string that you specify.

This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.

## Configuring the Find Text Activity
Before you configure the Find Text activity, you need to determine the following:

-   The name of the file that you want to search in.

-   The encoding type of the file you want to search in uses.

-   The text that you want to search for.

Use the following information to configure the Find Text activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the path and name of the file that you want to find the text in, or click the ellipsis button **\(...\)** and browse for it.|
|**File encoding**|Click the ellipsis button **\(...\)** and select the format that the file is encoded in from the File encoding drop\-down list. Verify that you select the correct encoding format: if the file uses a different encoding format, the activity fails.|
|**Search text**|Type the text that you are searching for in the file.|
|**Case sensitive**|Select this option to search only for lines where the case of the words matches the text from the **Search text** field exactly.|
|**Use regular expressions**|Select this option to use regular expressions in your search. For more information on regular expressions, see [Using Regular Expressions](assetId:///5f8da032-06a9-4ba0-acc1-29144a08dfca).|
|**Result**|Select one of the following options for your results:<br /><br />**Only the first line that matches the text will be returned**<br /><br />**All lines that match the text will be returned**|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Case sensitive|Indicates whether the Case sensitive check box was selected.|
|File encoding|The file encoding format that you selected in the File encoding field.|
|File name|The name of the file that was searched for text.|
|Return first line or all lines|Indicates whether the Only the first line that matches the text will be published or All lines that match the text will be published option was selected.|
|Line number of match|The line number where matching text was found.|
|Match end|The character offset position that the match ends on.|
|Match start|The character offset position that the match starts on.|
|Matched text|The text that matched the search string.|
|Number of lines matched|The number of lines where matching text was found.|
|Number of matches|The number of matching items that were found.|
|Original line|The entire line that contains the matching item.|
|Search text|The search string that was used for the search.|
|Use Regex|Indicates whether the Use regular expressions check box was selected.|


