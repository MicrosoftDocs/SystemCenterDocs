---
title: Monitor File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78ce48a7-f7a2-4075-acfc-882c8148169d
author:bwren
manager:cfreemanwa
---
# Monitor File
The Monitor File activity invokes a runbook when files that you specify in folders and sub\-folders have changed. You can monitor a file that indicates the completion of a transaction. For example, there are nightly transfers sent to your runbook server, and when the transfer is complete a file with the name "Complete" is written to the folder. This activity can automatically invoke a runbook that processes all the files in the folder when the "Complete" file is created.  
  
## Configuring the Monitor File Activity  
Use the following information to configure the Monitor File activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**In folder**|Type the path to the file that you are monitoring, or use the ellipsis **\(...\)** button to browse for it.|  
|**Include sub\-folders**|Select this option to copy any files within the sub\-folders of the path you have specified that match the filename that you have specified.|  
|**Filters**|Create filters with custom criteria for the files that you want to monitor. Perform the following for each filter that you want to create:<br /><br />1.  Click **Add** to open the **Filter Settings** dialog box.<br />2.  From the **Name** drop\-down list, select the criteria that you want to use. The **Relation** and **Value** menu options present custom options according to the criteria that you select from the **Name** list.<br />3.  Select options from the **Relation** and **Value** items.<br />4.  Click **OK**.|  
  
### Triggers Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Trigger if one of the files was**|Select a condition to invoke the activity if the condition in the monitored file is true.|  
|**Trigger if file properties changed**|Select a condition to invoke the activity if the condition in the monitored file is true.|  
  
### Authentication Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**User name**|Type the user name required to access the folder if it is on a remote computer.|  
|**Password**|Type the password required to access the folder if it is on a remote computer.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Change type|The type of changed that was detected on the file.|  
|Name and path of the file|The name and path of the file that was monitored.|  
|Include sub\-folders|Indicates that the **Include** sub\-folders check box was selected.|  
|Notify if changed|Indicates that the **Changed** check box was selected.|  
|Notify if created|Indicates that the **Created** check box was selected.|  
|Notify if deleted|Indicates that the **Deleted** check box was selected.|  
|Notify if renamed|Indicates that the **Renamed** check box was selected.|  
|Origin Folder|The folder that the monitored file was stored in.|  
|Notify if file attributes changed|Indicates that the **Attributes** check box was selected.|  
|Notify if file creation time changed|Indicates that the **Creation time** check box was selected.|  
|Notify if file last access time changed|Indicates that the **Last access time** check box was selected.|  
|Notify if file last write time changed|Indicates that the **Last write time** check box was selected.|  
|Notify if file security changed|Indicates that the **Security** check box was selected.|  
|User name|The user name used to access the folder if it was on a remote computer.|  
  
