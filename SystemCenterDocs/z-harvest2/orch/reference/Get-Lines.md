---
title: Get Lines
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 846ae2cb-ab9c-4d59-b0ca-3f0e82c8cbd6
author:bwren
manager:cfreemanwa
---
# Get Lines
The Get Lines activity gets multiple lines from a text file according to criteria that you specify. You can use the Get Lines activity to get specific lines from any location in a text file.  
  
This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  
  
## Configuring the Get Lines Activity  
Before you configure the Get Lines activity, you need to determine the following:  
  
-   The name of the file you want to get lines from.  
  
-   The encoding type that the file you want to get the lines from uses.  
  
-   The criteria you use to filter the lines.  
  
Use the following information to configure the Get Lines activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**File**|Type the path and name of the file that you want to get the text from, or click the ellipsis button **\(...\)** and browse for it.|  
|**File encoding**|Click the ellipsis button **\(...\)** and select the format that the file is encoded in from the **File encoding** drop\-down list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Lines**|Click **Add** to open the **Add Line** dialog box and create filters for the lines that you want to get from the file:<br /><br />**Name**: Search for lines by their name.<br /><br />**Range**: Search for lines by their range.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|File path|The filename and path of the file that the lines were taken from.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|\#Name\# line text|For each item that you add in the lines list of the dialog, a new published data item is created. This item displays the line text of each item in the Lines list. \#Name\# represents the name that you assigned in the Name field.|  
|\#Name\# line numbers|For each item that you add in the Lines list of the dialog, a new published data item is created. This item displays the line numbers where text was found from each item in the Lines list. \#Name\# represents the name that you assigned in the Name field.|  
|Total Number of Lines in the Ranges Specified|The total number of lines that were found in the ranges that were specified.|  
  
