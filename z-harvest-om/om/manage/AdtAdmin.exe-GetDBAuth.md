---
title: AdtAdmin.exe GetDBAuth
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5cec7a1-96ca-4782-b24a-ac822f9afbc4
author:mgoedtel
manager:cfreemanwa
---
# AdtAdmin.exe GetDBAuth
The *\/GetDBAuth* parameter displays the current authentication method used by the ACS collector to access the ACS database. The two available authentication methods are Windows Authentication and SQL authentication. If SQL authentication is used, the *\/GetDBAuth* parameter displays the name of the user account currently in use by the ACS collector to connect to the ACS database.  
  
## Syntax  
`AdtAdmin.exe /GetDBAuth [/Collector:<CollectorName>]`  
  
|Subparameter|Definition|  
|----------------|--------------|  
|\/Collector:CollectorName|Specifies an ACS collector whose database authentication account you want to display. If this subparameter is omitted, the local ACS collector is assumed.|  
  
## Example  
This example retrieves the authentication method used by the ACS collector to connect to the ACS Database. In the following example, the local ACS collector is assumed:  
  
`AdtAdmin /GetDBAuth`  
  
## See Also  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
[AdtAdmin.exe AddGroup](../../om/manage/AdtAdmin.exe-AddGroup.md)  
[AdtAdmin.exe DelGroup](../../om/manage/AdtAdmin.exe-DelGroup.md)  
[AdtAdmin.exe Disconnect](../../om/manage/AdtAdmin.exe-Disconnect.md)  
[AdtAdmin.exe GetQuery](../../om/manage/AdtAdmin.exe-GetQuery.md)  
[AdtAdmin.exe ListForwarders](../../om/manage/AdtAdmin.exe-ListForwarders.md)  
[AdtAdmin.exe ListGroups](../../om/manage/AdtAdmin.exe-ListGroups.md)  
[AdtAdmin.exe SetDBAuth](../../om/manage/AdtAdmin.exe-SetDBAuth.md)  
[AdtAdmin.exe SetQuery](../../om/manage/AdtAdmin.exe-SetQuery.md)  
[AdtAdmin.exe Stats](../../om/manage/AdtAdmin.exe-Stats.md)  
[AdtAdmin.exe UpdForwarder](../../om/manage/AdtAdmin.exe-UpdForwarder.md)  
[AdtAdmin.exe UpdGroup](../../om/manage/AdtAdmin.exe-UpdGroup.md)  
  
