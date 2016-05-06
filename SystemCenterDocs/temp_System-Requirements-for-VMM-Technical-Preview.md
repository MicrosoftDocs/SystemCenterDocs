---
title: temp_System Requirements for VMM Technical Preview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7de7bd4a-1c2f-4841-a9fb-5a9ecce7769b
---
# temp_System Requirements for VMM Technical Preview
This topic describes the operating system and other software requirements for [!INCLUDE[scvm_threshold_1](Token/scvm_threshold_1_md.md)]

## Operating system and other software support for servers and hosts in VMM
The following table lists the operating systems and other software supported on VMM servers and hosts in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]

|Type of [!INCLUDE[vmm12short](Token/vmm12short_md.md)] system|Versions of software supported in this release|Notes|
|--------------------------------------------------------------------|--------------------------------------------------|---------|
|VMM management server|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]|The VMM management server requires the Windows Assessment and Deployment Kit. Supported versions are<br /><br />[Windows Assessment and Deployment Kit (AD) for Windows 10](http://go.microsoft.com/fwlink/?LinkID=523995)<br /><br />The VMM management server uses the version of the .NET Framework that is included with [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)].<br /><br />For full functionality with service templates, the VMM management server requires the [SQL Server 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295).|
|VMM database|SQL Server 2014 Enterprise \(64\-bit\)<br /><br />SQL Server 2012 Enterprise \(64\-bit\)|Can be on same server or different server from VMM management server.|
|VMM console|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]<br /><br />[!INCLUDE[winthreshold_client_2](Token/winthreshold_client_2_md.md)]<br /><br />Windows Server 2012 R2<br /><br />Windows 8.1|Can be on same computer or different computer from VMM management server.|
|VMM library server|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]<br /><br />Windows Server 2012 R2<br /><br />Windows Server 2012<br /><br />Windows Server 2008 R2 SP1|Can be on a different server from VMM management server.<br /><br />To make the VMM library server highly available, you can create highly available file shares on a clustered file server. However, do not create highly available file shares for the VMM library on the same cluster as a highly available VMM management server installation. VMM does not support this configuration.|
|Hosts under management by VMM|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)], Hyper\-V server role<br /><br />Windows Server 2012<br /><br />Windows Server 2012 R2|You can bring existing Hyper\-V hosts under management, but you cannot deploy Hyper\-V hosts from bare metal.<br /><br />You can create failover clusters from Hyper\-V hosts running [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]. The hosts must be able to pass the tests in the failover cluster validation wizard or the [Test-Cluster](http://technet.microsoft.com/library/hh847274.aspx) Windows PowerShell cmdlet.<br /><br />You can create Scale\-Out File Server clusters from servers running [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]. The servers must be able to pass the tests in the cluster validation wizard or the [Test-Cluster](http://technet.microsoft.com/library/hh847274.aspx) Windows PowerShell cmdlet.|
|Windows Server Update Services \(WSUS\) server|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]<br /><br />[!INCLUDE[winblue_server_2](Token/winblue_server_2_md.md)]|You can add a WSUS server and use it to manage software updates \(patching\) for Hyper\-V hosts.<br /><br />You can also use the WSUS server to manage patching for "infrastructure servers" \(such as DHCP servers\) that are virtual machines running [!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)] as the guest operating system. These virtual machines can be highly available virtual machines running on host clusters.|
|Infrastructure Servers|[!INCLUDE[winthreshold_server_2](Token/winthreshold_server_2_md.md)]<br /><br />Windows Server 2012 R2||
|Server used for monitoring and reporting|Operations Manager in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)],  running SQL Server 2012 SP2 or SQL Server 2014 with reporting services enabled||
|SQL Server Utilities|SQL Server 2014 Feature Pack<br /><br />SQL Server 2012 Feature Pack||


