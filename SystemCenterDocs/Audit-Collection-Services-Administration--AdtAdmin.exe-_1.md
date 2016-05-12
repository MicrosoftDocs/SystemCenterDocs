---
title: Audit Collection Services Administration (AdtAdmin.exe)_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe986ed-e52b-4dd1-ba46-76173ac3fd7c
---
# Audit Collection Services Administration (AdtAdmin.exe)_1
The primary tool for managing Audit Collection Services \(ACS\) in [!INCLUDE[om12long](Token/om12long_md.md)] is a command\-line tool, AdtAdmin.exe, which is run locally on an ACS collector. You can use AdtAdmin to view current configurations and change the default configurations that apply to the ACS collector and ACS forwarders. AdtAdmin also allows you to apply filters that limit the events that are stored in the ACS database. These filters are formatted as Windows Management Instrumentation \(WMI\) Query Language \(WQL\) queries. \(WQL is a subset of the American National Standards Institute Structured Query Language \(ANSI SQL\) with minor semantic changes to support WMI.\)

## AdtAdmin Syntax
AdtAdmin has 12 parameters, each of which has a few to several subparameters. The general syntax of AdtAdmin is as follows:

`AdtAdmin.exe /<Parameter> [/<Subparameter>:<Value>]`

The following table lists each parameter of AdtAdmin along with a description. For more information about the syntax of a specific parameter, click the name of the parameter in the table to link to the topic that describes it.

|Parameter|Description|
|-------------|---------------|
|[AdtAdmin.exe AddGroup](AdtAdmin.exe-AddGroup.md)|Creates a group on an ACS collector. Groups are used to organize ACS forwarders.|
|[AdtAdmin.exe DelGroup](AdtAdmin.exe-DelGroup.md)|Deletes a previously created group on an ACS collector.|
|[AdtAdmin.exe Disconnect](AdtAdmin.exe-Disconnect.md)|Disconnects an ACS forwarder or group of forwarders from an ACS collector.|
|[AdtAdmin.exe GetDBAuth](AdtAdmin.exe-GetDBAuth.md)|Displays the authentication method used by the ACS collector to connect to the ACS database.|
|[AdtAdmin.exe GetQuery](AdtAdmin.exe-GetQuery.md)|Displays the WQL queries currently in use on an ACS collector. WQL queries are used to filter events before they are saved to the ACS database.|
|[AdtAdmin.exe ListForwarders](AdtAdmin.exe-ListForwarders.md)|Displays the name and some statistical information on the ACS forwarders that are connected to an ACS collector.|
|[AdtAdmin.exe ListGroups](AdtAdmin.exe-ListGroups.md)|Displays the groups that are present on an ACS collector.|
|[AdtAdmin.exe SetDBAuth](AdtAdmin.exe-SetDBAuth.md)|Specifies which authentication method the ACS collector uses to connect to the ACS database. Windows Authentication and SQL authentication are the available authentication methods.|
|[AdtAdmin.exe SetQuery](AdtAdmin.exe-SetQuery.md)|Defines a WQL query that the ACS collector uses to filter the audit event data.|
|[AdtAdmin.exe Stats](AdtAdmin.exe-Stats.md)|Displays statistical information about the ACS forwarders that are connected to an ACS collector.|
|[AdtAdmin.exe UpdForwarder](AdtAdmin.exe-UpdForwarder.md)|Allows you to change the name and the value of an ACS forwarder and also to change the group to which an ACS forwarder belongs|
|[AdtAdmin.exe UpdGroup](AdtAdmin.exe-UpdGroup.md)|Allows you to rename a group.|

## Common Subparameters
Each AdtAdmin parameter has from a few to several subparameters. The subparameters allow you to apply a command to a specific ACS collector, a specific ACS forwarder, or group of forwarders and are the same for most AdtAdmin parameters. The subparameters, defined in the following table, can be used with an AdtAdmin parameter unless otherwise noted.

|Subparameter|Description|
|----------------|---------------|
|\/Collector:CollectorName|Specifies an ACS collector to run a command against. If this subparameter is omitted, the local ACS collector is assumed.|
|\/Forwarder:Name|Specifies an ACS forwarder by its computer name.|
|\/ForwarderID:ForwarderIDNumber|Specifies an ACS forwarder by its identification number. An identification number is assigned to an ACS forwarder when it first connects to the ACS collector.|
|\/ForwarderSID:SID|Specifies an ACS forwarder by its computer security identification number \(SID\).|
|\/Group:GroupName|Specifies a group of ACS forwarders by the group’s name.|
|\/GroupID: IdentificationNumber|Specifies a group of ACS forwarders by the group’s identification number. An identification number is assigned to a group when it is first created.|
|\/Value:ValueNumber|Specifies an ACS forwarder or ACS group by its assigned connection value. The ACS collector prioritizes connections from ACS forwarders using connection values that range from \-1 through 99. A \-1 value means the forwarder is part of an ACS group and that the group's value is used to determine the forwarder's priority. A 0 value means the ACS collector ignores data from that ACS forwarder or group. If event saturation is detected, a collector disconnects forwarders or a group of forwarders with lower values before disconnecting forwarders with higher values.|

## See Also
[Collecting Security Events Using Audit Collection Services in Operations Manager](Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)
[How to Configure Certficates for ACS Collector and Forwarder](How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)
[Audit Collection Services Capacity Planning](Audit-Collection-Services-Capacity-Planning.md)
[Audit Collection Services Performance Counters](Audit-Collection-Services-Performance-Counters.md)
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)
[Audit Collection Services Security](Audit-Collection-Services-Security.md)
[How to Filter ACS Events for UNIX and Linux Computers](How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)
[Monitoring Audit Collection Services Performance](Monitoring-Audit-Collection-Services-Performance.md)
[How to Remove Audit Collection Services &#40;ACS&#41;](How-to-Remove-Audit-Collection-Services--ACS-.md)
[Audit Collection Services Security](Audit-Collection-Services-Security.md)


