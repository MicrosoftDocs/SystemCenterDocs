---
title: Overview: creating hosts or host clusters from bare metal with VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7c94f0d-67f1-4c79-8bb0-b9b7fe72c236
---
# Overview: creating hosts or host clusters from bare metal with VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

The procedures in this section describe how to use Virtual Machine Manager (VMM) to discover physical computers (bare-metal computers) on the network, automatically install one of the operating systems listed in this topic, and provision the computers into managed Hyper-V hosts or host clusters.

## Video overview of host provisioning
View the video overview here: [Quickly create multiple Hyper-V hosts in Virtual Machine Manager](http://channel9.msdn.com/blogs/System-Center-Help-Videos/Quickly-create-multiple-Hyper-V-hosts-in-Virtual-Machine-Manager)

The following sections provide more detail about the process shown in the video:

-   [Workflow and deployment process](Overview--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_workflow)

-   [Example scenario overview](Overview--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_example)

## <a name="BKMK_workflow"></a>Workflow and deployment process
The following sequences describes the workflow and deployment process for provisioning bare-metal computers into managed Hyper-V hosts or host clusters. The workflow has two main parts:

-   [1. Prepare the computers and the VMM environment](#BKMK_Prep)

-   [2. Run the appropriate wizard and scripts](#BKMK_Wiz)

### <a name="BKMK_Prep"></a>1. Prepare the computers and the VMM environment

1.  Perform initial configuration of the physical computers, including:

    -   Configuring the basic input/output system (BIOS) to support virtualization.

    -   Setting the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device.

    -   Configuring the logon credentials and IP address settings for the BMC on each computer.

    For more information, see [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

2.  Create Domain Name System (DNS) entries and Active Directory computer accounts for the computer names that will be provisioned, and allow time for DNS replication to occur.

    This step is not required, but it is strongly recommended in an environment where you have multiple DNS servers, where DNS replication may take some time.

3.  Prepare the PXE server environment, and add the PXE server to VMM management, as described in [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md) and [How to add a PXE server to VMM](How-to-add-a-PXE-server-to-VMM.md).

4.  Add the required resources to the VMM library.

    These resources include a generalized virtual hard disk with an appropriate operating system (as listed in [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md)) that will be used as the base image, and optional driver files to add to the operating system during installation.

5.  In the library, create one or more physical computer profiles that include:

    -   Configuration settings.

    -   Location of the operating system image.

    -   Operating system configuration settings.

    For more information, see [How to create a physical computer profile to provision hosts or host cluster nodes from bare metal in VMM](How-to-create-a-physical-computer-profile-to-provision-hosts-or-host-cluster-nodes-from-bare-metal-in-VMM.md).

### <a name="BKMK_Wiz"></a>2. Run the appropriate wizard and scripts

1.  Run the appropriate wizard:

    |To create a Hyper-V host, run the Add Resources Wizard|To create a Hyper-V host cluster, run the Create Hyper-V Cluster Wizard|
    |-----------------------------------------------------------|-----------------------------------------------------------------------------|
    |Use the wizard to:<br /><br />-   Discover the physical computers.<br />-   Configure settings such as the host group and the physical computer profile to use.<br />-   Configure custom deployment settings.<br />-   Start deploying the operating system and Hyper-V.<br /><br />For more information, see [How to deploy Hyper-V hosts from bare metal in VMM](How-to-deploy-Hyper-V-hosts-from-bare-metal-in-VMM.md).|Use the wizard to:<br /><br />-   Discover the physical computers.<br />-   Configure settings such as the host group and the physical computer profile to use.<br />-   Configure custom deployment settings.<br />-   Start deploying the host cluster.<br /><br />For more information, see [How to deploy a host cluster from bare metal in VMM](How-to-deploy-a-host-cluster-from-bare-metal-in-VMM.md).|

2.  During the deployment process (host or host cluster), the VMM management server restarts the physical computers.

    The management servers restarts the computers by issuing “Power Off” and “Power On” commands to the Baseboard Management Controller (BMC) using out-of-band management. When the physical computers restart, the PXE server responds to the boot requests from the physical computers.

3.  The physical computers boot from a customized Windows Preinstallation Environment (Windows PE) image on the Pre-boot execution environment (PXE) server.

    On each computer, the Windows PE agent:

    -   Prepares the computer.

    -   When necessary, configures the hardware.

    -   Downloads the operating system image (.vhd or .vhdx file) together with any specified driver files from the library.

    -   Applies the drivers to the operating system image.

4.  The management server installs the following Windows Server roles and features, as appropriate:

    |Hyper-V hosts|Hyper-V host clusters|
    |------------------|--------------------------|
    |Hyper-V role.|-   Hyper-V role.<br />-   Failover cluster feature.<br />-   Multipath I/O (MPIO) feature.<br /><br />After the VMM management server configures the cluster nodes, it creates the cluster.|

5.  The VMM management server runs any post-deployment scripts, restarting the computers as specified by the scripts.

6.  At the end of the deployment process, the VMM management server restarts the computer or computers.

## <a name="BKMK_example"></a>Example naming overview
The example names in this section are intended to demonstrate the concepts used when provisioning bare-metal computers in VMM.

The following table summarizes the example names that could be used in this scenario. Some of these names are also used in examples in procedures in this section.

> [!NOTE]
> The example resource names and configuration are intended to demonstrate the concepts. We recommend that you adapt them to your test environment.

|Resource|Example of resource names|
|------------|-----------------------------|
|Host names that are assigned to the physical computers|**HyperVHost05.contoso.com**<br /><br />**HyperVHost06.contoso.com**<br /><br />If a host cluster was created, it could be called **HVHostClus01.contoso.com**.|
|Target host group|**New York\Tier0_NY**|
|PXE server (provided through Windows Deployment Services)|**PXEServer01.constoso.com**|
|Run As accounts|**PXE Administrator**<br /><br />**Add Physical Host**<br /><br />**BMC Administrator**|
|Logical network|**Management** (for use with a network site that defines a static IP pool) **Note:** You can also use DHCP.|
|Physical computer profiles|**WS12Ent Hyper-V Hosts - Static**<br /><br />**WS12Ent Hyper-V Hosts - DHCP**|

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



