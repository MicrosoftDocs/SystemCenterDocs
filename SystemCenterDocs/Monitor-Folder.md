---
title: Monitor Folder
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a88688b-c7dd-4cc7-bda8-cd8ca52fdb05
---
# Monitor Folder
The Monitor Folder activity invokes a runbook when the folder that you specified has changed, or if the files within that folder have been changed. You can monitor the size of log files in a folder. If the files grow too large, the Monitor Folder activity can invoke a runbook that will archive, backup, and then purge the log files to clean up the folder.

## Configuring the Monitor Folder Activity
Before you configure the Monitor Folder activity, you need to determine the following:

-   The folder name you are monitoring.

-   What condition invokes the runbooks.

-   Optionally, you may need to know what file types you want to monitor.

Use the following information to configure the Monitor Folder activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Path**|Type the path to the folder that you are monitoring. You can use the ellipsis **\(...\)** button to browse for the folder.|
|**Include sub\-folders**|Select this option to monitor the files and folders in sub\-folders in the **Folder** that you specified.|
|**File Filters**|Create filters with custom criteria for the files that you want to monitor. Perform the following for each filter that you want to create:<br /><br />1.  Click **Add** to open the **Filter Settings** dialog box.<br />2.  From the **Name** menu list, select the criteria that you want to use. The **Relation** and **Value** menu options present custom options according to the criteria that you select from the **Name** menu items.<br />3.  Select from the **Relation** and **Value** menu items.<br />4.  Click **OK**.|

### Triggers Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Number of files is**|Select this option to invoke the Monitor Folder activity if the number of files is greater than, equal to, or less than the value that you provide. Select the criteria from the drop\-down list and type the value in the field.|
|**Total file size is**|Select this option to invoke the Monitor Folder activity if the total file size of the folder is greater than or less than the value that you provide. Select the criteria from the first drop\-down list, type the value in the field, and select the unit of measure from the last drop\-down list.|

### Authentication Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**User name**|Type the user name required to access the folder if it is on a remote computer.|
|**Password**|Type the password required to access the folder if it is on a remote computer.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Include sub\-folders|Indicates that the **Include sub\-folders** check box was selected.|
|Trigger if number of files changed|Indicates that the **Number of files is** check box was selected.|
|Trigger if total file size changed|Indicates that the **Total file size is** check box was selected.|
|Number of files|The number of files given to evaluate the **Number of files is** option.|
|Number of files relation|The relation that was used to evaluate the **Number of files is** option.|
|Number of files limit||
|Origin Folder|The folder that was monitored.|
|Total file size measure|The unit of measure selected to evaluate the **Total file size is** option.|
|Total file size relation|The relation that was used to evaluate the **Total file size is** option.|
|Total file size limit||
|Total file size number|The number given to evaluate the **Total file size is** option.|
|User name|The user name used to access the folder if it was on a remote computer.|


