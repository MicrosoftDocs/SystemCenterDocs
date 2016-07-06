---
title: Move VM Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae90e99f-95b9-451d-b788-892544109420
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
# Move VM Activity
This activity in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] moves a virtual machine from the Virtual Machine Manager \(VMM\) Library to a maintenance host.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
  
-   The Virtual Machine Manager console and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] must both be installed on the same server.  
  
-   Ensure that the Service Manager Workflow account has sufficient permissions to modify security groups in Active Directory Domain Services \(AD DS\).  
  
## Properties  
 The **Move VM** activity uses the input properties in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is True.\)|Determines whether the workflow should continue running if the activity fails.|  
|Has Error|HasError||N\/A|Specifies whether the activity has an error set. \(Read\-only\)|  
|Block LM If Host Busy|BlockLMIfHostBusy|Boolean|No. \(The default setting is False.\)|Blocks retrying a Hyper\-V live migration if the migration failed because the source host or the destination host is already participating in another live migration.|  
|Job Group|JobGroup|Guid \(string\)|No|Specifies an identifier for a series of commands that will run as a set.|  
|Job Variable|JobVariable|String|No|Specifies that job progress is tracked and stored in the variable named by this parameter.|  
|Management Group|ManagementGroup|String|No|Specifies the management group in which this activity will run. Set to **localhost**. \(Read\-only\)|  
|Path|Path|String|No|Specifies the destination of the virtual machine on the maintenance host.|  
|PROTipID|PROTipID|Guid|No|Specifies the ID of the Performance and Resource Optimization \(PRO\) tip that triggered this action. Allows for future auditing of PRO tips.|  
|Run Asynchronously|RunAsynchronously|Boolean|No. \(The default setting is False.\)|Specifies that the job runs asynchronously so that control returns to the command shell immediately.|  
|Script Server|Target|String|Yes|Specifies the Domain Name System \(DNS\) name of the server that runs the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. Do not use **localhost**.|  
|Script Time Limit|TimeoutSeconds|Integer|No. \(The default setting is 300 seconds.\)|Specifies the maximum number of seconds to allow for the activity to run.|  
|Start VM On Target|StartVMOnTarget|Boolean|No. \(The default setting is False.\)|Specifies that a virtual machine starts as soon as it reaches its destination host.|  
|Use Cluster|UseCluster|Boolean|No. \(The default setting is False.\)|Forces the use of Windows Server 2008 Cluster Migration for the transfer of a virtual machine that is in a saved state to a host, even if the cluster supports Hyper\-V live migration.|  
|Use LAN|UseLan|Boolean|No. \(The default setting is False.\)|Forces a transfer over the local area network \(LAN\) even if a faster transfer mechanism, such as a storage area network \(SAN\) transfer, is available.|  
|VM Host|VMHostName|String|Yes|Specifies the name of the maintenance host to which the virtual machine will be moved.|  
|VM ID|VMID|String|Yes|Specifies the unique ID of the virtual machine to be moved.|  
|VMM Server|VMMServer|String|Yes|Specifies the name of the System Center Virtual Machine Manager \(VMM\) server that manages the virtual machines.|  
  
 The **Move VM** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|VM ID|VMID|String|Specifies the unique ID of the virtual machine that was moved. The input **VM ID** and the output **VM ID** are equal unless the activity failed to find a virtual machine with a **VM ID** that matches the input **VM ID**. In that case, the output **VM ID** is set to Null.|  
  
## Errors and Exceptions  
 The **Move VM** activity uses the custom tracking service that is supplied by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] to log errors and exceptions when the activity runs. The activity generates errors or exceptions as appropriate if any of the script properties cannot be resolved.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteVirtual Machine Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7b249a87-858f-4f80-9be8-17cfa4533aba)