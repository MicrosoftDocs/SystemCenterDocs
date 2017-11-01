---
ms.assetid: 6cc028a5-1e33-4c8c-afaf-be1eb26bcf3f
title: Provision a scale-out file server (SOFS) cluster from bare metal computers
description: This article provides about provisioning an SOFS in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Provision a scale-out file server (SOFS) cluster from bare metal computers in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

In addition to adding existing file servers to an SOFS cluster in the System Center - Virtual Machine Manager (VMM)  fabric, VMM can discover provision bare-metal machines as SOFS cluster nodes. This article includes the steps for setting up a bare metal SOFS cluster in VMM.

## Before you start

Here's what you need for the deployment:

- **Physical computers** to deploy as SOFS cluster nodes. These computers must meet the prerequisites described in the table below. They can be running on operating system, or an operating system that will be overwritten during the deployment process.
- **Virtual hard disk** with an appropriate operating system, located on a VMM library share. When you create the virtual hard disk, you can create a virtual machine, install the guest operating system, and then use Sysprep with the /generalize and the /oobe options.<br/><br/> The operating system on the virtual hard disk that you deploy on the cluster nodes must support the boot from virtual hard disk (VHD) option.
- **PXE server** configured with Windows Deployment Services is needed for bare metal deployment.

### Physical computer requirements

**Prerequisite** | **Details**
--- | ---
**BMC** | Each physical computer must have a baseboard management controller (BMC) installed that enables out-of-band management by VMM.<br/><br/> Through a BMC, you can access the computer remotely, independent of the operating system, and control system functions such as the ability to turn the computer off or on.<br/><br/> The BMCs must use one of the supported out-of-band management protocols, and the management protocol must be enabled in the BMC settings.<br/><br/> Supported protocols: Intelligent Platform Management Interface (IPMI) versions 1.5 or 2.0; Data Center Management Interface (DCMI) version 1.0; System Management Architecture for Server Hardware (SMASH) version 1.0 over WS-Management (WS-Man); custom protocols such as Integrated Lights-Out (iLO)<br/><br/> The BMCs should use the latest version of firmware for the BMC model.<br/><br/> The BMCs must be configured with logon credentials and must use either static IP addressing or DHCP. If you use DHCP, we recommend that you configure DHCP to assign a constant IP address to each BMC, for example by using DHCP reservations.<br/><br/> The VMM management server must be able to access the network segment on which the BMCs are configured.
**Operating system** | Physical computers must be running Windows Server 2012 R2 or later.
**Accounts** | You'll need two RunAs accounts.<br/><br/> A Run As account for joining computers to the domain, and an account for access to the BMC on each computer.


### PFX server requirements

**Prerequisite** | **Details**
--- | ---
**Deployment requirements** | You must have a PXE server configured with Windows Deployment Services.<br/><br/> If you have an existing PXE server in your environment configured with Windows Deployment Services, you can add that server to VMM. Then you can use it for provisioning in VMM (and VMM will recognize only the resulting servers). All other requests will continue to be handled by the PXE server according to how it is configured.<br/><br/> If you don't have an existing PXE server, you can deploy the Windows Deployment Services role on a server running a supported operating system (Windows Server 2012 R2 or later).
**Location** | The PXE server must be in the same subnet as the physical computers that you want to provision.
**Windows Deployment Services installation** | When you install Windows Deployment Services you should install both the Deployment server and Transport server options. You don't need to add images.<br/><br/> During host deployment, VMM uses a virtual hard disk that you've created and stored in the library.<br/><br/> You don't need to configure settings on the PXE response tab. VMM provides its own PXE provider.
**Permissions** | When you add a PXE server, you must specify account credentials for an account that has local administrator permissions on the PXE server. You can enter a user name and password or specify a Run As account. You can create the RunAs account before you begin, or during deployment.


### Virtual disk and template requirements

