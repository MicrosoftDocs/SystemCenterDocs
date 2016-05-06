---
title: AdtAdmin.exe UpdForwarder
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28ef8261-7850-4e1d-839b-d1ee4dfd2ec6
---
# AdtAdmin.exe UpdForwarder
Using the *\/UpdForwarder* parameter, you can change the name and the value of an ACS forwarder and also change the group membership of an ACS forwarder.

## Syntax
`AdtAdmin.exe /UpdForwarder [/Collector:<CollectorName>] {/Forwarder:<Name> | /ForwarderID:<ForwarderIDNumber> | /ForwarderSid:<SID> | /Group:<GroupName> | /GroupID:<IdentificationNumber> | /GroupValue:<ValueNumber> | /Value:<ValueNumber>} {/Name:<NewName> | /Value:<NewValueNumber> /GroupValue:<NewValue>}`

|Subparameter|Definition|
|----------------|--------------|
|\/Collector:CollectorName|Specifies the ACS collector to which the ACS forwarder or forwarders sends audit events. If this subparameter is omitted, the local ACS collector is assumed.|
|\/Forwarder:Name|Specifies an ACS forwarder by its computer name.|
|\/ForwarderID:ForwarderIDNumber|Specifies an ACS forwarder by its identification number. An identification number is assigned to an ACS forwarder when it first connects to the ACS collector.|
|\/ForwarderSID:SID|Specifies an ACS forwarder by its computer security identification number.|
|\/Group:GroupName|Specifies a group of ACS forwarders by the group’s name.|
|\/GroupID: IdentificationNumber|Specifies a group of ACS forwarders by the group’s identification number. An identification number is assigned to a group when it is first created.|
|\/Value:ValueNumber|Specifies an ACS forwarder or ACS group by its assigned connection value. The ACS collector prioritizes connections from ACS forwarders using connection values. Connection values range from \-1 through 99. A value of \-1 means the forwarder is part of an ACS group and that the group's value is used to determine the forwarder's priority. A value of 0 means the ACS collector ignores data from that ACS forwarder or group. If event saturation is detected, a collector will disconnect forwarders or a group of forwarders with lower values before disconnecting forwarders with higher values.|
|\/GroupValue:NewValue|Specifies a new value for a group to which the ACS forwarder belongs.|
|\/Name:NewName|Specifies a new name for the ACS forwarder.|
|\/Value:NewValueNumber|Specifies a new value for the ACS forwarder.|

## Example
In this example, an ACS forwarder identified as Server1 has a current connection value of 5. This connection value is changed to 3:

`adtadmin /updforwarder /forwarder:Server1 /value:5 /value:3`

In this example, an ACS forwarder named "Accounting Computer" is assigned a new configuration value of 99:

`adtadmin /updforwarder /forwarder:"Accounting Computer" /value:99`

In this example, a group that contains the ACS forwarder named "Accounting Computer" is assigned a new configuration value of 2:

`adtadmin /updforwarder /forwarder:"Accounting Computer" /groupvalue:2`

In this example, the connection value of a group, specified by its identification number, is changed to 50:

`adtadmin /updforwarder /forwarderid:1 /value:50`

> [!NOTE]
> An ACS forwarder can be a member of only one group at a time. If the ACS forwarder is already a member of an ACS group, running this command removes the forwarder from that group. All names with spaces must be contained within parentheses.

## See Also
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../Topic/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](../Topic/AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](../Topic/AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](../Topic/AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetDBAuth](../Topic/AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe GetQuery](../Topic/AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](../Topic/AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](../Topic/AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetDBAuth](../Topic/AdtAdmin.exe-SetDBAuth.md)
[AdtAdmin.exe SetQuery](../Topic/AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](../Topic/AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdGroup](../Topic/AdtAdmin.exe-UpdGroup.md)

