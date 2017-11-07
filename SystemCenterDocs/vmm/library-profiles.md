---
ms.assetid: 5354d214-c317-47e9-b1dc-6108885ea832
title: Add profiles to the VMM library
description: This article provides guidance for adding profiles to the library in the VMM compute fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Add profiles to the VMM library



Use this article to learn about System Center - Virtual Machine Manager (VMM) profiles, and how to add them to the VMM library.

A VMM profile contains settings that are used when you create a new virtual machine or virtual machine template. Profiles make deployment easier by helping you to quickly create VMs with consistent settings. Profiles can be used to restrict the settings that are available to self-service users who create new VMs.

**Profile** | **Details** | **Used for VM templates** | **Used for service templates**
--- | --- | --- | ---
**Hardware profile** | Defines hardware configuration settings, such as CPU, memory, network adapters, a video adapter, a DVD drive, and the VM priority when resources are allocated on a VM host. | Yes | No
**Guest operating system profile** | Defines operating system configuration settings that are applied to a VM, including the type of operating system, the computer name, administrator password, domain name, product key, time zone, answer file, and RunOnce file. | Yes | No
**Application profile** | Provides instructions for installing an application. VMM supports multiple mechanisms for application deployment. Two of these mechanisms are for specific application packaging technologies: data\-tier applications \(DAC\) and WebDeploy (MSDeploy). A third mechanism enables you to install any application by running a script. You can use scripts that are created for Windows Installer \(MSI\), Setup.exe installation programs, Windows PowerShell Desired State Configuration (DSC), Puppet software, and Chef software. | No | Yes
**SQL Server profile** | Provides instructions for customizing an instance of Microsoft SQL Server for a SQL Server DAC when a virtual machine is deployed as part of a service.| No | Yes
**Capability profile** | Defines limits and capabilities for a specific set of resources, for example settings for network adapters, processor ranges, and memory. Capability profiles are used for hardware profiles or in cloud deployment. For example, you could configure a private cloud and assign it a Hyper-V capability profile that requires all resources to the highly available. In this example, you need to set up library resources such as hardware profiles to align with the capability. [To learn more review,](https://social.technet.microsoft.com/wiki/contents/articles/4149.capability-profiles-in-scvmm-2012.aspx) | Yes | Yes
**Physical computer profile** | Defines settings used to provision servers | No | No

## Create a hardware profile

1. In the VMM console click > **Library** > **Create** > **Hardware Profiles**.
2. In **New Hardware Profile** > **General**, type in a profile name. You can create a hardware profile with the default settings** but you probably want to tailor them. In **Hardware Profile** you can specify the hardware settings.
3. In **Compatibility** you can specify that a capability profile should be assigned to the hardware profile. Remember, capability profiles help limit available options when you're creating a new VM.
4. In **General** you can define how many virtual processors to assign to the VM. You can specify memory. startup and dynamic memory range. Startup specifies the memory that is assigned to the VM during startup. After startup this memory can be reclaimed back from the VM in accordance with the minimum memory settings.
5. In **Bus Configuration** you add and remove hardware that supports storage device.
6. In **Network Adapters**, you specify the number of network adapters in the VM, whether they'll have a static IP address or an address allocated from a pool, the MAC address and port profile. The port profile can be used to control how bandwidth is used on the adapters.
7. In **Advanced** you can specify high availability and performance settings. In **Availability** specify whether the VM should be highly available in deployed in a cluster. In **BIOS** select the order of virtual device and when **Num Lock** is enabled for password entry. In **CPU Priority** specify relative priority of CPU usage for the VM. If you set to High, the VM has more access to resources that those set to Low. In **Virtual NUMA** specify when the VM can use [virtual NUMA](vm-settings.md#configure-virtual-numa) In **Memory Weight** specify the relative memory priority for the VM.
8. After you've finished creating the hardware profile, you can right-click it to configure additional properties. In **Dependencies** you see any dependencies for the profile. For example if a library-based file is required we'd see it here. In **Access** you can see the roles or users who have permissions to use this profile. In **Validation Errors** you can check for errors.
9. After you've created the hardware profile, you can use it when you configure a virtual machine template, or create a virtual machine. You can select a complete hardware profile, or select it and then tweak settings for the individual VM or template.

## Create a guest OS profile

1. In the VMM console click > **Library** > **Create** > **Guest OS Profiles**.
2. In **New Guest OS Profile** > **General**, type in a profile name. In **Guest OS Profile** you specify the OS settings.
3. In **General Settings** > **Operating System**, specify the VM operating system. In **Identity Information**, specify the actual machine name of the VM. You probably want a unique name, so that you can specify a wildcard to generate a new name for each VM. You can also use characters ### to set an increasing numeric value. For example, if you type in ContosoVM-## it generates machines named ContosoVM-01, ContosoVM-02 etc. In **Admin Password** specify local admin permissions require a password. you can use the predefined Run As account. In **Product Key** type in the key for the OS installation. If you add an answer file under **Scripts**, you can select the **Product key provided by answer file** settings. In **Time Zone** specify the time location for the VM.
4. In **Roles and Features** specify what should be installed on the VM. Note that this setting is only used for the profile is used in a VM template which is then used in a service template.
5. In **Networking** specify domain settings for the VM and credentials to use for joining the domain.
6. In **Scripts**, specify any scripts you want to use for the VM. Scripts must be located on the library share. For example an installation answer file. The **GUIRunOnce** option allows you to run a script the first time a user logs on to the VM.
7. After you've created the guest OS profile you can right-click it to configure additional properties. In **Dependencies** you see any dependencies for the profile. For example Run As accounts. In **Access** you see the roles or users who have permissions to use this profile.
8. After you've created the hardware profile, you can use it when you configure a virtual machine template or create a VM.

## Create an application profile

1. In the VMM console click > **Library** > **Create** > **Application Profiles**.
2. In **New Application Profile** > **General**, type in a profile name. In **Application Configuration** you can specify the app settings.
3. In **Application Configuration** > **OS Compatibility**, specify the guest operating systems that are compatible with the application profile.
4. Click **Add** and select the type of application or script that you want to apply to the profile. To deploy any app type select **General**. To deploy SQL Server DAC packages or script, select **SQL Server Application Host** so that you can add packages and scripts to the profile. To deploy Web applications, click **Web Application Host** so that you can add Web Deploy packages and scripts to the profile.
5. If you selected **General** you can add more than one more of application or script to the profile.
6. For applications you can specify settings such as certificate, ports, and folders. You can also specify that deployment of the app should be managed by a script. You can specify the script name, and specify when it should run.
7. Select **Scripts** to add an unlimited number of scripts and properties such as parameters and security settings. For example you can configure script to create a guest cluster out of multiple VMs deployed by VMM. For example, you can specify that one script to run at Creation: First VM (to form the cluster on the first virtual machine) and a different script to run at Creation: VMs After First (to add additional virtual machines to the cluster).
5. After you're done can verify that the profile was created in **Library** > **Profiles** > **Application Profiles**.
6. You use application profiles in service templates. For example you could create a number of VM templates with  hardware and OS profiles. Then you create a service template that includes those VM templates, and the application profiles, to create a set of VMs that are configured and deployed together as a single entity.

## Create a SQL Server profile

1. In the VMM console click > **Library** > **Create** > **SQL Server Profiles**.
2. In **New SQL Server Profile** > **General** type in a profile name. In **SQL Server Configuration** you can specify the app settings.
3. In **Application Configuration** > **Add** > **SQL Server Deployment**. A SQL Server deployment corresponds to a single instances of SQL Server. If you want multiple instance of SQL Server on the same VM you need to create multiple deployments.
4. In **SQL Server Deployment** click **Deployment 1** and specify the deployment name, the SQL Server instance details. The RunAs account is optional, the VMM service account is used if you don't specify it.
5. In **Configuration** type in the path to the SQL Server installation file (setup.exe) and the SQL Server admins.
6. In **Service Account** specify which accounts to use.

## Create a capability profile

The exact settings for a capability profile depends on the profile in use. As an example let's configure the Hyper-V capability profile to specify high availability for resources used in a private VMM cloud.

1. In the VMM console, click > **Library** > **Create** > **Capability Profiles**.
2. In **Create Capability Profile** > **General**, type in a profile name. In **Capabilities** you specify the profile settings.
3. In **Capabilities** > **Fabric Compatibility** select **Hyper-V virtualization host**. You could also elect to set up a custom capability profile.
4. Set up the hardware configuration settings for the profile. The settings are similar to those used in a [hardware profile](#create-a-hardware-profile). However, in capability profiles these settings represent limits rather than exact values.
5. In **Advanced** > **Availability**, select **Highly available VM mode** > **Use default** > **Required**.
6. Complete the wizard. After you've created the profile you can select and enable it in **VMs and Services** > cloud name > **Properties** > **Capability Profiles**.
7. Remember that all of the other profiles and templates used for VMs in the cloud need to match the capability profile requirements and the high availability setting.

## Create a physical computer profile

VMM can are used to provision physical computers into Hyper-V hosts or into a scale-out file server (SOFS). When you're provisioning physical computers you can use a physical computer profile to specify settings for the machine. Create a physical computer profile as follows:

1. In the VMM console click > **Library** > **Create** > **Physical Computer Profile**.
2. In **New Physical Computer Profile** > **Profile Definition** type in a profile name and description.
3. In **OS Image** select a virtual hard disk from the library share. It should be running Windows Server 2012 R2 or later. To create the hard disk you can create a VM, install the guest operating system, and then use Sysprep with **/generalize** and **/oobe**. If the disk is dynamic VMM converts it to a fixed disk  during deployment. We recommend that you use a fixed disk type to help protect user data and increase performance.
4. In **Hardware Configuration** set up network adapters, disks and partitions, and any drivers.
5. In **Network Adapters** click **Connectivity Properties** to set up consistent device naming (CDN) for the adapter. Specify whether to allocate an IP address with DHCP or from a static pool. If it's a physical network adapter connected to a logical switch this option isn't available.
6. In **Disk** specify the partitioning scheme for the first disk. Select Master Boot Record (MBR) for BIO. or GUID Partition Table (GPT) for EFI. Specify a volume label, what free disk space to use, and what to designate as the boot partition. VMM copies the .vhd or .vhdx file to the boot partition and automatically creates a system partition on the same disk.
5. In Driver filter specify the driver files to be applied to the operating system during deployment. You can filter drives with plug and play IDs or with specific tags. With the tag option you need to add driver files to the library and assign corresponding tags to the library share before deployment.
3. In **OS Configuration** set up the domain, the password for the local admin, name and organization, product team, time zone, and an answer file for additional setup options. In GUIRunOnce you can specify commands or scripts that should run the first time a user signs into the machine.
4. Verify the settings in **Summary** and click **Finish**. You can check that the physical computer profile in **Library** > **Profiles** > **Physical Computer Profiles**.

## Next steps

Learn about creating [VM templates](library-vm-templates.md) and [service templates](library-resources.md) in the VMM library, and adding profiles to them.
