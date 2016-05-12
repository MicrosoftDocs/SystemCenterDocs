---
title: AdtAdmin.exe Disconnect
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d824084-2a39-485a-966f-9dd28dc76b86
---
# AdtAdmin.exe Disconnect
The *\/Disconnect* parameter disconnects a specified ACS forwarder or group of forwarders from the ACS collector. No output is generated from the *\/Disconnect* parameter. To check an ACS forwarder’s status after using the *\/Disconnect* parameter, use the*\/Connected* subparameter of the *\/Stats* parameter.

## Syntax
`AdtAdmin.exe /Disconnect [/Collector:<CollectorName>] {/Forwarder:<Name> | /ForwarderSid:<SID> | /Group:<GroupName> | /GroupID:<IdentificationNumber> | /Value:<ValueNumber>}`

-   \/Collector:CollectorName \- Specifies an ACS collector you want to disconnect. If this subparameter is omitted, the local ACS collector is assumed.

-   \/Forwarder:Name \-  Specifies an ACS forwarder by its computer name.

-   \/ForwarderID:ForwarderIDNumber \- Specifies an ACS forwarder by its identification number. An identification number is assigned to an ACS forwarder when it first connects to the ACS collector.

-   \/ForwarderSID:SID \- Specifies an ACS forwarder by its computer security identification number.

-   \/Group:GroupName \- Specifies a group of ACS forwarders by the group’s name.

-   \/GroupID: IdentificationNumber \- Specifies a group of ACS forwarders by the group’s identification number. An identification number is assigned to a group when it is first created.

-   \/Value:ValueNumber \- Specifies an ACS forwarder or ACS group by its assigned connection value. The ACS collector prioritizes connections from ACS forwarders using connection values. Connection values range from \-1 through 99. A value of \-1 means the forwarder is part of an ACS group and that the group's value is used to determine the forwarder's priority. A value of 0 means the ACS collector ignores data from that ACS forwarder or group. If event saturation is detected, a collector will disconnect forwarders or a group of forwarders with lower values before disconnecting forwarders with higher values.

## Example
This example disconnects an ACS forwarder named Server1:

`adtadmin /disconnect /forwarder:"Server1"`

## See Also
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe GetDBAuth](AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe GetQuery](AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](AdtAdmin.exe-UpdGroup.md)