**Prerequisite** | **Details**
--- | ---
**Virtual hard disk** | Make sure you have a generalized virtual hard disk in a VMM library share. It should be running Windows Server 2012 R2 or later.<br/><br/> We recommend that for production servers, you use a fixed disk (.vhd or .vhdx file format) to increase performance and to help protect user data.<br/><br/> Make sure you have a generalized virtual hard disk in a VMM library share. It should be running Windows Server 2012 R2 or later.
**Dynamic disk** | When you create a physical computer profile, VMM converts a dynamic disk to a fixed disk.
**Custom drivers** | If you plan to assign custom drivers to a physical computer profile, you add them to a VMM library share in one or more folders with a .CR (custom resources) extension. VMM recognizes them as custom resources.
**Answer file** | Like custom resources, if you want a physical computer profile to include references to an answer file (Unattend.xml file), create the answer file and add it to a VMM library share before you start deployment. For example, you might want to create an answer file to enable Remote Desktop Services and place it on a library share. Then you can select that file when you configure a physical computer profile.
**RDS** | If you use Remote Desktop Services (RDS) to manage servers, we recommend that you enable the RDS connections in the image. You can also enable RDS by using an answer file in the physical computer profile.
**Logical networks** | If you have already configured logical networks or logical switches in VMM, you can include those configurations in the physical computer profile.<br/><br/>To include static IP addressing controlled through a logical network in a physical computer profile configure the logical network. The logical network must include at least one network site and static IP address pool.<br/><br/>The network site must also be available to the host group or to a parent host group where you want to assign the hosts that you will be creating from bare metal.
**Logical switch** | To use a logical switch, install all necessary virtual switch extensions and extension providers, and create the switch before you create the physical computer profile.<br/><br/> In the logical switch, as a best practice, include one or more port classifications for the virtual ports.<br/><br/> To apply a logical switch to physical adapters in a physicl computer profile, make sure that you have installed the intended number of NICs on the physical computer. </br><br/>  

## Deployment steps

1. **Before you start**: Verify the prerequisites above before you start.
2. **Prepare physical computer**-Set up the BIOS on each physical computer to support virtualization.
2. **Prepare the PXE server environment**:  Add the PXE server to the VMM fabric.
3. **Add driver files**: Add driver files to the VMM library if you want to use custom drivers.
4. **Create profile**: Create a profile for the physical computers.
4. **Create the cluster**: Run the Create Clustered File Server Wizard to discover the physical computers, configure the cluster, and start the cluster deployment. The physical computers boot from a customized Windows PE image on the PXE server. The Failover Cluster and File Server roles are enable. After the cluster is created the Scale-Out File Server role is enabled. The computer is then restarted.
5. **Add nodes to SOFS cluster**: After you've provisioned the nodes you can create a new cluster with them, or add them to an existing one.




## Prepare physical computers

Prepare each computer to support virtualization, as follows:

1. Set the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device.
2. Configure the log on credentials and IP address settings for the BMC on each computer.
3. If your environment has multiple DNS servers, where replication may take some time, we strongly recommend that you create DNS entries for the computer names that will be assigned to the physical computers, and allow time for DNS replication to occur. Otherwise, deployment of the computers may fail.



## Add a PXE server to the VMM fabric

1. Click **Fabric** > **Servers** > **Home** > **Add** > **Add Resources** > **PXE Server**.
2. In **Computer name** specify the PXE server name.
3. Add the credentials for an account that has local administrator permissions on the PXE server. You can specify an existing Run As account, or create a new account. Manually enter user credentials in the format domain_name\user_name. Then click **Add**.
4. In **Jobs**, verify that the job status is **Completed**, and close the dialog box. The job sets up the new PXE server, installs the VMM agent on the PXE server, imports a new Windows Preinstallation Environment (Windows PE) image, and adds the machine account to VMM for the PXE server.
5. Verify that the PXE server is added in **Fabric** > **Servers** > **PXE Servers**. The agent status should be **Responding**.

## Add custom resources to the library

If you plan to assign custom drivers, the driver files must exist in the library. You can tag the drivers in the library, so that you can later filter them by tag.  After files are added, when you configure a physical computer profile, you can specify the driver files. VMM installs the specified drivers when it installs the operating system on a physical computer.

In the physical computer profile, you can select to filter the drivers by tags, or you can select to filter drivers with matching Plug and Play (PnP) IDs on the physical computer. If you select to filter the drivers by tags, VMM determines the drivers to apply by matching the tags that you assign to the drivers in the library to the tags that you assign in the profile. If you select to filter drivers with matching PnP IDs, you don't need to assign custom tags.


1. Locate a driver package that you want to add to the library.
2. In the library share that is located on the library server that is associated with the group where you want to deploy the physical computers, create a folder to store the drivers, and then copy the driver package to the folder.
3. We strongly recommend that you create a separate folder for each driver package, and that you do not mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the VMM library server will not discover those resources. Also, when you delete an .inf driver package from the library, VMM deletes the entire folder where the driver .inf file resides.
4. In the VMM console > **Library** > **Library Servers**, expand the library server where the share is located, right-click the share, and then click **Refresh**. After the library refreshes, the folder should appear.
5. Assign tags if required. In **Library**, expand the folder that you created to store the drivers, and click the folder that contains the driver package.
6. In the **Physical Library Objects**, right-click the driver .inf file, and then click **Properties**.
7. In the **Driver File Name Properties** > **Custom tags**, enter custom tags separated by a semi-colon, or click **Select** to assign available tags or to create and assign new ones. If you click **Select**, and then click **New Tag**, you can change the name of the tag after you click **OK**. For example, if you added a network adapter driver file, you could create a tag that is named ServerModel NetworkAdapterModel, where ServerModel is the server model and NetworkAdapterModel is the network adapter model.

