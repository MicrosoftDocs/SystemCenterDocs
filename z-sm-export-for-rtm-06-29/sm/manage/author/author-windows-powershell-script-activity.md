---
title: Windows PowerShell Script Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f888cdcb-2512-4485-a605-ed4af7ce9045
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
# Windows PowerShell Script Activity
This activity in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] runs a [!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] script as part of a Windows Workflow Foundation \(WF\) workflow.  
  
## Design\-Time Prerequisites  
 The **[!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] Script** activity depends upon the following prerequisites at design time:  
  
-   Windows PowerShell 2.0  
  
## Run\-Time Prerequisites  
 Windows PowerShell 2.0  
  
## Properties  
 The **[!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] Script** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Management Group|ManagementGroupName|String|No|Specifies the management group to which the script server belongs. By default, this is set to **localhost**. \(Read\-only\)|  
|Script Parameters|Parameters|Dictionary \<string,string\>|Yes|Specifies the name\/value list of parameters to be passed into the script when it runs.<br /><br /> You can set parameter values to any of the following management pack references:<br /><br /> -   $Target\/…$<br />-   $MPElement\[…\]<br />-   $Data\/…$. $Data references are resolved only at run time in the parameters \(not in the script itself\).<br /><br /> Using one of these references as the only value for a parameter sets that parameter to the XML string that represents the input data item \(from **GetItemXML**\).|  
|Script Body|ScriptBody|String|Yes|Specifies the text of the script itself.|  
|Snap\-ins|SnapIns|String|No|Lists [!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] snap\-ins to preload into the runspace.|  
|Script Server|Target|String|No|Specifies the Domain Name System \(DNS\) name of the server that runs the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the script to run.|  
  
## Errors and Exceptions  
 The **[!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)] Script** activity uses the custom tracking service that is supplied by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 For more information about [!INCLUDE[powshellshortname](../../../sm/manage/author/includes/powshellshortname_md.md)], see [Windows PowerShell](http://go.microsoft.com/fwlink/p/?LinkID=164777).  
  
## See Also  
 [DeleteScript Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///0814abca-00b9-42dd-bbca-0da5a6f69e18)