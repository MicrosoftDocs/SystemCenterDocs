---
title: Restart System
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc59b069-7bf0-4417-8f8b-d6fac34c8691
---
# Restart System
The Restart System activity will restart a computer on your network. The Restart System activity can either wait for applications to shut down gracefully or you can configure the activity to forcefully shut down any running applications. You also can send a message to notify your users of the reason for the disruption.

Some applications may consume memory and hard disk space and will not relinquish them without restarting the system. The Restart System activity can be used to restart these systems during maintenance windows to maintain service during business hours.

## Configuring the Restart System Activity
Before you configure the Restart System activity, you will need to determine the following:

-   The computer you want to restart.

-   Whether you want to forcefully shut down any running applications.

Use the following information to configure the Restart System activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the computer that you are restarting. You can also use the ellipsis **\( ... \)** button to browse for the computer.|
|**Message**|Type a message that will be displayed to users of the **Computer** before it is shut down.|
|**Wait**|Type the number of seconds after sending the **Message** to the users before the system will be shut down.|
|**Force applications to close**|Select to forcefully shut down any applications that are running when the system is restarted.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer|The computer that was restarted.|
|Message to display|The message that was sent to the computer before restarting.|
|Shutdown delay|The number of seconds of delay between the message being sent and the computer restart.|
|Force open apps to close|Determines whether open applications were forced to shut down when the computer was restarted. This value can be either True or False.|


