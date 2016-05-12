---
title: Monitor Computer IP
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eee8ce17-c286-41ac-9736-00e96fa78f71
---
# Monitor Computer IP
The Monitor Computer\/IP activity will send a ping to a remote computer or IP address and wait for a response. You can configure the Monitor Computer\/IP activity to invoke your runbook if the computer is either reachable or unreachable. The Monitor Computer\/IP activity can be used to invoke runbooks that will automatically notify administrators when a vital system has become unreachable on the network.

## Configuring the Monitor Computer\/IP Activity
Before you configure the Monitor Computer\/IP activity, you will need to determine the following:

-   The computer you are monitoring.

-   Whether you are waiting for the computer to become reachable or waiting for it become not reachable.

> [!IMPORTANT]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.

Use the following information to configure the Monitor Computer\/IP activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer that you are monitoring. You can also browse for the computer using the ellipsis **\(...\)** button.|
|**The computer is not reachable**|Select to invoke the Monitor Computer\/IP activity when the computer that you are monitoring cannot be reached using a ping.|
|**The computer is reachable**|Select to run the Monitor Computer\/IP activity when the computer that you are monitoring can be reached using a ping.|
|**Test frequency**|Specify the amount of time between each ping to the **Computer**.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer to ping|The computer that is being monitored.|
|Percentage of packets received|The percentage of packets that were received back from the ping.|


