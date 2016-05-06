---
title: Insert Line
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae2bc14f-7027-484e-95c0-4cad77b8f5ef
---
# Insert Line
The Insert Line activity inserts lines into a text file on a line number that you specify.

This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.

## Configuring the Insert Line Activity
Before you configure the Insert Line File activity, you need to determine the following:

-   The name of the file you want to insert text into.

-   The file encoding type of the file you want to insert text into.

-   The line number location where you want to insert the text.

Use the following information to configure the Insert Line activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the path and name of the file that you want to insert the text into, or click the ellipsis button **\(...\)** and browse for it.|
|**File encoding**|Click the ellipsis button **\(...\)** and select the format that the file is encoded in from the **File encoding** drop\-down list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|
|**Text**|Type the text that you want to insert into the file.|
|**Line number**|Type the line number where the text will be inserted.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|File name|The name of the file that the text was inserted into.|
|File encoding|The file encoding format that you selected in the File encoding field.|
|Line text|The text of the line that was inserted.|
|Line number|The line number that was inserted, if only one line was inserted.|

