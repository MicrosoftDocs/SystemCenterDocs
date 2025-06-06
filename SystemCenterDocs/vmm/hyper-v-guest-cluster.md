---
ms.assetid: bed9e382-7a24-48d2-a15c-cb3413756236
title: Create a guest cluster from a service template
description: This article provides guidance about creating a guest cluster from a service template
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/21/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Create a guest cluster from a VMM service template



Use this article if you want to create a guest failover cluster using a System Center Virtual Machine Manager (VMM) service template.

A guest failover cluster consists of multiple VMs that are deployed in a cluster and use shared storage. Services in VMM are used to group together virtual machines to provide an app. Service templates contain information about a service, including the VMs that are deployed as part of the service, the applications to install on VMs, and the network configuration that must be used. You can add VM templates, network settings, applications, and storage to a service template. [Learn more](library-service-templates.md).

You can use service templates to create a guest cluster. That cluster can then be configured to run an app, such as SQL Server.

## Before you start

Here are some considerations before you deploy VMs to Hyper-V host clusters:

::: moniker range="sc-vmm-2016"
- VMs in a guest cluster can only be deployed to Hyper-V host clusters running Windows Server 2012 R2 or later. Otherwise, deployment will fail.
::: moniker-end
::: moniker range=">sc-vmm-2016 <=sc-vmm-2022"
- VMs in a guest cluster can only be deployed to Hyper-V host clusters running Windows Server 2016 or later. Otherwise, deployment will fail.
::: moniker-end
::: moniker range="sc-vmm-2025"
- VMs in a guest cluster can only be deployed to Hyper-V host clusters running Windows Server 2019 or later. Otherwise, deployment will fail.
::: moniker-end
- You can deploy a guest failover cluster that uses shared .vhdx files on a Hyper-V failover cluster. In this scenario, if Hyper-V uses Cluster Shared Volumes (CSVs) on block-level storage, then the shared vhdx files are stored on a CSV that's configured as shared storage.

- Alternatively, Hyper-V can use SMB file-based storage deployed by Scale-Out File Server (SOFS) as the location of the shared .vhdx files.

- No other shared storage types are supported for guest clusters. Non-Microsoft SMB storage isn't supported.

- You need many scripts to create the guest cluster, including a script to run on the first VM in the cluster and a script to run on the other VMs so that they can join the cluster. Script settings are specified in the service template application settings.

- To configure shared disks for the cluster, you need to use new VHDX files. Don't reuse from a previous cluster. Ensure that the hard disk files are in the VMM library.

- Identify a single path in SCSI-based storage where all the VHDX files for the guest cluster will be placed at deployment time. You can use storage classifications to control the placement of VHDX files, but you need at least one location in the classification with the capacity to hold all the VHDX files. VMM doesn't deploy the VHDX files to multiple locations.

- You can vary the location of VHDX files at deployment time, even if you use the same service template to deploy multiple guest clusters. To do this, you need to deploy the guest clusters to a host group and not a cloud. Then at deployment, you specify a single path for all the shared VHDX files for the cluster. This overrides the location specified in the VM template.

- You need a virtual hard disk file that contains the operating system (prepared with Sysprep) that you want the VMs in the guest cluster to use. When each node is created, VMM uses a copy of the virtual hard disk file for the system disk of the node.

## Specify scripts that run when a guest cluster is created

To specify scripts that run when a guest cluster is created, follow these steps:

