---
title: Invoke Runbook
description: This article describes the Invoke Runbook activity that launches a runbook that you have specified.
ms.custom: UpdateFrequency2, engagement-fy23
ms.date: 03/28/2025
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 78020370-0059-4788-9eed-2c1687aaf56e
caps.latest.revision: 19
author: jyothisuri
ms.author: jsuri
---
# Invoke Runbook

The Invoke Runbook activity launches a runbook that you've specified. You can transfer data to runbooks by configuring an [Initialize Data](initialize-data.md) activity in the invoked runbook. You can return data from the invoked runbook by configuring a [Return Data](return-data.md) activity.

 You can use the Invoke Runbook activity to invoke generic runbooks that only perform specific actions that don't depend on how the runbook is invoked. For example, you can create a runbook that calls separate runbooks to perform a backup maintenance procedure that in turn calls a runbook to shut down services, another runbook to back up data, and then a final runbook to restart the services.  

> [!IMPORTANT]
> If you modify the folder name or location of a runbook, you must also reconfigure any Invoke Runbook activity that references the modified runbook.  

## Configure the Invoke Runbook activity

 Before you configure the Invoke Runbook activity, you need to know which runbook you're invoking.  

### Details  

Use the following information to configure the Invoke Runbook activity.

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Runbook**|Select the ellipsis **(...)** button to browse for the runbook that you want to invoke. **Important:**  Don't invoke a runbook that starts with a Monitor activity.|  
|**Invoke by path**|Select to force the Invoke Runbook activity to invoke the runbook by the specific path and name. When selected, any runbook with the same name in the same folder location is invoked. When unselected, the runbook that is invoked can be moved around the environment and the Invoke Runbook activity automatically maps itself to the new location.|  
|**Wait for completion**|Select to force the Invoke Runbook activity to keep the invoked runbook running until it's completed. **Important:** Don't select **Wait for completion** if any return data in the invoked runbook is also return data in the invoking runbook.|  
|**Parameters**|If you've selected a runbook that contains an [Initialize Data](initialize-data.md) activity, the list of parameters required to invoke that activity will be displayed. Enter a value for each parameter.|  
|**Runbook Servers**|Enter the list of runbook servers that will run this runbook. Separate each name with a semi-colon `(;)`. The order in which the runbook servers are listed will be the order used for failover and load balancing of the runbook. The runbook server names must correspond to the names that are displayed within the runbook server’s tree in the Orchestrator Deployment Manager. Leave this field blank to use the runbook or global defaults for the runbook server assignment.|  

### Published Data

 The following table lists the published data items from the Invoke Runbook activity:  

|Item|Description|  
|----------|-----------------|  
|Child runbook Job ID|The job ID of the invoked runbook.|  
|Child runbook status|The status published by the child runbook.|  

 The Invoke Runbook activity returns any data that the invoked runbook has defined in the Returned Data tab of the runbook properties. The values of these properties must be populated using [Return Data](return-data.md) activity in that workflow. If the current runbook needs to return data from the invoked runbook, then it must have its own [Return Data](return-data.md) activity that includes these values.  

### Credentials

 If you use the Invoke Runbook activity and you use [Security Credentials](../common-activity-properties.md#security-credentials), the account you use must be a member of the Orchestrator System group to run successfully.  

## Related content

- [Initialize Data](initialize-data.md).
- [Return Data](return-data.md).
- [Security Credentials](../common-activity-properties.md#security-credentials).
