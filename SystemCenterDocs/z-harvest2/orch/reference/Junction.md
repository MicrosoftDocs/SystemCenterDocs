---
title: Junction
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 834609dd-c152-4a8e-8c59-069e5857f365
author:bwren
manager:cfreemanwa
---
# Junction
The Junction activity allows you to wait for multiple branches in a runbook to complete before continuing past the junction. This activity can also publish data again from any branch so that downstream activities past the Junction activity can consume the data. Data from different branches than the one you selected will not be available.  
  
You can choose to propagate no data from any of the branches previous to the Junction activity. When you select an activity, the junction runs once, regardless of the data provided in previous activities. For example, a Monitor File activity waits for files to be added to a folder. When the files are added, two branches in the runbook will copy the file to a new location and at the same time, read the lines of the files and add them to master file. The Junction activity waits for all these to complete and then propagates the data from the Copy File branch and the Delete File activity will delete the original files.  
  
## Configuring the Junction activity  
Before you configure the Junction activity, you need to determine which branch will continue on the runbook you are invoking.  
  
Use the following information to configure the Junction activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Return data from**|Click the ellipsis **\(...\)** button and select the activity whose data you want to publish again to the activities that follow the junction. From the **Select an Activity** dialog box, choose **<None>** to propagate no data to the activities following the junction.|  
  
### Published Data  
The following table lists the data items published by this activity.  
  
|Item|Description|  
|--------|---------------|  
|Selected branch|The activity that was selected to have its data published.|  
  
## See Also  
[Standard Activities](../../orch/reference/Standard-Activities.md)  
  
