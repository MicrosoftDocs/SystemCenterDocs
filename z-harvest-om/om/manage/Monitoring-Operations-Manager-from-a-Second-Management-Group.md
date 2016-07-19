---
title: Monitoring Operations Manager from a Second Management Group
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e16ee23-917d-4c0c-91c9-3ee9ebd64b7c
author:mgoedtel
manager:cfreemanwa
---
# Monitoring Operations Manager from a Second Management Group
Businesses using [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] in multiple management groups sometimes want to monitor one management group from another management group. This topic provides some tips for monitoring one management group \(management group A\) from a second management group \(management group B\).  
  
-   You can install an agent on management servers in management group A from management group B. If you install the agent manually, configure the agent to report to a management server in management group B.  
  
-   Disable Active Directory integration for the agent you install on the management server in management group A.  
  
-   To upgrade the management server in management group A, you must remove the management group B agent first.  
  
-   After the agent is installed, ensure that you do not configure the agent to also report to management group A \(“multihome” the agent\).  
  
-   Ensure that the Run As accounts for the Default Action Account and Privileged Monitoring Account profiles for the management server in management group B are using credentials that can remotely authenticate and that have sufficient permissions on the management servers in management group A.  
  
## See Also  
[Operations Manager Monitoring Scenarios](../../om/manage/Operations-Manager-Monitoring-Scenarios.md)  
[Integrating Active Directory and Operations Manager](../../om/manage/Integrating-Active-Directory-and-Operations-Manager.md)  
[Connecting Operations Manager With Other Management Systems](../../om/manage/Connecting-Operations-Manager-With-Other-Management-Systems.md)  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[Monitoring UNIX and Linux Computers by Using Operations Manager](../../om/manage/Monitoring-UNIX-and-Linux-Computers-by-Using-Operations-Manager.md)  
[Monitoring .NET Applications](../../om/manage/Monitoring-.NET-Applications.md)  
[Monitoring Service Level Objectives by Using Operations Manager](../../om/manage/Monitoring-Service-Level-Objectives-by-Using-Operations-Manager.md)  
[Monitoring Networks by Using Operations Manager](../../om/manage/Monitoring-Networks-by-Using-Operations-Manager.md)  
[Monitoring Clusters by Using Operations Manager](../../om/manage/Monitoring-Clusters-by-Using-Operations-Manager.md)  
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../../om/manage/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)  
[Monitoring Across Untrusted Boundaries in Operations Manager](../../om/manage/Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)  
[Agentless Monitoring in Operations Manager](../../om/manage/Agentless-Monitoring-in-Operations-Manager.md)  
  
