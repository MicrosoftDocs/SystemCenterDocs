---
title: Command Script Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e08852eb-bcf3-497b-9d49-834caafa6910


















---
# Command Script Activity
This activity runs a command\-line script as part of a Windows Workflow Foundation \(WF\) workflow.  
  
## Design\-Time Prerequisites  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **Command Script** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. By default, this is set to **localhost**. \(Read\-only\)|  
|Script Parameters|Parameters|Dictionary \<string,string\>|Yes|Specifies command\-line switches or switch\/value pairs to be passed into the script when it runs.|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Script Server|Target|String|No|Specifies the Domain Name System \(DNS\) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the script to run.|  
  
## Errors and Exceptions  
 The **Command Script** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteScript Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///0814abca-00b9-42dd-bbca-0da5a6f69e18)
