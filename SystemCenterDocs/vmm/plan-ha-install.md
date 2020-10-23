---
ms.assetid: b60c4398-37f7-4015-afe7-229d7c62ea01
title: Plan a highly available VMM deployment
description: This article provides planning information for deploying VMM and its components in high availability mode
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 10/23/2020
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Plan a highly available VMM deployment

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end


This article helps you to plan a highly available System Center - Virtual Machine Manager (VMM) deployment.

For resilience and scalability you can deploy VMM in high availability mode, as follows:

- Deploy the VMM management server in a failover cluster.
- Make library server file shares highly available
- Deploy the SQL Server VMM database as highly available.

## Plan a highly available SQL Server deployment


- You should set up SQL Server before you deploy the VMM management servers.
- We recommend you use a highly available SQL Server installation on a failover cluster and configure SQL Server Always On availability groups.
You shouldn't install SQL Server on the VMM cluster.
- Review the [best practices](https://msdn.microsoft.com/library/ms189910.aspx) for failover cluster node prerequisites.
- Always On availability groups are supported in VMM. Use **synchronous commit** for higher protection with more overhead. If you use **asynchronous-commit** mode the secondary database can lag behind the primary database making some data loss possible.
- The database server must be in the same domain as the VMM server, or in a domain with a two-way trust.
- Using a clustered database with VMM requires Kerberos authentication. To support this, the SQL Server instance must associate a Service Principal Name (SPN) with the account that SQL Server will be running on.


## Plan a highly available VMM management server
- Don't install on a Hyper-V host parent partition. You can install VMM on a VM.
- Before you start you'll need to set up the VMM service account and distributed key management. [Learn more](~/vmm/install.md)
- Only one instance of VMM can be deployed to a failover cluster of up to 16 nodes.
- The user who creates the cluster has **Create Computers objects** permission to the OU or the contain where the servers that will form the cluster reside. If this isn't possible ask a domain admin to pre-stage a cluster computer object for the cluster.
- Requirements for computers running as VMM management nodes:
	- All cluster nodes that will act as VMM servers must be running either Windows Server 2016 or Windows Sever 2019.
	- Each cluster node must be joined to a domain and must have a computer name that does not exceed 15 characters.
	- The VMM service network name must not exceed 15 characters.
	- Windows ADK needs to be installed on each computer. Install from setup or the [download center](https://go.microsoft.com/fwlink/p/?LinkId=614942). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
	- If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2012 feature pack](https://go.microsoft.com/fwlink/p/?LinkId=253555) or [SQL Server 2014 feature pack](https://go.microsoft.com/fwlink/?LinkID=529794) or [SQL Server 2016 feature pack](https://www.microsoft.com/en-us/download/details.aspx?id=52676).


## Plan a highly available VMM library

You can create highly-available library servers to ensure that file-based resources, templates, and profiles are resilient and available.

- VMM doesn't automatically create the VMM library as highly available when you deploy VMM in high availability mode. You need to create highly available library servers by deploying the library on a file server cluster.
- You'll need to set up a file server failover cluster. Deploying highly available library shares on the VMM cluster isn't supported.
- Computers you'll configure as file servers should be running Windows Server 2012 R2 or later. We recommend that all nodes have the same version of Windows.
- All nodes you want to add as file servers should be in the same domain.
- Make sure the hardware and software that you want to use for the library meets the system requirements.
- The user who creates the cluster has **Create Computers objects** permission to the OU or the contain where the servers that will form the cluster reside. If this isn't possible ask a domain admin to pre-stage a cluster computer object for the cluster.
- The account you use to create the cluster should be a domain user on all the computers you want to add as file server nodes.
- The library server can't be a scale-out file server (SOFS).  It must be on a failover cluster that doesn't use the SOFS cluster role. This is because when you deploy the library the VMM agent is deployed on the host. For SOFS there are multiple hosts in a cluster provides shares which makes it complicated for agent deployment. When you have a standalone or clustered library server, you can leverage storage on SOFS by creating shares on it.
- You can deploy the library shares on a cluster with physical nodes, or a guest cluster.
- If you want to add clustered storage when you create the cluster make sure all computers can access the storage.
- If you want to deploy a distributed VMM library in different datacenters you'll need to set up a scheduled copy between the two library shares. No replication is available.

## Next steps

- [Set up a highly available VMM deployment](high-availability.md)
