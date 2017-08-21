---
ms.assetid: bc7828ab-1e1f-43d4-a390-c14321f9124b
title: Deploy VMM for high availability
description: This article provides instructions for deploying the VMM server in high availability mode
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  08/21/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Deploy a highly available VMM management server

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes the steps for deploying a highly available System Center 2016 - Virtual Machine Manager (VMM) server.

## Before you start

- Read the [planning steps](plan-ha-install.md) for a highly available deployment.
- This procedure presumes you're setting up a single failover cluster with two or more file servers.

## Set up the failover cluster

1. Click **Server Manager** > **Manage** > **Add Roles and Features**.
2. In **Select installation type** click **Role-based or feature-based installation**.
3. In **Select destination server** click the server you want to configure for failover clustering. On Select features click **Failover Clustering**. Click **Add Feature** to install the failover cluster management tools.
4. In **Confirm installation selections** click **Install**. A server restart isn't needed.
5. Repeat for each server you want to add as a node in the file server cluster.
6. After you have at least two nodes in the cluster you can run cluster validation tests (Open **Failover Cluster Manager** and under **Management** click **Validate Configuration**.
7. In **Select Servers or a Cluster** specify the NetBIOS or FQDN of a node you're adding and click **Add**. In **Testing Options** click **Run all tests (recommended)**.
8. In **Summary**, if the tests completed correctly click **Create the cluster now using the validated nodes**. Click **View Report** to troubleshoot any issues.
9. In **Access Point for Administering the Cluster** specify the cluster name. For example **VMMLibrary**.
 When the cluster is created this name is registered as the cluster computer object (CNO) in Active Directory. If you specify a NetBIOS name for the cluster the CNO is created in the same location where the computer objects for the cluster node reside (either the default Computers container or an OU). You can specify a different location by adding the distinguished OU name. For example CN=ClusterName, OU=Clusters,DC=Contoso. For more information, see [distributed key management](plan-install.md#distributed-key-management).
10. If the server isn't configured to use DHCP specify a static IP address for the cluster. Select each network you want to use for cluster management and in **Address** select the IP address. This is the IP address that is associated with the cluster in DNS.
11. In **Confirmation** review the settings. Clear **Add all eligible storage to the cluster** if you want to configure storage later. Click **Next** to create the cluster.
12. In **Summary** confirm that the cluster was created and that the cluster name is listed in Failover Cluster Manager.

### Install VMM on the first cluster node

1. On either node of the cluster you created run VMM setup and click **Install**.
2. VMM detects its installing on a cluster node and asks you if you want to make the VMM server highly available. Click **Yes**.
3. In **Select features to install** select the VMM management server and the VMM console.
4. In **Product registration information** specify organizational details and the product key.
5. IN **EULA and CEIP** accept the EULA and specify whether you want to participate in CEIP.
6. In **Installation Location** accept the default settings.
7. In **Prerequisites** VMM checks whether all prerequisites are met and installs missing components. If you don't have the Windows ADK installed, download and install it.
8. In **Database configuration** specify the database to use for VMM. The database should be highly available and deployed in a separate failover cluster. This dialog appears if VMM isn't clustered, or if it's clustered but not using Always On Availability Groups. Specify the cluster name.
9. In **Cluster configuration** specify the name of the VMM cluster for example **HAVMMM**.
10. In **Configure service account and distributed key management** specify the service account and key location you created earlier. VMM Run As accounts are stored as encrypted in the VMM database. For a high availability deployment, you need to access encrypted keys from a central location so you should have created a distributed key management container in Active Directory before you ran setup.

 Learn more about distributed key management container  [here](plan-install.md#distributed-key-management).
11. In **Port configuration** modify port settings if you need to.
12. Finish installing VMM. You can't specify a library share right now. In a highly available deployment you create the library share after installation is complete.

## Install VMM on the second cluster node

1. Run setup and confirm that you want to **add this server as a node** to the highly available deployment.
2. During the wizard specify the service account password. You don't need to specify other information.
