---
title: AdtAdmin.exe UpdGroup
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc810932-a0d8-45e2-abad-10d4e8a13312
---
# AdtAdmin.exe UpdGroup
The *\/UpdGroup* parameter renames an existing group. Groups are used in ACS to organize ACS forwarders.

## Syntax
`AdtAdmin.exe /UpdGroup {/Group:<ExistingName> | /GroupID:<IdentificationNumber>} /Name:<NewName>`

|Subparameter|Description|
|----------------|---------------|
|**\/Group**|Specifies an ACS group to rename. You can specify the group using its name or identification number.|
|*ExistingName*|Identifies the ACS group to rename by its group name.|
|*IdentificatonNumber*|Identifies the ACS group to rename by its group identification number.|
|**\/Name:***NewName*|Specifies the new name for the ACS group.|

> [!NOTE]
> A group’s identification number can be obtained using the AdtAdmin *\/ListGroups* command.

## Example
Use the following example to rename the Accounting Computers ACS group to "Desktop Computers":

`AdtAdmin /UpdGroup /Group:"Accounting Computers" /Name:"Desktop Computers"`

## See Also
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](./Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](./AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](./AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](./AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetDBAuth](./AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe GetQuery](./AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](./AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](./AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](./AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](./AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](./AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](./AdtAdmin.exe-UpdForwarder.md)



