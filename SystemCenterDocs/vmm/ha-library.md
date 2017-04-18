---
ms.assetid: 93d075bc-983c-4b91-b800-9c300a47fca2
title: Deploy the VMM library for high availability
description: This article describes how to set up the VMM library in a highly available deployment
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Deploy a highly available VMM library

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes the steps for deploying a highly available System Center 2016 - Virtual Machine Manager (VMM) library. You set up a Windows failover cluster running the File Server role. Then you create file shares on the cluster and assign them as VMM library shares.


## Before you start

Read the [planning steps](plan-ha-install.md) for a highly available VMM deployment.



## Set up the failover cluster

This procedure presumes you're setting up a single failover cluster with two or more file servers.

1. Click **Server Manager** > **Manage** > **Add Roles and Features**.
2. In **Select installation type** click **Role-based or feature-based installation**.
3. In **Select destination server** click the server you want to configure for failover clustering. On Select features click **Failover Clustering**. Click **Add Feature** to install the failover cluster management tools.
4. In **Confirm installation selections** click **Install**. A server restart isn't needed.
5. Repeat for each server you want to add as a node in the file server cluster.
6. After you have at least two nodes in the cluster you can run cluster validation tests (you'll need at least two nodes in the cluster). Open **Failover Cluster Manager** and under **Management** click **Validate Configuration**.
7. In **Select Servers or a Cluster** specify the NetBIOS or FQDN of a node you're adding and click **Add**. In **Testing Options** click **Run all tests (recommended)**.
8. In **Summary**, if the tests completed correctly click **Create the cluster now using the validated nodes**. Click **View Report** to troubleshoot any issues.
9. In **Access Point for Administering the Cluster** specify the cluster name. For example **VMMLibrary**. When the cluster is created this name will be registered as the cluster computer object (CNO) in Active Directory. If you specify a NetBIOS name for the cluster the CNO is created in the same location where the computer objects for the cluster node reside (either the default Computers container or an OU). You can specify a different location by adding the distinguished OU name. For example CN=ClusterName, OU=Clusters,DC=Contoso.
10. If the server isn't configured to use DHCP specify a static IP address for the cluster. Select each network you want to use for cluster management and in **Address** select the IP address. This is the IP address that will be associated with the cluster in DNS.
11. In **Confirmation** review the settings. Clear **Add all eligible storage to the cluster** if you want to configure storage later. Click **Next** to create the cluster.
12. In **Summary** confirm that the cluster was created and that the cluster name is listed in Failover Cluster Manager.

If you want to build a guest cluster to deploy the file server read Rudolf Vesely's useful [blog post](https://techstronghold.com/blogs/virtualization/building-guest-virtual-file-server-failover-cluster-on-hyper-v-host-with-windows-server-2012-r2).

## Set up the file server role

1. On each computer you'll set up as a file server node, in **Failover Cluster Manager** select **Configure Role**.
2. In the **High Availability Wizard** > **Select Role**, select**File Server**.
3. In **File Server Type** select **File Server for general use**.
4.  In **Client Access Point** type the cluster name (in our procedure this was **VMMLibrary** and the cluster IP address.
5.  In **Select storage** specify the shared storage you want to use.
6.  Confirm the settings and finish the wizard.

## Create a file share

1. In **Failover Cluster Management** > cluster name > **Roles**. Select the file server and click **Add File Share**.
2. In **New Share Wizard** > **Select Profile** select **SMB Share - Quick**.
3. In **Share Location** select the file server.
4. In **Share Name** specify the share name and description.
5. In **Other Settings** leave the default settings.
6. In **Permissions** grant full access to the SYSTEM and Administrators accounts, and to the VMM admin account. In **Confirmation** review settings and click **Create**.

## Add the share as a VMM library

1. Open the VMM console > **Library** > **Add Library Server**.
2. In **Add Library Server Wizard** > **Enter Credentials** specify a domain account with permissions for the file cluster.
3. In the **Select Library Servers** page, type in the domain in which the file cluster is located and in **Computer name** specify the name you assigned to file server cluster or click **Search** to find it. Click **Add** > **Next**.
4. On the **Add Library Servers** page select the library shares you want to add. If you want to add the default library resources to the share select **Add Default Resources**. In addition to default resources this adds the ApplicationFrameworks folder to the share.
5. On the **Summary** page review settings and click **Add Library Servers**. In **Library** > **Library Servers** verify the library server and share are listed.
6. After the share is created you can copy resources to the library share.
