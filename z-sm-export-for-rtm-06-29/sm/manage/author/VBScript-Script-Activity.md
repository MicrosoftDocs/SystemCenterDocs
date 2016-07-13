---
title: VBScript Script Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f382f12-ba04-4b5d-8f5e-bfeb1c21b646
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# VBScript Script Activity
This activity in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] runs a VBScript script as part of a Windows Workflow Foundation \(WF\) workflow.  
  
## Design\-Time Prerequisites  
 The **VBScript Script** activity depends on the following prerequisites at design time:  
  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **VBScript Script** activity uses the input properties that are described in the following table.  
  
|Display Name|Internal Name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow continues to run if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. \(By default, this is set to **localhost**\) \(Read\-only\)|  
|Script Parameters|Parameters|Dictionary \<string,string\>|Yes|Provides the list of the standard switches and any associated values that this script uses when it runs.|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Script Server|Target|String|No|Specifies the Domain Name System \(DNS\) name of the server that runs the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the script to run.|  
  
## Errors and Exceptions  
 The **VBScript Script** activity uses the custom tracking service that is supplied by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteScript Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///0814abca-00b9-42dd-bbca-0da5a6f69e18)