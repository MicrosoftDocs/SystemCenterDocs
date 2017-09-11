---
ms.assetid: 350b385c-dc51-421c-a954-623a7fd416c2
title: Provision a Hyper-V host or cluster from bare metal computers
description: This article explains how to provision Hyper-V hosts or clusters from bare metal computers in the VMM fabric.
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  09/09/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Provision a Hyper-V host or cluster from bare metal computers

>Applies To: System Center 2016 - Virtual Machine Manager

Use this article to provision a Hyper-V host or cluster from bare metal computers with nothing installed on them, in the System Center 2016 - Virtual Machine Manager (VMM) fabric.

In addition to adding existing Windows servers to the fabric as Hyper-V hosts and clusters, VMM can discover physical bare-metal machines, automatically install an operating system, and provision them as Hyper-V server hosts  and clusters.

Here's how you do this:

1. **Verify prerequisites**-Make sure you have all the prerequisites before you start.
2. **Initial configuration**-Set up the BIOS on the machine to support virtualization, setting the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device, and configuring the logon credentials and IP address settings for the BMC on each computer. You need to create DNS entries and Active Directory account for the machine names, and we recommend you allow time for DNS replication to occur.
2. **Prepare the PXE server environment**:  Add the PXE server to VMM management, as described in Prerequisites: creating hosts, host clusters, or Scale-Out File Server clusters from bare metal in VMM and How to add a PXE server to VMM.
3. **Add resources to VMM library**: Add resources that include a generalized virtual hard disk with an appropriate operating system (as listed in Prerequisites: creating hosts, host clusters, or Scale-Out File Server clusters from bare metal in VMM) to use as the base image, and optional driver files to add to the operating system during installation.
4. **Create profiles**: In the library, create one or more physical computer profiles. These profiles include configuration settings, such as the location of the operating system image, and hardware and operating system configuration settings.
5. **Create Hyper-V host or cluster**: You run different wizards depending on whether you want to set up a standalone host or cluster.


## Before you start
Ensure the following prerequisites:

