---
title: Installing a Highly Available VMM Management Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b952e8ab-ce6f-4014-9e96-50cedaf415ed
---
# Installing a Highly Available VMM Management Server
The procedures in this section describe how to do the following in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]:

-   [How to Install a Highly Available VMM Management Server](../Topic/How-to-Install-a-Highly-Available-VMM-Management-Server.md)

-   [How to Install a VMM Management Server on an Additional Node of a Cluster](../Topic/How-to-Install-a-VMM-Management-Server-on-an-Additional-Node-of-a-Cluster.md)

-   [How to Connect to a Highly Available VMM Management Server by Using the VMM Console](../Topic/How-to-Connect-to-a-Highly-Available-VMM-Management-Server-by-Using-the-VMM-Console.md)

-   [How to Uninstall a Highly Available VMM Management Server](../Topic/How-to-Uninstall-a-Highly-Available-VMM-Management-Server.md)

Before you begin the installation of a highly available VMM management server, ensure the following:

-   All computers on which you are installing the highly available VMM management server meet the minimum hardware requirements and that all prerequisite software is installed on all computers, as described in the following topics:

    -   [System Requirements for System Center Technical Preview](../Topic/System-Requirements-for-System-Center-Technical-Preview.md)

    -   [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

-   You have created a domain account that will be used by the Virtual Machine Manager service. You must use a domain account for a highly available VMM management server. For more information about using a domain account, see [Specifying a Service Account for VMM](../Topic/Specifying-a-Service-Account-for-VMM.md).

-   You have installed and configured the failover cluster on which you will install the highly available VMM management server.  For more information about installing and configuring a failover cluster, see[Failover Clustering Overview](http://technet.microsoft.com/library/hh831579.aspx).

-   You are prepared to use distributed key management to store encryption keys in Active Directory Domain Services \(AD DS\). You must use distributed key management for a highly available VMM management server. For more information about distributed key management, see [Configuring Distributed Key Management in VMM](../Topic/Configuring-Distributed-Key-Management-in-VMM.md).

-   You have a computer with a supported version of Microsoft SQL Server installed and running before you start the installation of [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. For information about supported versions of SQL Server for the VMM database, see the following:

    -   [SQL Server Version Compatibility for System Center Technical Preview](../Topic/SQL-Server-Version-Compatibility-for-System-Center-Technical-Preview.md)

    -   [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md)

The following are some recommendations to consider for installing highly available VMM management servers in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]:

-   We recommend that you use a highly available installation of SQL Server.

-   We recommend that the highly available installation of SQL Server is installed on a separate failover cluster from the failover cluster on which you are installing the highly available VMM management server.

-   We also recommend that you use a highly available file server for hosting your library shares.

The following are some additional considerations about highly available VMM management servers in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]:

-   You can only have one implementation of a highly available VMM management server on a given failover cluster.

-   You can have VMM management servers installed on as many as sixteen nodes on a failover cluster, but there can only be one node active at any time.

-   You cannot perform a planned failover \(for example, to install a security update or to do maintenance on a node of the cluster\) by using the VMM console. To perform a planned failover, use Failover Cluster Manager.

-   During a planned failover, ensure that there are no tasks actively running on the VMM management server. Any running tasks will fail during a failover. Any failed jobs will not start automatically after a failover.

-   Any connections to a highly available VMM management server from the VMM console will be lost during a failover. The VMM console will be able to reconnect automatically to the highly available VMM management server after a failover.

