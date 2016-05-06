---
title: AdtAdmin.exe Stats
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1dd732b-61ab-4b90-8ae9-6dd18be78ad3
---
# AdtAdmin.exe Stats
The *\/Stats* parameter lists statistical information about ACS forwarders that are connected to the ACS collector. These statistics include identification numbers, SIDs, names, and assigned value numbers. The *\/Stats* parameter is used to verify recently completed configuration changes and to retrieve information that is needed when using other AdtAdmin parameters, such as *\/Disconnect* or *\/Setquery*. All ACS collectors, ACS groups, and ACS forwarders are included in the list unless you specify otherwise. Also, every statistic is listed, by default. If you want only a single statistic, you can specify which statistic that you want to display as part of the command syntax.

## Syntax
After you chose a parameter, you can then choose to list all statistics or you can choose to list a particular statistic. This topic includes a table of the parameters that specify the ACS forwarder or group of ACS forwarders that you want to list and a second table that includes the individual statistic subparameters that you can specify.

The syntax of the AdtAdmin.exe \/Stats parameter is as follows:

`AdtAdmin.exe /Stats [/Collector:<CollectorName>] {/[Forwarder:<Name>] | [/ForwarderSid:<SID>] | [/Value:<ValueNumber>} | {[/Group:<GroupName>] | [/GroupID:<IdentificationNumber>]} [<StatisticParameter>]`

|Subparameter|Definition|
|----------------|--------------|
|\/Collector:CollectorName|Specifies an ACS collector whose statistics you want to list. If this subparameter is omitted, the local ACS collector is assumed.|
|\/Forwarder:Name|Specifies an ACS forwarder by its computer name.|
|\/ForwarderID:ForwarderIDNumber|Specifies an ACS forwarder by its identification number. An identification number is assigned to an ACS forwarder when it first connects to the ACS collector.|
|\/ForwarderSID:SID|Specifies an ACS forwarder by its computer security identification number.|
|\/Group:GroupName|Specifies a group of ACS forwarders by the group’s name.|
|\/GroupID: IdentificationNumber|Specifies a group of ACS forwarders by the group’s identification number. An identification number is assigned to a group when it is first created.|
|\/Value:ValueNumber|Specifies an ACS forwarder or ACS group by its assigned connection value. The ACS collector prioritizes connections from ACS forwarders using connection values. Connection values range from \-1 through 99. A value of \-1 means the forwarder is part of an ACS group and that the group's value is used to determine the forwarder's priority. A value of 0 means the ACS collector ignores data from that ACS forwarder or group. If event saturation is detected, a collector disconnects forwarders or a group of forwarders with lower values before disconnecting forwarders with higher values.|

The following table lists the available statistic parameters. If you do not list a statistic parameter, all statistics display.

|Statistic Parameter|Definition|
|-----------------------|--------------|
|Average event rate|Displays the average number of events per second received from an ACS forwarder or group of forwarders over the current connection.|
|Average time to collector|Displays the average number of milliseconds elapsed from the time an event is generated on an ACS forwarder or group of forwarders to the time the ACS collector receives that event.|
|Connect time|Displays the date and time that an ACS forwarder connected to the ACS collector. This parameter is valid only if the *\/Connected* parameter has a value of 1 \(connected\).|
|Connected|Displays the current connection status of an ACS forwarder or group of forwarders. The value of this parameter is either a 0 \(not connected\) or a 1 \(connected\).|
|Current event rate|Displays the events per second currently being received from an ACS forwarder or group of forwarders.|
|Last action|Displays the date and time of the last transmission from an ACS forwarder.|
|Seconds since connection|Displays the number of seconds an ACS forwarder has been connected to the ACS collector. This parameter is valid only if the *\/Connected* subparameter has a value of 1 \(connected\).|
|Total transmitted events|Displays the number of audit events received from an ACS forwarder or group of forwarders over the present connection.|
|Version|Displays the version of an ACS forwarder's ACS software.|

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
[AdtAdmin.exe UpdForwarder](./AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](./AdtAdmin.exe-UpdGroup.md)