**Component** | **Prerequisite** | **Details**
--- | --- | ---
**Physical computer** | Support for discovery | Each physical computer must have a baseboard management controller (BMC) installed that enables out-of-band management. Through a BMC, you can access the computer remotely, independent of the operating system, and control system functions such as the ability to turn the computer off or on. BMC requirements:<br/><br/> The BMCs must use one of the supported out-of-band management protocols, and the management protocol must be enabled in the BMC settings.<br/><br/> The supported protocols are: Intelligent Platform Management Interface (IPMI) versions 1.5 or 2.0; Data Center Management Interface (DCMI) version 1.0; System Management Architecture for Server Hardware (SMASH) version 1.0 over WS-Management (WS-Man); custom protocols such as Integrated Lights-Out (iLO)<br/><br/> The BMCs should use the latest version of firmware for the BMC model.<br/><br/> The BMCs must be configured with logon credentials and must use either static IP addressing or DHCP. If you use DHCP, we recommend that you configure DHCP to assign a constant IP address to each BMC, for example by using DHCP reservations.<br/><br/> The VMM management server must be able to access the network segment on which the BMCs are configured.
**Physical computer** | Hyper-V role requirements | Computer that supports the Hyper-V role, must use x64-based processors and have the appropriate basic input/output system (BIOS) settings enabled.
**Physical computers** | DNS | If your environment has multiple Domain Name System (DNS) servers, where DNS replication may take some time, we strongly recommend that you create DNS entries for the computer names that are assigned to the physical computers, and allow time for DNS replication to occur. Otherwise, deployment of the computers may fail.
**Physical computer** | BIOS/EFI | Determine whether the computers use Extensible Firmware Interface (EFI) or BIOS. If you have computers of each type, you must create a separate profile for each type.
**Physical computers** | Operating system | You can add a Windows Server 2016 node to a Windows Server 2012 R2 cluster, subject to the requirements specified previously; however, you cannot add a Windows Server 2012 R2 node to a Windows Server 2016 cluster.
**PXE server** | Deployment requirements | You must have a PXE server configured with Windows Deployment Services.<br/><br/> If you have an existing PXE server in your environment configured with Windows Deployment Services, you can add that server to VMM. Then you can use it for provisioning in VMM (and VMM recognizes only the resulting servers). All other requests continues to be handled by the PXE server according to how it is configured.<br/><br/> If you don't have an existing PXE server, you can deploy the Windows Deployment Services role on a server running a supported operating system (Windows Server 2012 R2 or later).<br/><br/>When you install Windows Deployment Services you should install both the Deployment server and Transport server options. Note that you don't need to add images. During host deployment, VMM uses a virtual hard disk that you've created and stored in the library. In addition you don't need to configure settings on the PXE response tab. VMM provides its own PXE provider.<br/><br/> The PXE server must be in the same subnet as the physical computers that you want to provision.<br/><br/> When you add a PXE server, you must specify account credentials for an account that has local administrator permissions on the PXE server. You can enter a user name and password or specify a Run As account. If you want to use a Run As account, you can create the RunAs account before you begin, or during deployment.
**PXE server** | Boot order | On each computer, set the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device.
**Virtual hard disk** | Operating system | Make sure you have a generalized virtual hard disk in a VMM library share. It should be running Windows Server 2012 R2 or later.<br/><br/> We recommend that for production servers, you use a fixed disk (.vhd or .vhdx file format) to increase performance and to help protect user data. Note that by default, when you create a physical computer profile, VMM converts a dynamic disk to a fixed disk.<br/><br/> If you plan to assign customer drivers they must exist in the library.<br/><br/> To create the virtual hard disk, you can create a virtual machine, install the guest operating system, and then use sysprep with the /generalize and the /oobe options.<br/><br/> The operating system on the virtual hard disk that you deploy on hosts or clusters must support the boot from virtual hard disk (VHD) option.<br/><br/> If you use Remote Desktop Services (RDS) to manage servers, we recommend that you enable the RDS connections in the image. You can also enable RDS by using an answer file in the physical computer profile.
**Networking** | Logical networks | If you have already configured logical networks or logical switches in VMM, you can include those configurations in a physical computer profile.<br/><br/> To include a logical switch that you want to apply to physical NICs in a physical computer profile (for hosts or host clusters), you must first take certain steps. Make sure that you have installed the intended number of NICs on the host computer or computers. In addition, before you create the physical computer profile in VMM, create the logical switch.<br/><br/> To include static IP addressing controlled through a logical network in a physical computer profile configure the logical network. The logical network must include at least one network site and static IP address pool. The network site must also be available to the host group or to a parent host group where you want to assign the hosts that you are creating from bare metal.</br><br/> To include a virtual NIC for hosts in a physical computer profile (for hosts or host clusters), you must first take certain steps. Make sure that you have installed the intended number of physical NICs on the computer or computers that are to become hosts. In addition, on the VMM management server, install all necessary virtual switch extensions and extension providers, create at least one VM network, and create a logical switch. In the logical switch, as a best practice, include one or more port classifications for the virtual ports.
**Physical computer profile** | Answer file | If you want a physical computer profile to include references to an answer file (Unattend.xml file) or to custom resources (for example, an application installer that is referenced in post-deployment script commands), create the answer file or obtain the custom resources before deployment, and add them to a VMM library share. Within a library share, place custom resources in one or more folders with a .CR (custom resource) extension. VMM recognizes them as custom resources. For example, you might want to create an answer file to enable Remote Desktop Services and place it on a library share. Then you can select that file when you configure a physical computer profile.<br/><br/> By default when you deploy servers or clusters from bare metal, VMM automatically performs the following (no answer file or post-deployment commands needed): Installs the Hyper-V role for Hyper-V hosts. Installs the Hyper-V role, failover cluster feature, and multipath I/O (MPIO) for Hyper-V clusters.
**Accounts** | You need two Run As accounts.<br/><br/> A Run As account for joining computers to the domain. You can create a Run As account in the Settings workspace.<br/><br/> A Run As account for access to the baseboard management controller (BMC) on each computer.

