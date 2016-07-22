---
title: Add AD DS User to Group Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c88c0d5-42ee-444a-a22b-a4d7c4df6636


















---
# Add AD DS User to Group Activity
This activity adds a user to a security group in Active Directory Domain Services \(AD&nbsp;DS\) in System Center 2012 - Service Manager. The user and the group must belong to the same domain, and all the containers in the domain are searched.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
 When you use this activity, make sure that the Service Manager Workflow account has sufficient permissions to modify security groups in AD&nbsp;DS.  
  
## Properties  
 The **Add AD DS User to Group** activity uses the input properties that are listed in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|User Domain|UserDomain|String|Yes|The fully qualified domain name \(FQDN\) of the user.|  
|User Name|UserName|String|Yes|The logon name of the user.|  
|Group Name|FullyQualifiedGroupName|String|Yes|The FQDN of the group.|  
  
 The **Add AD DS User to Group** activity generates the output that is described in the following table.  
  
|Display Name|Internal Name|Type|Description|  
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
