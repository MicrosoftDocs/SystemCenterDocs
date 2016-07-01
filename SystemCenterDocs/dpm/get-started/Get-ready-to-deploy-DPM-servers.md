---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-30
title:  Get ready to deploy DPM servers
ms.technology:  data-protection-manager
ms.assetid:  517ce276-b811-4a06-ade3-ff71303ccf5b
---

# Get ready to deploy DPM servers

>Applies To: System Center 2016 Technical Preview - Data Protection Manager

There are a few planning steps to consider before you begin to deploy your DPM servers:

-   [Plan for DPM server deployment](#BKMK_Server) - Figure out how many DPM servers you'll need and where to place them.

-   [Plan firewall settings](#BKMK_Firewall) - Get information about firewall, port and protocol settings on the DPM server, protected machines, and a remote SQL Server if you're setting one up.

-   [Grant user permissions](#BKMK_Users) - Specify who can interact with DPM.

## <a name="BKMK_Server"></a>Plan for DPM server deployment
Firstly determine how many servers you'll need:

-   DPM can protect up to 600 volumes, 300 replica volumes, and 300 recovery point volumes. To protect this maximum size, DPM needs 120 TB per DPM server, with 80 TB replica space with a maximum recovery point size of 40 TB.

-   A single DPM server can protect up to 2000 databases (recommended disk size 80 TB).

-   A single DPM server can protect up to 1000 client computers and 100 servers.

-   DPM has a snapshot limit of 9,000 disk-based snapshots on a single server, including those retained when you stop protection of a data source. The snapshot limit applies to express full backups and file recovery points, but not to incremental synchronizations. Note that the limit applies regardless of storage pool size.

-   For DPM server capacity planning you can use the [DPM storage calculators](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=24375). These calculators are Excel sheets and are workload specific. They provide guidance about the number of DPM servers required, processor core, RAM, and virtual memory recommendations, and required storage capacity. Because these calculators are workload-specific you'll need to combine the recommended settings and consider them together with the system requirements, and your specific business topology and requirements, including data source and storage locations, compliance and SLA requirements, and disaster recovery needs. Note that the calculators were released for DPM 2010 but remain relevant for later DPM versions.

Then figure out how to locate the servers:

-   DPM must be deployed in an Active Directory domain (Windows Server 2008 onwards).

-   When deciding where to locate your DPM server, consider the network bandwidth between the DPM server and the protected computers. If you are protecting data over a wide area network (WAN), there is a minimum network bandwidth requirement of 512 kilobits per second (Kbps).

-   DPM supports teamed network adapters (NICs). Teamed NICs are multiple physical adapters that are configured to be treated as a single adapter by the operating system. Teamed NICs provide increased bandwidth by combining the bandwidth available using each adapter and failover to the remaining adapter when an adapter fails. DPM can use the increased bandwidth achieved by using teamed adapter on the DPM server.

-   Another consideration for the location of your DPM servers is the need to manage tapes and tape libraries manually, such as adding new tapes to the library or removing tapes for offsite archive.

-   A DPM server can protect resources within a domain, or across domains within a forest that has a two-way trust relationship with the domain that the DPM server is located in. If there isn't a two-way trust across domains, you need a separate DPM server for each domain. A DPM server can protect data across forests if there's a forest-level two-way trust between the forests.

-   Consider the network bandwidth between the DPM server and the protected computers. If you are protecting data over a WAN there's a minimum network bandwidth requirement of 512 Kbps. Note that DPM supports teamed NICs that provide increased bandwidth by combining bandwidth available for each network adapter, and failover if an adapter fails.

## <a name="BKMK_Firewall"></a>Plan firewall settings and user permissions

### Firewall settings
Firewall settings for DPM deployment are required on the DPM server, on machines you want to protect, and on the SQL Server used for the DPM database if you're running it remotely. If Windows Firewall is enabled when you install DPM then DPM setup automatically configures the firewall settings on the DPM server. The firewall settings are summarized in the following table.

|Location|Rule|Details|Protocol|Port|
|------------|--------|-----------|------------|--------|
|DPM server|System Center <version> Data Protection Manager DCOM Setting|Used for DCOM communication between DPM server and protected machines|DCOM|135/TCP Dynamic|
|DPM server|System Center <version> Data Protection Manager|Exception for Msdpm.exe (the DPM service). Runs on the DPM server|All protocols|All ports|
|DPM server<br /><br />Protected machines|System Center <version> Data Protection Management Replication Agent|Exception for Dpmra.exe (protection agent service used to back up and restore data). Runs on the DPM server and on protected machines.|All protocols|All ports|
|Protected machines||Configure incoming exception for sqserv.exe|||
|Protected machines||DPM issues commands to the protection agent with DCOM calls to the agent.   You'll need to open the upper ports (1024-65535) for DPM to communicate|DCOM|135/TCP Dynamic|
|Protected machines||The DPM data channel is TCP. Both the DPM server and the protected machines initiate connections. DPM communicates with the agent coordinator on port 5718 and with the protection agent on port 5719|TCP|5718/TCP<br /><br />5719/TCP|
|Protected machines||Used for host name resolution between DPM/protected machine, and the domain controller|DNS|53/UDP|
|Protected machines||Used for authentication of the connection endpoint, between DPM/protected machine, and the domain controller|Kerberos|88/UDP<br /><br />88/TCP|
|Protected machines||Used for queries between the DPM server and the domain controller|LDAP|389/TCP<br /><br />389/UDP|
|Protected machines||Used for miscellaneous operations between 1) DPM and protected machines, 2) DPM and the domain controller 3) Protected machines and the domain controller. Also used for SMB directly hosted on TCP/IP for DPM functions|NetBIOS|137/UDP<br /><br />138/UDP<br /><br />139/TCP<br /><br />445/TCP|
|Remote SQL Server||Enable TCP/IP for the DPM instance of SQL Server with the following: default failure audit; enable password policy checking|||
|Remote SQL Server||Enable incoming exception for sqservr.exe for DPM instance of SQL Server to allow TCP on port 80. The report server listens for HTTP requests on port 80.|||
|Remote SQL Server||Default instance of database engine listens on TCP port 1443.  Can be modified<br /><br />To use the SQL Server Browser service to connect on non-default port set UDP port 1434|||
|Remote SQL Server||Named instance of SQL Server uses Dynamic ports by default. Can be modified.|||
|Remote SQL Server||Enable RPC|||

### <a name="BKMK_Users"></a>Grant user permissions
Before you begin a DPM deployment, verify that appropriate users have been granted required privileges for performing the various tasks. These are summarized in the following table.

|DPM task|Permissions needed|
|------------|----------------------|
|Add the DPM server to a domain|Domain admin account, or user right to add workstation to domain|
|Install DPM|Admin account on the DPM server|
|Install DPM protection agent on machine you want to protect|Domain account that's in the local administrators group on the machine|
|Extend AD schema to enable end-user recovery|Schema admin privileges for the domain|
|Create AD container to enable end-user recovery|Domain admin privileges|
|Grant DPM server permission to change container contents|Domain admin privileges|
|Enable end-user recovery on DPM server|Admin account on the DPM server|
|Install recovery point client software on protected machine|Admin account on machine|
|Access previous versions of protected data from protected machine|User account with access to protected share|
|Recover SharePoint data|SharePoint farm admin that's also an admin on the front-end Web server on which the protection agent is installed.|
