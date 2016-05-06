---
title: AdtAdmin.exe GetDBAuth
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5cec7a1-96ca-4782-b24a-ac822f9afbc4
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
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../Topic/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](../Topic/AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](../Topic/AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](../Topic/AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetQuery](../Topic/AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](../Topic/AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](../Topic/AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](../Topic/AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](../Topic/AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](../Topic/AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](../Topic/AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](../Topic/AdtAdmin.exe-UpdGroup.md)