1. [Set up an application profile](library-profiles.md#create-an-application-profile).
2. In **New Application Profile** > **General** > **Compatibility**, leave the default **General** setting enabled.
3. In **Application Configuration** > **OS Compatibility**, select one or more editions of a server operating system.
4. Add the scripts you need for creating the first node of the cluster and then adding other nodes. Provide the scripts as follows:
    - For a script that will run on the first node of the cluster when it's created (and not on other nodes), **for Script command type**, select **Creation: First VM**.
    - For a script that'll run on later nodes of the cluster when they're created (and not on the first node), for **Script command type**, select **Creation: VMs After First**.
    - For each script, specify the executable name and the parameters through which the script will run and the Run As account.
    - Configure other settings as needed, including how long the script must run before timing out, failure, and restart policies.
    - A script can contain settings to be entered when you're configuring the service for deployment. To format this type of setting, enter the parameter in the **Parameters** field in the following format: @\<SettingLabel\>@ (for example, enter @ClusterName@). Example: a script FormCluster.exe that runs with Cmd.exe and the /q and /c parameters and requires the cluster name would be Executable Program: **Cmd.exe**, Parameters: **/q** **/c** **FormCluster.cmd** **\@ClusterName@**
    - You can also add scripts to delete the cluster in an orderly way. **Script command type** would be **Deletion: VMs Before Last** or **Deletion: Last VM**.
    - You can also add a script of type **Pre-Install** that'll run on the first VM and on later VMs that are created as part of the service tier.
5. Select **OK** to save settings and verify that the profile was created in **Profiles** > **Application Profiles**. The profile appears in the **Profiles** pane.

## Create a VM template

Create a VM template that includes settings for a shared .vhdx file. This file must be deployed to shared storage that has SCSI channels available for each cluster node to provide the same access to the file for each node.

To create a VM template, follow these steps:

1. In the VMM library, verify that you have a virtual hard disk that contains the operating system (created using SysPrep) you want to use for VM in the guest cluster. It mustn't be blank.
2. Select **Create a VM template**.
3. In the **Create VM Template Wizard** > **Select Source**, select **Use an existing VM template or virtual hard disk stored in the library** > **Browse**.
4. In **Select VM Template Source**, select the virtual hard disk you want to use.
5. In **Configure Hardware**, specify a hardware profile or hardware settings.
6. To configure the guest cluster to use a shared .vhdx, in **Bus Configuration** select **SCSI adapter 0**, and then next to **New**, select **Disk**. The new disk appears as a listing under the SCSI adapter. Select the disk and select **Share the disk across the service tier**.
7. Clear **Contains the operating system for the virtual machine**. Select **Browse** and select the .vhdx file that you want VMM to deploy to shared storage and select **OK**. Repeat for each additional node in the cluster. Add the same disk each time but ensure that the SCSI channel is unique for each node.
6. In **Network Adapters**, select the adapter and select **Enable guest specified IP addresses**. This enables the nodes (VMs) in the cluster to specify the IP addresses for the cluster itself and for applications that you configure to run in the cluster.
7. In **Advanced** > **Availability**, select **Make this virtual machine highly available**. With this setting, enable the VM is created as a clustered instance on the host cluster so that if one host fails, the VM fails over to another host in the cluster.
8. Select **Manage availability sets** > **Create**. The availability set you create will be used by all the nodes in the guest cluster. This means that VMM will attempt to keep the VMs on separate hosts so that if one host fails VMs on a different host can provide services.
9. In **Configure Operating System**, open the **Guest OS profile** list and select a guest operating system profile or **Create new Windows operating system customization settings**. Your selection determines whether additional wizard pages are displayed.
    - Under **Identity Information** > **Computer name**, you can provide a pattern to generate computer names. For example, if you enter server####, the computer names that are created are server0001, server0002, and so on. The use of a pattern ensures that when you add additional virtual machines to a service, the computer names that are generated are related and identifiable. If you use this method to specify the computer name, you can't use it in combination with a name prompt parameter (@\<name\>@). You can use one method or the other, but not both.
    - Under **Networking**, you can specify Active Directory settings using the FQDN or using at signs (@) before and after the domain name; for example, @Domain@. Using the at signs (@) in this way, the necessary information can be entered when the virtual machine is deployed as part of a service. You don't need a trust relationship between the domain in which the service is deployed and the VMM management server domain.
10. Finish the wizard to create the VM template.

## Include the VM template in a service template

To include the VM template in a service template, follow these steps:

1. [Create a service template](library-service-templates.md), and add the VM template to the appropriate template tier.
2. After you save and validate the template, right-click the tier object in the service template designer and select **Properties**.
3. In **Application Configuration**, add the application profile you created. When the service is deployed, the scripts in the application profile will run. Save and validate the service template.
4. Right-click the service template again > **Properties**.
5. In **General**, select **This machine tier can be scaled out** and specify a value greater than 1 for **Default instance count** and **Maximum instance count**. The maximum must be set to less or equal to the number of SCSI channels you configured in the VM template. The default count must be less than the maximum.
6. In **Number of upgrade domains**, specify the same value as that in **Maximum instance count**. For example, if you specify a default count of 3 and a maximum count of 3, the guest cluster will have three nodes. The number of upgrade domains must also be set to 3 so that updates are performed in three stages, one node (VM) at a time. This leaves at least two VMs in the guest cluster running during planned maintenance.
7. Save and validate the service template.

After you've set up the guest cluster, you're ready to deploy the service.

## Next steps

[Create and deploy VMs in the VMM fabric from a VM template](vm-template.md).
