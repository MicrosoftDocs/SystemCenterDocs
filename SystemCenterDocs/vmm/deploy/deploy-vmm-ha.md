---
ms.assetid: 00698994-021a-413e-94fb-54b07ebe3e4a
title: Deploy VMM for high availability
description: This article describes how to deploy the VMM server in high availability mode.
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Deploy VMM for high availability

>Applies To: System Center 2016 Technical - Virtual Machine Manager

For resilience and scalability you can deploy System Center 2016 - Virtual Machine Manager (VMM) in high availability mode.

## Before you start

You'll need to prepare for a  high availability deployment

- You can only set up one VMM deployment on a failover cluster. You can install VMM management nodes on up to 16 nodes but only one node can be active at any one time.
- Requirement for computers running as VMM management nodes:
	- All the computers that will act as VMM servers must be running Windows Server 2012 R2 or later.
	- You'll need to install Windows ADK for Windows 8.1 on each computer. Install from setup or the [download center](http://go.microsoft.com/fwlink/p/?LinkID=302319). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
	- If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2012 feature pack](http://go.microsoft.com/fwlink/p/?LinkId=253555).
	- Each computer must be joined to a domain, and computer name shouldn't exceed 15 characters.
- Don't install on a Hyper-V host. You can install VMM on a VM.


## Deploy high availability components

- [Deploy the VMM management server in a failover cluster](deploy-vmm-server-ha.md)
- [Make library server file shares highly available](deploy-library-ha.md)
- [Deploy the SQL Server VMM database as highly available](deploy-sql-ha.md)
