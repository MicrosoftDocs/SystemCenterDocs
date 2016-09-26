---
title: Set up file storage in the VMM fabric
description: This article describes how to set up file storage in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Set up file storage in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

You can manage file storage that supports SMB 3.0 in the System Center 2016 - Virtual Machine Manager (VMM) storage fabric. This includes  Windows file servers, scale-out file servers (SOFS), network-attached storage (NAS) devices from third-parties such as EMC, and NetApp.

This article describes how to add file storage to the VMM fabric. After file shares are available in the fabric, you can assign them to Hyper-V hosts and clusters.


## Add a file share to the VMM fabric

When you add a file server, VMM automatically discovers all the shares that are currently present on the server.

1. Click **Fabric** > **Storage** > **Add Resources** > **Storage Devices**.
2. In **Add Storage Devices Wizard** > **Select Provider Type**, select **Add a Windows-based file server as managed storage device** to manage a single or clustered file server in the VMM console.
3. In **Specify Discovery Scope**, specify the address or name of the file server. If the file server resides in a domain that isn't trusted by the domain in which the virtual machine hosts are located, select **This computer is in an untrusted Active Directory domain**. Select a Run As account that can access the file server.
4. In **Gather Information**, VMM automatically tries to discover and import information about the shares on the file server. If the discovery process succeeds, information about the file server is displayed. When the process finishes, click **Next**.
5. In **Select Storage Devices**, select the file shares that you want VMM to manage.
6. In **Summary**, review the settings and click **Finish**.

## Create a file share

You need to create a file share on the file server. When you do this VMM assigns permissions automatically.

1. Click **Fabric** > **Storage** > **Providers**.
2. Select the file server > **Create File Share**.
3. In **Create File Share**, specify the path on which you want to create the share. If it doesn't exist VMM will create it.  


## Assign files shares

You can assign file shares on any host on which you want to create VMs that will use the file share as storage.


1. Click **Fabric** > **Servers** > **All Hosts**, and select the host or cluster node you want to configure.
2. In **Host** > **Properties**, click **Properties** > **Host Access**. Specify a Run As account. By default the Run As account that was used to add the host to VMM is listed. In the Run As account box, configure the account settings. You can't use the account that you use for the VMM service.

	- If you used a domain account for the VMM service account, add the domain account to the local Administrators group on the file server.
	- If you used the local system account for the VMM service account, add the computer account for the VMM management server to the local Administrators group on the file server. For example, for a VMM management server that is named VMMServer01, add the computer account VMMServer01$.
	- Any host or host cluster that accesses the SMB 3.0 file share must have been added to VMM using a Run As account. VMM automatically uses this Run As account to access the SMB 3.0 file share.
	- If you specified explicit user credentials when you added a host or host cluster, you can remove the host or cluster from VMM, and then add it again by using a Run As account.

3. Click **Host Name Properties** > **Storage** > **Add File Share**.
4. In **File share path**, select the required SMB 3.0 file share, and then click **OK**. To confirm that the host has access, open the **Jobs** workspace to view the job status. Or, open the host properties again, and then click the **Storage** tab. Under **File Shares**, click the SMB 3.0 file share. Verify that a green check mark appears next to **Access to file share**.
5. Repeat this procedure for any standalone host that you want to access the SMB 3.0 file share, or for all nodes in a cluster
