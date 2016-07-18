---
title: AdtAdmin.exe GetQuery
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33a1da40-3be5-4f4f-b867-baea8f2e1728
author:mgoedtel
manager:cfreemanwa
---
# AdtAdmin.exe GetQuery
The *\/GetQuery* parameter lists the Windows Management Instrumentation \(WMI\) Query Language \(WQL\) queries that are currently in use as filters on the ACS collector\(s\). Only the *\/Collector* subparameter applies to the *\/GetQuery* parameter.  
  
> [!NOTE]  
> The *\/SetQuery* parameter applies a WQL filter. For more information about the *\/SetQuery* parameter, see [AdtAdmin.exe \/SetQuery](assetId:///c65438fb-efc4-437f-807b-79414d3abee3).  
  
## Syntax  
`AdtAdmin.exe /GetQuery [/Collector:CollectorName]`  
  
|Subparameter|Definition|  
|----------------|--------------|  
|**\/Collector:***CollectorName*|Specifies a single ACS collector from which to retrieve a list of current WQL queries that are applied as filters.|  
  
## See Also  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
[AdtAdmin.exe AddGroup](../../om/manage/AdtAdmin.exe-AddGroup.md)  
[AdtAdmin.exe DelGroup](../../om/manage/AdtAdmin.exe-DelGroup.md)  
[AdtAdmin.exe Disconnect](../../om/manage/AdtAdmin.exe-Disconnect.md)  
[AdtAdmin.exe GetDBAuth](../../om/manage/AdtAdmin.exe-GetDBAuth.md)  
[AdtAdmin.exe ListForwarders](../../om/manage/AdtAdmin.exe-ListForwarders.md)  
[AdtAdmin.exe ListGroups](../../om/manage/AdtAdmin.exe-ListGroups.md)  
[AdtAdmin.exe SetDBAuth](../../om/manage/AdtAdmin.exe-SetDBAuth.md)  
[AdtAdmin.exe SetQuery](../../om/manage/AdtAdmin.exe-SetQuery.md)  
[AdtAdmin.exe Stats](../../om/manage/AdtAdmin.exe-Stats.md)  
[AdtAdmin.exe UpdForwarder](../../om/manage/AdtAdmin.exe-UpdForwarder.md)  
[AdtAdmin.exe UpdGroup](../../om/manage/AdtAdmin.exe-UpdGroup.md)  
  
