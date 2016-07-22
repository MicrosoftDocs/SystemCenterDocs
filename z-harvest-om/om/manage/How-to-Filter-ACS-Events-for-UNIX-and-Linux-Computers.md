---
title: How to Filter ACS Events for UNIX and Linux Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2443e38b-8682-474a-ae1f-0c2f7de34a84
author:mgoedtel
manager:cfreemanwa
---
# How to Filter ACS Events for UNIX and Linux Computers
By default, ACS collects and stores every event recorded in the Windows Security Event logs. A large number of the events can make it difficult to identify potential problems. You want to collect only the security events that meet your audit and security compliance requirements.  
  
Best practice is to archive the data by using an ACS Archiver and then restore it to a historical repository. From this repository, you can run your filtering. The following procedure provides the ability to maintain all audit events and optimize the audit data report performance.&nbsp;For example, you may want to store all Successful Logon Events \(540,528\), but not report on them unless audited.  
  
### To filter Event IDs by using AdtAdmin  
  
1.  At a command prompt, change the working directory to **%windir%\\system32\\security\\AdtServer**.  
  
2.  At the same command prompt, set the query parameters by entering **AdtAdmin \/setquery \/query:"select \* from AdtsEvent where NOT \(EventID\=560 OR EventID\=562 OR ...\)"**, where the EventIDs listed are the audit events to be ignored in the event log.  
  
    For example, to set a filter so that only the UNIX and Linux security events are logged to the Windows Security Event log , set the query parameters by entering **AdtAdmin \/setquery \/query:"select \* from AdtsEvent where NOT \(EventID\=560 OR EventID\=562 OR EventID\=569 OR EventID\=570 OR EventID\=571 OR EventID\=26401 OR EventID\=4665 OR EventID\=4666 OR EventID\=4667 OR EventID\=4624 OR EventID\=4634 OR EventID\=4648 OR EventID\=5156 OR EventID\=4656 OR EventID\=4658 OR EventID\=5159\)"**.  
  
For additional information about how to use AdtAdmin.exe, see [Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md).  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[How to Configure Certficates for ACS Collector and Forwarder](../../om/manage/How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[How to Remove Audit Collection Services &#40;ACS&#41;](../../om/manage/How-to-Remove-Audit-Collection-Services--ACS-.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
