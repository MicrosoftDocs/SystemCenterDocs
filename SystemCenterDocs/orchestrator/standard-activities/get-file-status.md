---
title: Get File Status
description: This article describes the functionality of Get File Status activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b61d52ec-e35d-42cf-a0fb-fda815e3195b
caps.latest.revision: 15
author: jyothisuri
ms.author: jsuri
---
# Get File Status

The Get File Status activity verifies that a file exists on the local file system or a network location using a UNC path. You can check that a file is available before copying to another location or before starting any services that depend on the existence of the file. If the file doesn't exist, you can take corrective action using the [Copy File](copy-file.md) activity to copy the file from another location.  

## Configure the Get File Status Activity

 Before you configure the Get File Status activity, you need to determine the file name and path name you're checking.  

 Use the following information to configure the Get File Status activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the name and path of the file that you're checking the status of, or select the ellipsis **(...)** button and browse for it.|  
|**Include sub-folders**|Select this option to copy any files within the sub-folders of the path you've specified that match the filename that you've specified.|  
|**File age**|Select **Is less than** or **Is more than** to specify the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Enter the number of days that you'll use with the **File age** measure.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Date and time the file was created|The local date and time on which the file was created.|  
|UTC date and time the file was created|The UTC date and time on which the file was created.|  
|File age days|The number of days that was provided to evaluate the file age.|  
|Modified date option|The option that was selected to search for files according to a date range.|  
|File exists|Indicates whether the file exists or not.|  
|File name extension|The extension, or file type, of the file.|  
|File folder|The folder that the file was found in.|  
|File name|The name of the file.|  
|File owner|The name of the owner of the file.|  
|File size (bytes)|The size of the file in bytes.|  
|Name and path of the origin file|The file name and path that was provided.|  
|Last accessed date and time|The date and time on which the file was created in localized format.|  
|Last accessed UTC date and time|The date and time on which the file was created in UTC format.|  
|Last modified date and time|The date and time on which the file was created in localized format.|  
|Last modified UTC date and time|The date and time on which the file was created in UTC format.|  
|Include sub-folders|Indicates whether the Include sub-folders checkbox was selected.|  
|File path|The source file name and path.|  
|Encoding type (text files only)|The file encoding format used by the file if the file is a text file.|
