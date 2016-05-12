---
title: Get Service Status
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 212191ed-8156-45f1-bb09-0ccda3823d16
---
# Get Service Status
The Get Service Status activity will check the status of a service on any computer. Use the Get Service Status to check the status of service before performing another action. For example, if you have an SQL Server backup runbook that requires that SQL Server is stopped before performing the backup, you can check the status and then stop the service using the [Start or Stop Service](Start-or-Stop-Service.md) activity.

## Configuring the Get Service Status Activity
Before you configure the Get Service Status activity, you need to determine the following:

-   The computer where the service is located

-   The name of the service

Use the following information to configure the Get Service Status activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer where the service that you are checking is located. You can also use the ellipsis **\(...\)** button to browse for the computer. The runbook server that runs this runbook must have the appropriate rights to monitor the services on that computer.|
|**Service**|Type the name of the service that you are checking. You can also browse for the service using the ellipsis **\(...\)** button.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Service display name|The name of the service as it appears in the Windows Services control panel utility.|
|Service real name|The name of the ran file that the service is running.|
|Service status|The current status of the service.|
|Service computer|The name of the computer where the service is located.|


