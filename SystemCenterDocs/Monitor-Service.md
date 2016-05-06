---
title: Monitor Service
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 274d3f61-125f-4d90-9ab3-33208908534e
---
# Monitor Service
The Monitor Service activity invokes runbooks when a service has been started or stopped. You can use the Monitor Service activity to monitor services on any remote computer. Use the Monitor Service activity to create runbooks that take corrective actions when services unintentionally shut down. For example, if a SQL Server service that hosts critical data stops responding, you can use a Monitor Service activity with a [Start or Stop Service](Start-or-Stop-Service.md) activity to automatically restart the service.

## Configuring the Monitor Service Activity
Before you configure the Monitor Service activity, you need to determine the following:

-   Which computer hosts the service that you are monitoring

-   Which service you want to monitor

-   Whether the runbook will run when the service is started or stopped

Use the following information to configure the Monitor Service activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer where the service that you are monitoring is located. You can also browse for the computer using the ellipsis **\(...\)** button. The runbook server that runs this activity must have the appropriate rights to monitor the services on that computer.|
|**Service**|Type the name of the service that you are monitoring. To open the **Choose a Service** dialog box, click the ellipsis **\(...\)** button.|
|**Service is started**|Select to invoke the Monitor Service activity when the selected service has been started.|
|**Service is stopped or paused**|Select to invoke the Monitor Service activity when the selected service has been stopped or paused.<br /><br />When a service is restarted using the Windows Service Control Manager it is stopped and then started in succession. This will cause the Monitor Service activity to be invoked regardless of whether you have specified to invoke when the **Service is started** or **Service is stopped or paused**.|
|**Restart stopped service**|Select the **Restart stopped service** box to restart a service that has stopped. You can also use the Start\/Stop Service activity instead of selecting this option.|
|**Test frequency**|Select the amount of time to wait between each time that the Monitor Service activity checks the status of the service.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Service display name|The name of the service as it appears in the Windows Services control panel utility.|
|Service real name|The name of the file that the service is running.|
|Service status|The current status of the service.|
|Service computer|The name of the computer where the service is located.|
|Test interval|The number of seconds between each check of the service status.|
|Restart stopped service|Determines whether the service is automatically restarted when it is found to be stopped. This value can be either True or False.|


