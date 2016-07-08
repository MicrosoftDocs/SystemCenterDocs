---
title: Save State VM Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01819538-2722-49dd-b0a6-0143394acd45


















---
# Save State VM Activity
This activity in System Center 2012 - Service Manager saves the state of a virtual machine and then stops the virtual machine.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
  
-   The Virtual Machine Manager console and Service Manager must be both installed on the same server.  
  
-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active Directory Domain Services \(AD DS\).  
  
## Properties  
 The **Save State VM** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable that is named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. \(Read\-only\)|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization \(PRO\) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. \(The default setting is False.\)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System \(DNS\) name of the server that runs the Service Manager console. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be saved.|  
|VMM Server|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager \(VMM\) server that manages the virtual machines.|  
  
 The **Save State VM** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was saved. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  
  
## Errors and Exceptions  
 The **Save State VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteVirtual Machine Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7b249a87-858f-4f80-9be8-17cfa4533aba)
