---
title: Get Computer IP Status
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22f388d5-ad23-4722-a3f5-25e26893dba8
---
# Get Computer IP Status
The Get Computer\/IP Status activity will send a ping to a remote computer or IP address and wait for a response. If a response is received, then the Get Computer\/IP Status activity will succeed. If a response is not received, the activity will fail.

The Get Computer\/IP Status activity can be used to confirm that a computer is available before performing an action on that computer. You can also use the Get Computer\/IP Status activity to check the availability of a computer as part of the level 1 diagnostic step when performing problem management processes.

## Configuring the Get Computer\/IP Status Activity
Before you configure the Get Computer\/IP Status activity, you need to determine the computer name or IP address of the computer that you are monitoring.

> [!IMPORTANT]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.

Use the following information to configure the Get Computer\/IP Status activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer that you are checking. You can also use the ellipsis **\(...\)** button to browse for the computer.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Computer to ping|The computer that is being monitored.|
|Percentage of packets received|The percentage of packets that were received back from the ping.|

