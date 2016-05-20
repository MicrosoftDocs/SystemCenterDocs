---
title: Overview: creating Scale-Out File Servers from bare metal in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad4b7faa-26fb-4f3f-849e-e563162956cf
---
# Overview: creating Scale-Out File Servers from bare metal in VMM
The procedures in this section describe how to use [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] to discover physical computers \(bare\-metal computers\) on the network, automatically install one of the operating systems listed in this topic, and provision the computers into managed Scale\-Out File Servers.

## <a name="BKMK_workflow"></a>Workflow and deployment process
The following sequence describes the workflow and deployment process for provisioning bare\-metal computers into Scale\-Out File Servers.

The following sequences describes the workflow and deployment process for provisioning bare\-metal computers into managed Hyper\-V hosts or host clusters. The workflow has two main parts:

-   [1. Prepare the computers and the VMM environment](#BKMK_Prep)

-   [2. Run the appropriate wizard and scripts](#BKMK_Wiz)

### <a name="BKMK_Prep"></a>1. Prepare the computers and the[!INCLUDE[vmm12short](Token/vmm12short_md.md)] environment

1.  Perform initial configuration of the physical computers, including:

    -   Configuring the basic input\/output system \(BIOS\) to support virtualization.

    -   Setting the BIOS boot order to boot from a Pre\-Boot Execution Environment \(PXE\)\-enabled network adapter as the first device.

    -   Configuring the logon credentials and IP address settings for the BMC on each computer.

    For more information, see [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md).

2.  Create Domain Name System \(DNS\) entries and Active Directory computer accounts for the computer names that will be provisioned, and allow time for DNS replication to occur.

    This step is not required, but it is strongly recommended in an environment where you have multiple DNS servers, where DNS replication may take some time.

3.  Prepare the PXE server environment, and add the PXE server to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management, as described in [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md) and [How to add a PXE server to VMM](How-to-add-a-PXE-server-to-VMM.md).

4.  Add the required resources to the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] library.

    These resources include a generalized virtual hard disk with an appropriate operating system \(as listed in [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)\) that will be used as the base image, and optional driver files to add to the operating system during installation.

5.  In the library, create one or more physical computer profiles that include:

    -   Configuration settings.

    -   Location of the operating system image.

    -   Operating system configuration settings.

    For more information, see [How to create a physical computer profile to provision hosts or host cluster nodes from bare metal in VMM](How-to-create-a-physical-computer-profile-to-provision-hosts-or-host-cluster-nodes-from-bare-metal-in-VMM.md).

### <a name="BKMK_Wiz"></a>2. Run the wizard and scripts

1.  Run the  Create Scale\-Out File Server Wizard to do the following:

    -   Discover the physical computers.

    -   Configure settings such as the cluster name.

    -   Configure custom deployment settings.

    -   Start deploying the Scale\-Out File Server.

    For more information, see [How to deploy a Scale-Out File Server from bare metal in VMM](How-to-deploy-a-Scale-Out-File-Server-from-bare-metal-in-VMM.md).

2.  During the deployment process, the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server restarts the physical computers.

    The management servers restarts the computers by issuing “Power Off” and “Power On” commands to the Baseboard Management Controller \(BMC\) using out\-of\-band management. When the physical computers restart, the PXE server responds to the boot requests from the physical computers.

3.  The physical computers boot from a customized Windows Preinstallation Environment \(Windows PE\) image on the Pre\-boot execution environment \(PXE\) server.

    On each computer, the Windows PE agent:

    -   Prepares the computer.

    -   When necessary, configures the hardware.

    -   Downloads the operating system image \(.vhd or .vhdx file\) together with any specified driver files from the library.

    -   Applies the drivers to the operating system image.

4.  The management server installs the following Windows Server roles and features:

    -   Failover cluster feature.

    -   File server role.

    After the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server configures the cluster nodes, it creates the cluster.

5.  The [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server installs the Scale\-Out File Server role on the new cluster.

6.  The [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server runs any post\-deployment scripts, restarting the computers as specified by the scripts.

7.  At the end of the deployment process, the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] management server restarts the computers.

8.  You can now configure storage pools and file shares on the Scale\-Out File Server as described in the section [Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

## <a name="BKMK_example"></a>Example naming overview
The example names in this section are intended to demonstrate the concepts used when provisioning bare\-metal computers in [!INCLUDE[vmm12short](Token/vmm12short_md.md)].

The following table summarizes the example names that could be used in this scenario. Some of these names are also used in examples in procedures in this section.

> [!NOTE]
> The example resource names and configuration are intended to demonstrate the concepts. We recommend that you adapt them to your test environment.

|Resource|Example of resource names|
|------------|-----------------------------|
|Node names that are assigned to the physical computers|**SOFSNode05.contoso.com**<br /><br />**SOFSNode06.contoso.com**|
|Cluster name|**SOFSClus01.contoso.com**|
|Scale\-Out File Server name|**SOFSClus01**|
|PXE server \(provided through Windows Deployment Services\)|**PXEServer01.constoso.com**|
|Run As accounts|**PXE Administrator**<br /><br />**Add Physical Host**<br /><br />**BMC Administrator**|
|Logical network|**Management** \(for use with a network site that defines a static IP pool\) **Note:** You can also use DHCP.|
|Physical computer profiles|**WS12Ent SOFSNode \- Static**<br /><br />**WS12Ent SOFSNode \- DHCP**|

## See Also
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


