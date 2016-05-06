---
title: AdtAdmin.exe AddGroup
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9e088a5-a5dc-47ca-9593-5631a7e3e4e7
---
# AdtAdmin.exe AddGroup
The *\/AddGroup* parameter creates a group that is used to organize ACS forwarders. The group does not contain any ACS forwarders when it is created. Use the *\/UpdForwarder* parameter to add ACS forwarders to a group. This command does not generate output. You can use the *\/ListGroups* parameter to verify that the group was created.

## Syntax
`AdtAdmin.exe /AddGroup [/Collector:<CollectorName>] [/Group:<GroupName>]`

|Subparameter|Description|
|----------------|---------------|
|\/Collector:CollectorName|Specifies an ACS collector on which you want to create a group. If this subparameter is omitted, the local ACS collector is assumed.|
|\/Group:GroupName|Specifies the name of the new group. Replace *GroupName* with the name of the new group.|

## Example
Use the following example to create a group called "Accounting Computers":

`adtadmin /addgroup /group:"Accounting Computers"`

## See Also
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe DelGroup](AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetDBAuth](AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe GetQuery](AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](AdtAdmin.exe-UpdGroup.md)


