---
title: AdtAdmin.exe GetQuery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33a1da40-3be5-4f4f-b867-baea8f2e1728
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
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetDBAuth](AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe ListForwarders](AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](AdtAdmin.exe-UpdGroup.md)


