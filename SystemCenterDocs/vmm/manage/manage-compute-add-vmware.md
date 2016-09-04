---
title: Set up VMware servers in the VMM compute fabric
description: This article provides guidance about adding and managing VMware servers in the VMM fabric
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-09-04
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---



# Set up VMware servers in the VMM compute fabric

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Read this article to learn about managing VMware servers and VMs in the System Center 2016 - Virtual Machine Manager (VMM) fabric. You add vCenter and ESX/ESXi hosts to the fabric, associate adapters on hosts with logical networks, and import templates from VMware if required. You'll also learn about current options for converting VMware VMs to Hyper-V (V2V).

## Overview

VMM enables you to deploy and manage virtual machines and services across multiple hypervisor platforms, including VMware vSphere hosts and vCenter servers.

- VMM integrates directly with VMware vCenter Server. Through the VMM console, you can manage the day-to-day operations of VMware vSphere hosts and clusters, such as the discovery and management of hosts.
- VMM provides the ability to create, manage, store, place and deploy virtual machines on vSphere hosts.
- More advanced management should continue on the vCenter Server, for example configuring port groups,  standard and distributed virtual switches (or “vSwitches”), vMotion and Storage vMotion.


## Before you start

- VMM supports the management of hosts and clusters running VMware ESX or ESXi 4.1, and VMware ESX or ESXi 5.0.
- You need a vCenter server in your deployment. vSphere hosts and host clusters should be managed by a vCenter server, which in turn is managed by VMM.
- The following features are supported by VMM when hosts and clusters are managed with a vCenter server:
	- VMM command shell (same shell across all hypervisors)
	- VM placement based on host ratings when you create, deploy, or migrate VMware VMs. Includes concurrent VM deployment during service deployment.
	- You can deploy VMM services to vSphere hosts. You can't deploy vApps.
	- You can make vSphere host resources available to a VMM cloud by creating clouds from host groups in which vSphere hosts are located, or by creating a cloud from a VMware resource pool. Note that VMM doesn't integrate with VMware vCloud.
	- You can use dynamic optimization and power optimization for vSphere hosts. VMM can load balance virtual machines on vSphere clusters using live migration. With power optimization, you can configure VMM to turn vSphere hosts on and off for power management.
	- You can transfer VMware resources using live migrating between hosts in a cluster (uses vMotion) and live storage migration (uses storage vMotion). Resources supported for transfer include network migration to and from the library and between hosts. Note that VMware thin provision disks become thick when you migrate a disk to the VMM library.
	- You can place vSphere hosts managed by VMM into and out of maintenance mode.
	- You can organization and store VMware VMs, VMDK files, and VMware templates in the VMM library. You can create new VMs from templates. Note that VMM doesn't support older VMDK disk types. These disk types are supported: regular VMDK files (VMFS and moniolithic flat), VMDK files that are used to access physical disks (vmfsPassthroughRawDeviceMap), and snapshots (vmfssparse).
	- You can create templates using .vmdk files stored in the library. You can also import templates stored on vSphere hosts (only template metadata is imported to VMM)
	- VMM supports existing standard and distributed vSwitches and port groups. vSwitches and port groups must be configured with the vCenter server.
	- You can do regular VMM networking tasks, including assigning logical networks, static IP address and MAC address to Windows-based VMs running on VMware.
	- VMM supports and recognized VMware Paravirtual SCSI (PVSCSI) storage adapters.
	- VMM doesn't support VMware VM with virtual hard disks connected to an IDE bus.
	- VMM supports VMware thin provision hard disk through the dynamic disk type. Note that if you create and deploy a VM to a vSphere host configured to use a dynamic disk the disk will be thin provisioned. If a VM was created as a thin provisioned disk out-of-band VM will display it as dynamic. If you save a thin provision disk to the library VMM will save it as thick. It remains thick if you create a VM from it.
	- All storage must be added to vSphere hosts outside VMM.
	- Communication between VMM and the vCenter server is SSL encrypted. You'll need a certificate to identify the vCenter server You can use a self-signed certificate for a vCenter server or a third-party verified certificate.
	- If you're using a self-signed certificate for authenticating the vCenter server to VMM you can manually import the certificate to the Trusted People certificate store on the VMM management server before adding the vCenter server. If you don't you'll be prompted to do this during deployment.
	- You'll need an account with admin permissions for the vCenter server (local or Active Directory account) and an account with admin permissions for the vSphere hosts. You can create Run As accounts before you begin. If you don't  you'll need to create accounts during the deployment procedure.
	- You can decide whether you want VMM to communicate with the vSphere hosts managed by the vCenter server over a secure connection. If so you'll need a certificate to authentication communications on each vSphere host or cluster. You can either use the self-signed certificate that VMware created when vSphere was installed on the host, or a certificate from a trusted CA. If you're using a self-signed certificate you can  import it from each vSphere host to the vMM management server before you begin deployment
	- Before you configure network settings for vSphere hosts make sure you've created logical networks that you want to associated with the physical network adapters on the hosts.

## Add a v-Center server

1. Click **Fabric** > **Servers** > **vCenter servers** > **Add** > **Add Resources** > **VMware vCenter Server**.
2. In **Add VMware vCenter Server**, specify the name (FQDN, NetBIOS, or IP address) of the vCenter server. Add the port needed to connect to the vCenter server (443 by default).
3. In **Run As account**, click the Run As account with admin permissions for the vCenter server. Click **Create Run As Account** if you don't have one.
4. In **Security**, select or clear **Communicate with VMware ESX hosts in secure mode**. We recommend you keep the setting checked. If selected you'll need a certificate and public key for each vSphere host managed by the vCenter server.
5. If you're using a self-signed certificate to communicate with the vCenter server and you haven't manually copied it to the Trusted People certificate store the **Import Certificate** dialog will appear. Click **Import** to add the certificate to the store.
6. In **Jobs** wait until the job has a Completed status and then check that the server appears in **Fabric** > **Servers** > **vCenter Server** with a **Responding** status.


