---
title: Add AD DS Computer to a Group Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e932318-795f-4b75-bafb-e279fb2682dc


















---
# Add AD DS Computer to a Group Activity
This activity adds a computer to a security group in Active Directory Domain Services \(AD DS\) in System Center 2012 - Service Manager. The computer and the group must belong to the same domain, and all containers in the domain are searched.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
 When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD DS.  
  
## Properties  
 The **Add AD DS Computer to Group** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Computer Domain|ComputerDomain|String|Yes|The fully qualified DNS domain name where the computer is located \(for example, contoso.com\)|  
|Computer Name|FullyQualifiedComputerName|String|Yes|The name of the computer.|  
|Group Name|FullyQualifiedGroupName|String|Yes|The name of the Active Directory Domain Services group.|  
  
 The **Add AD DS Computer to Group** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Description|  
|------------------|-------------------|----------|-----------------|  
|Output|Output|Boolean|The result of the operation: **True** if the addition succeeded, **False** if it failed.|  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteActive Directory Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///45cd915d-cd2d-47fc-b01f-ef78749552bf)