## Add a PXE server to the VMM fabric

1. Click **Fabric** > **Servers** > **Add** > **Add Resources** > **PXE Server**.
2. In Computer name specify the PXE server name.
3. Add the credentials for an account that has local administrator permissions on the PXE server. You can specify an existing Run As account (or click Create Run As Account to create a new one), manually enter user credentials in the format domain_name\user_name. Click **Add**.
4. In **Jobs** verify that the job status is Completed and close the dialog box. The job sets up the new PXE server, installs the VMM agent on the PXE server, imports a new Windows Preinstallation Environment (Windows PE) image, and adds the machine account for the PXE server to VMM.
5. Verify that the PXE server is added in **Fabric** > **Servers** > **PXE Servers** > **Home** > **Show** > **Fabric Resources** > **PXE Servers**. The agent status should be **Responding**.

## Add and assign driver files

If you plan to assign custom drivers, the driver files must exist in the library. You can tag the drivers in the library, so that you can later filter them by tag.  After files are added, when you configure a physical computer profile, you can specify the driver files. VMM installs the specified drivers when it installs the operating system on a physical computer.

In the physical computer profile, you can select to filter the drivers by tags, or you can select to filter drivers with matching Plug and Play (PnP) IDs on the physical computer. If you select to filter the drivers by tags, VMM determines the drivers to apply by matching the tags that you assign to the drivers in the library to the tags that you assign in the profile. If you select to filter drivers with matching PnP IDs, you don't need to assign custom tags.

1. Locate a driver package that you want to add to the library.
2. In the library share that is located on the library server that is associated with the group where you want to deploy the physical computers, create a folder to store the drivers, and then copy the driver package to the folder.
3. We strongly recommend that you create a separate folder for each driver package, and that you do not mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the VMM library server is unable to discover the resources. Also, when you delete an .inf driver package from the library, VMM deletes the entire folder where the driver .inf file resides.
4. In the VMM console, open the Library workspace. In the **Library** > **Library Servers**, expand the library server where the share is located, right-click the share, and then click **Refresh**. After the library refreshes, the folder that you created to store the drivers appears.
5. Now assign tags if required. In **Library**, expand the folder that you created to store the drivers in the previous procedure, and then click the folder that contains the driver package.
6. In the **Physical Library Objects**, right-click the driver .inf file, and then click **Properties**.
7. In the **Driver File Name Properties** > **Custom tags*,* enter custom tags separated by a semi-colon, or click **Select** to assign available tags or to create and assign new ones. If you click **Select**, and then click **New Tag**, you can change the name of the tag after you click **OK**. For example, if you added a network adapter driver file, you could create a tag that is named ServerModel NetworkAdapterModel, where ServerModel is the server model and NetworkAdapterModel is the network adapter model.

## Create a physical computer profile

