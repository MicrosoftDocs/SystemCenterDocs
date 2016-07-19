---
title: Shutdown VM Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f65413db-6874-416a-9b42-1810cf5c5370


















---
# Shutdown VM Activity
This activity in System Center 2012 - Service Manager shuts down the guest operating system on a virtual machine.  
  
 You can use the **Shutdown VM** activity on a virtual machine on a Windows\-based host \(a Hyper\-V host or a Virtual Server host\) only if virtualization guest services are installed on the virtual machine. For a virtual machine that is deployed on a Hyper\-V host, the virtualization guest service is called Integration Components. For a virtual machine that is deployed on a Virtual Server host, the virtualization guest service is called Virtual Machine Additions.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
  
-   The Virtual Machine Manager console and Service Manager must both be installed on the same server.  
  
-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active Directory Domain Services \(AD DS\).  
  
## Properties  
 The **Shutdown VM** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable that is named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. \(Read\-only\)|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization \(PRO\) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. \(The default setting is False.\)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System \(DNS\) name of the server that runs the Service Manager console. Do not use **Localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the activity to run.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be shut down.|  
|VMMServer|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager \(VMM\) server that manages the virtual machines.|  
  
 The **Shutdown VM** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was shut down. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  
  
## Errors and Exceptions  
 The **Shutdown VM** activity uses the custom tracking service that is supplied by Service Manager to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteVirtual Machine Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7b249a87-858f-4f80-9be8-17cfa4533aba)