## Create a physical computer profile

Before you start, determine whether the physical computers use Extensible Firmware Interface (EFI) or BIOS. If you have both,  create a separate profile for each type.

1. Click **Library** > **Home** > **Create** > **Physical Computer Profile**.
2. In the **New Physical Computer Profiles Wizard** > **Profile Description** type in a name and description and select **VM host**.
3. In **OS Image** > **Virtual hard disk file** > **Browse**, click the generalized virtual hard disk that you added to the library share. By default, if the disk is dynamic VMM converts it to a fixed disk during host deployment. We recommend that for production servers you use a fixed disk to increase performance and help protect user data.
4. In **Hardware Configuration** > **Management NIC** select the network adapter you'll use to communicate with VMM and whether to use DHCP or a static address. If you want to use Consistent Device Naming (CDN) for the adapter or configure logical switches and ports click **Physical Properties**. Click **Add** to add the adapter.
5. In **Disk** specify the partitioning scheme for the first disk. You can use GPT if the physical computer profile is EFI. In **Partition Information** select the volume label, whether to use all remaining free space or a specific size, and whether to designate the partition as the boot partition. You can also add a new disk or partition. During deployment VMM will copy the virtual hard disk file to the boot partition and automatically create a system partition on the same disk.
6. In **Driver filter** filter the drivers that will be applied to the operating system during host deployment.  You can filter by Plug and Play ID or by specific tags. If you select to filter drivers with matching tags make sure you've added driver files to the library and assigned corresponding tags.
7. In **OS Configuration** specify the domain that the Hyper-V host or cluster should join, specify local admin credentials and identity information. Add the product key for installation, and set the time zone. In GUIRunOnce you can specify one or more commands that will run when the user logs on to the Hyper-V host for the first time.
8. In **Host Settings** specify the path of the host to store the files that are associated with virtual machines placed on the host. Don't specify drive C because it's not available for placement. If you don't specify a path VMM placement will determine the most suitable location.
9. In **Summary** verify the settings. Wait until Jobs shows a status of completed, and then verify the profile in **Library** > **Profiles** > **Physical Computer Profiles**.

## Provision a Scale-Out File Server cluster from bare metal

The Create Clustered File Server Wizard does the following:

1. Discovers the physical computers through out-of-band management
2. Deploys the Windows Server operating system image on the computers by using the physical computer profile (if configured to do so)
3. Enables the file server role on the computers
4. Enables the Scale-Out File Server role on the cluster
5. Adds the provisioned computers as a Scale-Out File Server cluster under VMM management

Run the wizard:

1. Click **Fabric** > **Servers** > **Home** > **Create** > **File Server Cluster**.
2. In the **Create Clustered File Server Wizard** > **General** type in a cluster name, file server name, and cluster IP addresses if needed.
3. In **Resource Type** select the option to provision bare-metal computers. Select the physical computer profile and click **Next**.
4. In **Credentials and Protocols** click **Browse** next to the Run As account and choose the account with permissions to access the BMC. In the **Protocol** list click the out-of-band management protocol you want to use for discovery. If you want to use DCMI click **Intelligent Platform Management Interface (IPMI)**. DCMI 1.0 isn't listed but it is supported. Make sure you use the latest version of firmware for the BMC model.
5. In **Discovery Scope** specify the IP address scope that includes the IP addresses of the BMCs. You can add a single address, a subnet, or range.
6. In **Target Resources** select the computers you want to provision, allow time for deep discovery, and click items to review and modify information. Note that if the number of physical network adapters doesn't match the number of physical adapters defined in the computer profile you'll need to add the missing information. If you don't want to deploy a computer immediately you can select its BMC IP address and click **Remove**.
7. In **Deployment Customization** configure the settings and when there are no more warnings about missing information click **Next**.

	- **DHCP**: If your physical computer profile uses DHCP click an BMC IP address and type in a computer name. Decide whether to skip the AD check. If you do the check deployment will continue if the computer account exists. Click the entry for each BMC IP address.
	- **Static**: If the profile uses static IP addresses for each BMC IP address, type in a MAC address of the computer's network adapter that's used to communicate with VMM. Click the logical network you want to use. The default logical network is the one indicated in the profile. Click the IP subnet you want to use. The subnet list is scope to what's defined for the logical network in the associated network sites. You should select the IP subnet that corresponds to the physical location in which you're deploying the server and the network to which the adapter is connected. you can automatically assign an IP address or assign a specific address.
8. In **Summary**, confirm the settings and click **Finish**. To confirm the cluster was added, click **Fabric** > **Storage** > **File Servers**.