1. Click **Library** > **Home** > **Create** > **Physical Computer Profile**.
2. In the **New Physical Computer Profiles Wizard** > **Profile Description**, type in a name and description and select **VM host**.
3. In **OS Image** > **Virtual hard disk file** > **Browse**, click the generalized virtual hard disk that you added to the library share. By default, if the disk is dynamic VMM converts it to a fixed disk during host deployment. We recommend that for production servers you use a fixed disk to increase performance and help protect user data.
4. In **Hardware Configuration** > **Management NIC** select the network adapter used to communicate with VMM and whether to use DHCP or a static address. If you want to use Consistent Device Naming (CDN) for the adapter or configure logical switches and ports click **Physical Properties**. Click **Add** to add the adapter.
5. In **Disk**, specify the partitioning scheme for the first disk. You can use GPT if the physical computer profile is EFI. In **Partition Information**, select the volume label, whether to use all remaining free space or a specific size, and whether to designate the partition as the boot partition. You can also add a new disk or partition. During deployment VMM copies the virtual hard disk file to the boot partition and automatically create a system partition on the same disk.
6. In **Driver filter**, filter the driver filters to be applied to the operating system during host deployment.  You can filter by Plug and Play ID or by specific tags. If you select to filter drivers with matching tags make sure you've added driver files to the library and assigned corresponding tags.
7. In **OS Configuration** specify the domain that the Hyper-V host or cluster should join, specify local admin credentials and identity information. Add the product key for installation, and set the time zone. In GUIRunOnce, specify one or more commands to run when the user logs on to the Hyper-V host for the first time.
8. In **Host Settings** specify the path of the host to store the files that are associated with virtual machines placed on the host. Don't specify drive C because it's not available for placement. If you don't specify a path, VMM placement determines the most suitable location.
9. In **Summary** verify the settings. Wait until Jobs shows a status of completed, and then verify the profile in **Library** > **Profiles** > **Physical Computer Profiles**.

### PCP post deployment settings
After you successfully create and deploy the PCP,  you can configure additional settings such as RDMA, QoS, and SET using the PCP post deployment script.

#### Sample script
Here is the sample script to configure RDMA, SET and QoS.

```powershell
# Install data center bridging
Install-WindowsFeature Data-Center-Bridging

#Enable RDMA, assuming customer chosen switch name for storage as Storage1Switch and Storage2Switch
Enable-NetAdapterRDMA "Storage1Switch"
Enable-NetAdapterRDMA "Storage2Switch"

# set Qos Policy
New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

# Enable net qos flow control
Enable-NetQosFlowControl  -Priority 3

# Disable net qos flow control other than 3
Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

# Enable net adapter qos on all adapters
Enable-NetAdapterQos  -InterfaceAlias "*"

# set qos traffic class
New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 50  -Algorithm ETS

# Install windows feature
Install-WindowsFeature –Name Hyper-V

Install-WindowsFeature –Name RSAT-Hyper-V-Tools

# set net adapter property "encapsulated overhead"
NetAdapterAdvancedProperty -Name "*" -DisplayName "Encapsulated Overhead" -DisplayValue "160"

#disable ipv6
netsh int ipv6 isatap set state disabled

#Configure SET team mapping between virtual network adapter to physical network adapters. (Note: to get names of adapters, use command Get-NetAdapater. For team mapping use command
$physicalAdapters = Get-NetAdapter -Physical
$virtualStorageAdapter1 = Get-VMNetworkAdapter -ManagementOS | Where-Object {$_.Name -eq "Storage1Switch"}
$virtualStorageAdapter1 = Get-VMNetworkAdapter -ManagementOS | Where-Object {$_.Name -eq "Storage2Switch"}

Set-VMNetworkAdapterTeamMapping -ManagementOS -PhysicalNetAdapterName $physicalAdapters[0].Name -VMNetworkAdapterName $virtualStorageAdapter1.Name
Set-VMNetworkAdapterTeamMapping -ManagementOS -PhysicalNetAdapterName $physicalAdapters[1].Name -VMNetworkAdapterName $virtualStorageAdapter2.Name

#Set firewall rules.
[System.String[]]$Alias=@("vEthernet (WssdStorage2)", "vEthernet WssdStorage1)");
$Profile ='Any'
$Name="File and Printer Sharing"
$rules = Get-NetFirewallRule -DisplayGroup $Name

foreach ($rule in $rules)
     {
   		 $rule | Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -  
         LocalAddress Any -RemoteAddress Any
     }

 Set-NetFirewallRule -DisplayGroup $Name -Enabled True -Profile $Profile – InterfaceAlias $Alias
 $Profile='Any'
 $Name=='FPS-LLMNR-In-UDP'
 Set-NetFirewallRule -Name $Name -Enabled True -Profile $Profile
 [System.String[]]$Alias=@("Storage2Switch", "Storage1Switch", "ManagementSwitch");
 $Profile ='Any'
 $Name="Windows Remote Management"
 Set-NetFirewallRule -DisplayGroup $Name -Enabled True -Profile $Profile –InterfaceAlias $Alias

 #Set assurance settings
 reg add HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard /v EnableVirtualizationBasedSecurity /t REG_DWORD /d 1 /f
 reg add HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard /v RequirePlatformSecurityFeatures /t REG_DWORD /d 2 /f
 reg add HKLM\SYSTEM\CurrentControlSet\Control\LSA /v LsaCfgFlags /t REG_DWORD /d 1 /f
 reg add HKLM\SYSTEM\CurrentControlSet\Control\LSA /v DisableRestrictedAdmin /t REG_DWORD /d 0 /f
 ```

