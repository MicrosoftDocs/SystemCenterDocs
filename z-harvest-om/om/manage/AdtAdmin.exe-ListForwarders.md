---
title: AdtAdmin.exe ListForwarders
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fadc16d3-c22b-438e-8804-75f6da5ce5d5
author:mgoedtel
manager:cfreemanwa
---
# AdtAdmin.exe ListForwarders
The *\/ListForwarders* parameter lists the ACS forwarders, along with some statistics on each, that have ever connected to the ACS collector. The data that displays is a subset of the data that displays using the *\/Stats* parameter. If no subparameters are used, all ACS forwarders that have ever connected to the ACS collector are included. If you specify an ACS group, all ACS forwarders that belong to the group are listed.  
  
## Syntax  
`AdtAdmin.exe /ListForwarders [/Collector:<CollectorName>] {/[Forwarder:<Name>] | [/ForwarderSid:<SID>] | } {[/Group:<GroupName>] | [/GroupID:<IdentificationNumber>] | [/Value:<ValueNumber>]}`  
  
|Subparameter|Definition|  
|----------------|--------------|  
|\/Collector:CollectorName|Specifies an ACS collector whose statistics you want to list. If this subparameter is omitted, the local ACS collector is assumed.|  
|\/Forwarder:Name|Specifies an ACS forwarder by its computer name.|  
|\/ForwarderID:ForwarderIDNumber|Specifies an ACS forwarder by its identification number. An identification number is assigned to an ACS forwarder when it first connects to the ACS collector.|  
|\/ForwarderSID:SID|Specifies an ACS forwarder by its computer security identification number.|  
|\/Group:GroupName|Specifies a group of ACS forwarders by the group's name.|  
|\/GroupID: IdentificationNumber|Specifies a group of ACS forwarders by the group's identification number. An identification number is assigned to a group when it is first created.|  
|\/Value:ValueNumber|Specifies an ACS forwarder or ACS group by its assigned connection value. The ACS collector prioritizes connections from ACS forwarders using connection values. Connection values range from \-1 through 99. A value of \-1 means the forwarder is part of an ACS group and that the group's value is used to determine the forwarder's priority. A value of 0 means the ACS collector ignores data from that ACS forwarder or group. If event saturation is detected, a collector will disconnect forwarders or a group of forwarders with lower values before disconnecting forwarders with higher values.|  
  
## Examples  
Use the following example to list all ACS forwarders, along with some statistics on each, that have connected to this ACS collector:  
  
`adtadmin /listforwarders`  
  
Use the following example to list the ACS forwarders, along with some statistics on each, that belong to the ACS group that has a group identification number of 4:  
  
`adtadmin /listforwarders /groupid:4`  
  
> [!NOTE]  
> Use quotation marks if the name contains spaces.  
  
Use the following example to list statistics on an ACS forwarder that has the name PC 101:  
  
`adtadmin /listforwarders /forwarder:"PC 101"`  
  
## See Also  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
[AdtAdmin.exe AddGroup](../../om/manage/AdtAdmin.exe-AddGroup.md)  
[AdtAdmin.exe DelGroup](../../om/manage/AdtAdmin.exe-DelGroup.md)  
[AdtAdmin.exe Disconnect](../../om/manage/AdtAdmin.exe-Disconnect.md)  
[AdtAdmin.exe GetDBAuth](../../om/manage/AdtAdmin.exe-GetDBAuth.md)  
[AdtAdmin.exe GetQuery](../../om/manage/AdtAdmin.exe-GetQuery.md)  
[AdtAdmin.exe ListGroups](../../om/manage/AdtAdmin.exe-ListGroups.md)  
[AdtAdmin.exe SetDBAuth](../../om/manage/AdtAdmin.exe-SetDBAuth.md)  
[AdtAdmin.exe SetQuery](../../om/manage/AdtAdmin.exe-SetQuery.md)  
[AdtAdmin.exe Stats](../../om/manage/AdtAdmin.exe-Stats.md)  
[AdtAdmin.exe UpdForwarder](../../om/manage/AdtAdmin.exe-UpdForwarder.md)  
[AdtAdmin.exe UpdGroup](../../om/manage/AdtAdmin.exe-UpdGroup.md)  
  
