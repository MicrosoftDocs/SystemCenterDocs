---
title: Start or Stop Service
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1aedb89-b6c9-44fd-9491-9818f5d1327a
---
# Start or Stop Service
The Start\/Stop Service activity will start, stop, pause, or restart a Windows service. The Start\/Stop Service activity can be used to restart a service that has stopped responding or shut down a service in preparation for a backup. This activity uses a satellite license.

## Configuring the Start\/Stop Service Activity
Before you configure the Start\/Stop Service activity you need to determine the following:

-   The service name

-   The computer where the service is running

-   Parameters that are required to start the service.

    > [!NOTE]
    > This depends on the service you are interacting with; it may not be required.

Use the following information to configure the Start\/Stop Service activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Action**|Select one of the following actions that you want to take on the service:<br /><br />-   **Start service**: Start the service if it is stopped. This action is ignored if the service is already running.<br />-   **Stop service**: Stop a running service. This action is ignored if the service is already stopped.<br />-   **Pause service**: Pause a running service. This action is ignored if the service is already stopped or paused.<br />-   **Restart service**: Stop then start a running service. If the service is already stopped it will only be started.|
|**Computer**|Type the computer where this service is running. Type **localhost** to specify the runbook server where the runbook is being processed. You can also use the ellipsis **\(...\)** button to browse for the computer.|
|**Service**|Type the name of the service. You can also use the ellipsis **\(...\)** button to browse for the service. Browsing is only available if you have specified a valid **Computer**.|
|**Parameters**|Type any parameters that are required to interact with the **Service**.|
|**Action must complete in less than**|Specify the maximum amount of time in which the action must complete. After the time has expired, the Start\/Stop Service activity will timeout and return a failure.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Service display name|The name of the service as it appears in the Windows Services control panel utility.|
|Service real name|The name of the ran file that the service is running.|
|Service status|The current status of the service.|
|Service computer|The name of the computer where the service is located.|
|Control Parameters|The parameters that were passed to the service when it was started, stopped, paused or restarted.|
|Control Time Allowance|The maximum amount of time that was specified to complete the Start, Stop, Pause, or Restart of service action.|
|Control Action|The action that was taken on the service: Start, Stop, Pause, or Restart.|