## Provision a Hyper-V host from bare metal

When you deploy a Hyper-V host from bare metal, VMM does the following:

1. Discovers the physical computer through out-of-band management.
2. Deploys an operating system image on the computer through the physical computer profile.
3. Enables the Hyper-V role on the computer.
4. Brings the computer under VMM management as a managed Hyper-V host.

Provision as follows:

1. Click **Fabric** > **Servers** > **Home** > **Add** > **Add Resources** > **Hyper-V Hosts and Clusters**.
2. In the **Add Resource Wizard** > **Resource location**, select **Physical computers to be provisioned as virtual machine hosts**.
3. In **Credentials and Protocol** select the Run As account with permissions to access the BMC. In the **Protocol** list, click the out-of-band management protocol that your BMCs use. If you want to use Data Center Management Interface (DCMI), click Intelligent Platform Management Interface (IPMI). Although DCMI 1.0 is not listed, it is supported. Make sure the correct port is selected.
5. In **Discovery Scope**, specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range.
    - If you are provisioning a single computer, you can either specify a single IP address, or specify an IP address range that both starts and ends with the intended IP address. If you specify a single IP address, when you click **Next**, the computer is restarted.
    - If you specify an IP address range, when you click **Next**, information about the computer is displayed, and you can confirm that you specified the computer that you meant to.
6. If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs (identified by IP addresses), and select the ones you want to provision as hosts. If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**.
8. In **Provisioning Options**, click a host group for new Hyper-V hosts. Select the physical computer profile you want to apply.
9. In **Deployment Customization**, review the list of computers again, and provide information for each computer that you want to include.
    - If you see a computer that you don't want to include, select the BMC (identified by IP address) and then click **Remove**.
    - To configure computers click the BMC IP address.
    - Specify a unique computer name, without wildcard characters.
    - Select or clear **Skip Active Directory for this computer name**. The Active Directory check prevents deployment if the computer account already exists. This helps prevent deploying a computer with the same name as an existing computer. Note that if you skip the Active Directory check, and there is an existing computer account in AD DS other than the Run As account that was specified in the physical computer profile, the deployment process fails to join the computer to the domain.
11. For the computer you are configuring, click a network adapter (on the left). You can modify the configuration, or fill in more information (...).
12. You can specify the MAC address of the management NIC (not the BMC) and static IP settings for this network adapter. If you specify an address select a logical network and an IP subnet if applicable.  If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that's within the logical network or its subnet. If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the host and to the network that the adapter is connected to. Otherwise, deployment may fail.
12. Configure the adapter settings for each network adapter. Note that if the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now (for example, if physical hardware needs to be installed or uninstalled), you can select the computer's BMC IP address from the list and then click **Remove**.
13. Repeat the configuration for each BMC IP address in the list. When you have filled in information for all the computers you want to provision, click **Next**.
15. In **Summary**, confirm the settings, and then click **Finish** to deploy the new Hyper-V hosts and bring them under VMM management. Depending on your settings, the **Jobs** dialog box might appear. Make sure that all steps in the job have a status of **Completed**, and then close the dialog box.
16. To confirm that the host was added click **Fabric** > **Servers** > **All Hosts** > host group, and verify that the new Hyper-V host appears in the group.

