---
ms.assetid: bc7828ab-1e1f-43d4-a390-c14321f9124b
title: Deploy highly available VMM management server
description: This article provides instructions for deploying the VMM server in high availability mode
author: jyothisuri
ms.author: jsuri
ms.date: 08/02/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-deployment, engagement-fy24
---

# Deploy a highly available VMM management server



This article describes the steps for deploying a highly available System Center Virtual Machine Manager (VMM) server.

## Before you start

- Read the [planning steps](plan-ha-install.md) for a highly available deployment.
- This procedure presumes you're setting up a single failover cluster with two or more file servers.

## Set up the failover cluster

Follow these steps to set up the failover cluster:

1. Select **Server Manager** > **Manage** > **Add Roles and Features**.
2. In **Select installation type**, select **Role-based or feature-based installation**.
3. In **Select destination server**, select the server you want to configure for failover clustering. On **Select features**, select **Failover Clustering**. 
4. Select **Add Feature** to install the failover cluster management tools.
5. In **Confirm installation selections**, select **Install**. A server restart isn't needed.
6. Repeat for each server you want to add as a node in the file server cluster.
7. After you've added at least two nodes in the cluster, you can run cluster validation tests. Open **Failover Cluster Manager** and under **Management**, select **Validate Configuration**.
8. In **Select Servers or a Cluster**, specify the NetBIOS or FQDN of a node you're adding and select **Add**. In **Testing Options**, select **Run all tests (recommended)**.
9. In **Summary**, if the tests completed correctly, select **Create the cluster now using the validated nodes**. Select **View Report** to troubleshoot any issues.
10. In **Access Point for Administering the Cluster**, specify the cluster name. For example, **VMMLibrary**.
 When the cluster is created, this name is registered as the cluster computer object (CNO) in Active Directory. If you specify a NetBIOS name for the cluster, the CNO is created in the same location where the computer objects for the cluster node reside (either the default Computers container or an OU). You can specify a different location by adding the distinguished OU name. For example, CN=ClusterName, OU=Clusters, DC=Contoso. For more information, see [distributed key management](plan-install.md#distributed-key-management).
10. If the server isn't configured to use DHCP, specify a static IP address for the cluster. Select each network you want to use for cluster management, and in **Address**, select the IP address. This is the IP address that is associated with the cluster in DNS.
11. In **Confirmation**, review the settings. Clear **Add all eligible storage to the cluster** if you want to configure storage later. Select **Next** to create the cluster.
12. In **Summary**, confirm that the cluster was created and that the cluster name is listed in Failover Cluster Manager.

### Install VMM on the first cluster node

1. On either node of the cluster you created, run the VMM setup and select **Install**.
2. VMM detects its installation on a cluster node and asks you if you want to make the VMM server highly available. Select **Yes**.
3. In **Select features to install**, select the VMM management server and the VMM console.
4. In **Product registration information**, specify organizational details and the product key.
5. In **EULA and CEIP**, accept the End User License Agreement (EULA) and specify whether you want to participate in Customer Experience Improvement Program (CEIP).
6. In **Installation Location**, accept the default settings.
7. In **Prerequisites**, VMM checks whether all the prerequisites are met and installs the missing components. If you don't have the Windows ADK installed, [download](/windows-hardware/get-started/adk-install) and install it.
8. In **Database configuration**, specify the database to use for VMM. The database should be highly available and deployed in a separate failover cluster. This dialog appears if VMM isn't clustered or if it's clustered but not using Always On Availability Groups. Specify the cluster name.
9. In **Cluster configuration**, specify the name of the VMM cluster. For example, **HAVMMM**.
10. In **Configure service account and distributed key management**, specify the service account and key location you created earlier. VMM Run As accounts are stored as encrypted in the VMM database. For a high availability deployment, you need to access encrypted keys from a central location. So you should have created a distributed key management container in Active Directory before you ran setup. Learn more about distributed key management container [here](plan-install.md#distributed-key-management).
11. In **Port configuration**, modify the port settings if required.
12. Finish installing VMM. You can't specify a library share right now. In a highly available deployment, you create the library share after the installation is complete.

## Install VMM on the second cluster node

1. Run setup and confirm that you want to **add this server as a node** to the highly available deployment.
2. In the wizard, specify the service account password. You don't need to specify other information.

## Next steps

[Deploy SQL Server for VMM high availability](./ha-sql.md).