## Add an ESX/ESXi host

1. Ensure that the vCenter server is managed by VMM before you start. When you added the vCenter server vSphere hosts for the server are discovered automatically.
2. Click **Fabric** > **Add Resources** > **VMware ESX Hosts and Clusters**.
2. In the **Add Resource Wizard** > **Credentials** click the Run As account that has admin permissions on the vSphere hosts you want to add. Create a Run As account if you don't have one
3. In **Target Resources** click the vCenter server. If the hosts are clustered they'll be listed together with the cluster nodes.
3. In **Computer Name** select the hosts or clusters you want to add, or **Select All**.
4. In **Host Settings** click the host group to which you want to assign the host or cluster. You don't need to add VM placement paths.
5. In **Summary** verify the settings and click **Finish**. Wait until the Jobs dialog shows a **Completed** status.
6. Click **Fabric** > **Servers **> **All Hosts** and in the host group check the status of each host or cluster. Either **OK** or **OK (limited)**.
7. If it's limited it means you've enabled the setting **Communicate with VMware ESX hosts in secure mode** but haven't yet imported a certificate from each vSphere host. To modify the security setting right-click the vCenter server > **Properties** > **Security**.
5. To import the certificate click each relevant host name > **Properties** > **Management** > **Retrieve** > **OK**. The host status should be **OK** after the import.

## Associate host adapters with logical networks

By default when you added vSphere hosts to VMM, VMM automatically created logical networks that match the virtual network switch name. Note that VMM doesn't automatically create port groups so you'll need to configure port groups wiht the necessary VLANs that correspond to network sites on the vCenter server.

Associate the logical network with the physical network adapter (for an external virtual network) as follows:

1. Click **Fabric** > **Servers** > **All Hosts** > vSphere host > **Host** > **Properties** > **Hardware**.
2. In **Network Adapters** select the physical network adapter on the host. In **Logical network connectivity**, select the logical networks you want to associate with the adapter. Note that only logical networks available to the host group are available.
3. Click **Advanced** > **Advanced Network Adapter Properties** to see IP subnets and VLANs available for a logical network. By default for a logical network the subnets and VLANs are scope to the host group or inherited via a parent host group. If none appears it indicates that no network site existing for the logical network. If **Unassigned** is available, click it to view VLANS to which the physical adapter is connected, but that aren't included in a network site.
4. View virtual network settings in the host properties > **Virtual Networks**. View compliance information in **Fabric** > **Networking** > **Logical Networks** > **Hosts** > **Logical Network Information for Hosts** > **Compliance**. **Fully compliant** indicates that all subnets and VLAN that are in the network site are assigned to the network adapter.


## Import templates from vCenter

You can import VMware templates from the vCenter server to the VMM library. VMM copies only the metadata associated with the template and not the .vmdk file. This means that VMM is dependent on the vCenter server to use the template.

1. Click **Library **> **Home **> **Import** > **Import VMware template**.
2. In **Import VMware Templates**, select each template you want to import and click OK.
3. Verify the templates in **Library** > **Templates** > **VM Templates**.

## Convert VMware VMs to Hyper-V (V2V)

There are currently a couple of methods for converting VMWare VMs to Hyper-V:

- **Convert Virtual Machine Wizard**: In the VMM console you can use this wizard. This method has a number of limitations:
- Supported for vSphere 4.1 onwards.
- 
	- You can't convert VMware workstations
	- You can't convert VMs with virtual hard disks connected to an IDE bus
	- Online conversions aren't supported. You need to power off the VMware VMs.
	- Anti-virus apps must be supported.
	- VMware tools must be uninstalled from the guest operating system of the VM.
	
- [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn873998.aspx): This standalone tool converts VMware VMs to Hyper-V hosts or Azure VMs. It also converts physical machines and disks to Hyper-V hosts. IMPORTANT: This tool is in the process of retirement. It won't be available after June 3, 2017. [Learn more](https://blogs.technet.microsoft.com/scvmm/2016/06/04/important-update-regarding-microsoft-virtual-machine-converter-mvmc/)
- Azure Site Recovery currently doesn't have to ability for a direct VMware to Hyper-V conversion. [Read more](https://feedback.azure.com/forums/256299-site-recovery/suggestions/10050060-asr-to-support-vmware-to-hyper-v-protection-migrat) about up-voting this solution.


## Convert using the wizard

1. Click **VMs and Services** > **Home** > **Create** > **Create Virtual Machines** > **Convert Virtual Machine**.
2. In **Convert Virtual Machine Wizard** > **Select Source** click **Browse**. In **Select Virtual Machine Source**, select the VMware VMs you want to convert.
3. In **Specify Virtual Machine Identity**, modify the machine name and description as required.
4. In **Virtual Machine Configuration**, specify the number of processor and memory settings.
5. In **Select Host**, select a Hyper-V host for placement. In **Select Path** configure the storage location on the host for the VM files. The default VM paths are listed.
6. In **Select Networks**, select the logical network, virtual network, and the VLAN as applicable. The list matches whatever is configured on the physical adapters of the host.
7. In **Add Properties** configure settings.
8. In **Summary**, review the settings and select **Start the virtual machine after deploying it** if required. Then click **Create** to start the conversion. Verify the VM was converted in **VMs and Services** > **Home** > **Show** > **VMs**.
