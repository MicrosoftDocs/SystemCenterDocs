---
title: Invoke Runbook
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78020370-0059-4788-9eed-2c1687aaf56e
author:bwren
manager:cfreemanwa
---
# Invoke Runbook
The Invoke Runbook activity launches a runbook that you have specified. You can transfer data to runbooks by configuring an [Initialize Data](../../orch/reference/Initialize-Data.md) activity in the invoked runbook. You can return data from the invoked runbook by configuring a [Return Data](../../orch/reference/Return-Data.md) activity.  
  
You can use the Invoke Runbook activity to invoke generic runbooks that only perform specific actions that do not depend on how the runbook is invoked. For example, you can create a runbook that calls separate runbooks to perform a backup maintenance procedure that in turn calls a runbook to shut down services, another runbook to back up data, and then a final runbook to restart the services.  
  
> [!IMPORTANT]  
> If you modify the folder name or location of a runbook, you must also re\-configure any Invoke Runbook activity that references the modified runbook.  
  
## Configuring the Invoke Runbook activity  
Before you configure the Invoke Runbook activity, you need to know which runbook you are invoking.  
  
Use the following information to configure the Invoke Runbook activity.  
  
### Details  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Runbook**|Click the ellipsis **\(...\)** button to browse for the runbook that you want to invoke. **Important:** Do not invoke a runbook that starts with a Monitor activity.|  
|**Invoke by path**|Select to force the Invoke Runbook activity to invoke the runbook by the specific path and name. When selected, any runbook with the same name in the same folder location is invoked. When unselected, the runbook that is invoked can be moved around the environment and the Invoke Runbook activity automatically maps itself to the new location.|  
|**Wait for completion**|Select to force the Invoke Runbook activity to keep the invoked runbook running until it is completed. **Important:** Do not select **Wait for completion** if any return data in the invoked runbook is also return data in the invoking runbook.|  
|**Parameters**|If you have selected a runbook that contains an [Initialize Data](../../orch/reference/Initialize-Data.md) activity, the list of parameters required to invoke that activity will be displayed. Enter a value for each parameter.|  
|**Runbook Servers**|Type the list of runbook servers that will run this runbook. Separate each name with a semi\-colon **\(;\)**. The order in which the runbook servers are listed will be the order used for failover and load balancing of the runbook. The runbook server names must correspond to the names that are displayed within the runbook server's tree in the Orchestrator Deployment Manager. Leave this field blank to use the runbook or global defaults for the runbook server assignment.|  
  
### Published Data  
The following table lists the published data items from the Invoke Runbook activity.  
  
|Item|Description|  
|--------|---------------|  
|Child runbook Job ID|The job ID of the invoked runbook.|  
|Child runbook status|The status published by the child runbook.|  
  
The Invoke Runbook activity returns any data that the invoked runbook has defined in the Returned Data tab of the runbook properties. The values of these properties must be populated using [Return Data](../../orch/reference/Return-Data.md) activity in that workflow. If the current runbook needs to return data from the invoked runbook, then it must have its own [Return Data](../../orch/reference/Return-Data.md) activity that includes these values.  
  
### Credentials  
If you use the Invoke Runbook activity and you use [Security Credentials](../../orch/manage/Common-Activity-Properties.md#BKMK_SecurityCredentials), the account you use must be a member of the Orchestrator System group to run successfully.  
  
## See Also  
[Initialize Data](../../orch/reference/Initialize-Data.md)  
[Return Data](../../orch/reference/Return-Data.md)  
[Security Credentials](../../orch/manage/Common-Activity-Properties.md#BKMK_SecurityCredentials)  
  