## Provision a Hyper-V cluster from bare metal

When you deploy a Hyper-V cluster from bare metal VMM does the following:
1. Discovers the physical computers through out-of-band management.
2. Deploys an operating system image on the computers by using the selected physical computer profile.
3. Installs the failover clustering feature, and the Hyper-V role and MPIO feature.
4. Brings the provisioned cluster under VMM management

Provision as follows:

1. Click **Fabric** > **Servers** > **Add** > **Add Resources** > **Hyper-V Hosts and Clusters**.
2. In **General Configuration**, specify a name for the host cluster. Choose a storage configuration if required:
    - For shared storage, click **Storage connected to the cluster using shared SAS, FC, or iSCSI**.
    - For Storage Spaces Direct, click **Disk subsystem directly connected to individual nodes in the cluster**.
3. In **Resource Type** > select **Physical computers to be provisioned**:
    - Specify the administrator Run As account to use for creating the cluster.
    - Select the physical computer profile (which provides the domain name and administrator Run As account for each node).
    - Next to the **BMC Run As** account box, click **Browse**, and select a Run As account that has permissions to access the BMC.
    - In the **Out-of-band management** protocol list, click the protocol that your BMCs use. If you want to use Data Center Management Interface (DCMI), click Intelligent Platform Management Interface (IPMI). Although DCMI 1.0 is not listed, it is supported. Ensure that the correct port is selected.
    - If the **Skip cluster validation** option appears, and you don't need support from Microsoft for this cluster, you can skip validation.
4. In **Discovery Scope**, specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range. Deep discovery provides detailed information about a computer (for example, MAC addresses of network adapters) but restarts the computer, and requires additional time. You can allow or skip deep discovery.
5. If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs (identified by IP addresses), and select the ones you want to include in the cluster.
6. If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**. Allow or skip deep discovery. Deep discovery provides detailed information about a computer (for example, MAC addresses of network adapters) but restarts the computer, and requires additional time. Then click **Next**.
7. In **Deployment Customization** provide information for each computer that you want to include. If you see a computer that you don't want to include, select the BMC (identified by IP address) and then click **Remove**.
    - To configure computers click the BMC IP address. Specify a unique computer name, without wildcard characters.
    - Select or clear **Skip Active Directory for this computer name**. The Active Directory check prevents deployment if the computer account already exists. Note that if you skip the check and there's an existing computer account in AD other than the Run As account that was specified in the physical computer profile, the deployment process fails to join the computer to the domain.
    - For the computer you are configuring, click a network adapter. You can modify the configuration, or fill in more information.
    - You can specify the MAC address of the management NIC (not the BMC) and static IP settings for this network adapter. If you specify an address select a logical network and an IP subnet if applicable.  If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that is in within the logical network or its subnet. If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the host and to the network that the adapter is connected to. Otherwise, deployment may fail.
8. Configure the network adapter settings for each network adapter. Note that if the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now (for example, if physical hardware needs to be installed or uninstalled), you can select the computer's BMC IP address from the list and then click **Remove**.
9. Repeat the configuration for each BMC IP address in the list.
10. When you have filled in needed information for all the computers you want to provision, click Next.
11. In **Summary** confirm the settings, and then click **Finish** to deploy the new Hyper-V hosts and bring them under VMM management. Depending on your settings, the Jobs dialog box might appear. Make sure that all steps in the job have a status of Completed, and then close the dialog box.
12. To confirm that the host was added click **Fabric** > **Servers** > **All Hosts** > and locate and click the new host cluster. In the **Hosts** pane, in the **Host Status** column, verify that each node in the cluster is OK.
