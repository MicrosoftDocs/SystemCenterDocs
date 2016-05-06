---
title: End Process
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 349554ed-af74-42fd-b061-bb75e0a3bd0f
---
# End Process
The End Process activity ends processes that are running on the runbook server or on a remote computer. The End Process activity can be used to shut down an application that is not responding. The activity returns **success** if the named process is successfully ended or if the name process is not running. This activity uses a satellite license.

## Configuring the End Process Activity
Before you configure the End Process activity, you need to determine the following:

-   Name or ID of the process

-   Computer on which it is running

Use the following information to configure the End Process activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the computer where this process is running. Enter **localhost** to specify the runbook server where the runbook is being processed. You can also use the ellipsis **\(...\)** button to browse for the computer.|
|**Process**|Type the name or process ID of the process that you are ending. You can also use the ellipsis **\(...\)** button to browse for the process. Browsing is only available if you have specified a valid **Computer**.|
|**End all instances**|Select to end all processes that match the Process that you have specified when multiples are found.|
|**Fail if there is more than one instance**|Select to cause the end process to fail if it finds more than one process matching the name you specified.|
|**Terminate in**|Type the number of seconds to wait for the process to be shut down gracefully before it is shut down forcefully.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Number of instances|The number of processes that matched the **Process** you specified.|
|Process ID|The process ID of each of the processes that matched the **Process** you specified.|

