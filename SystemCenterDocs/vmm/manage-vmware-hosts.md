---
ms.assetid: 6cd25f33-e832-4898-83dd-bed12f06aed8
title: Set up VMware servers in the VMM compute fabric
description: This article provides guidance about managing VMware servers in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 12/03/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---



# Set up VMware servers in the VMM compute fabric



Read this article to learn about managing VMware servers and VMs in the System Center Virtual Machine Manager (VMM) fabric.

VMM enables you to deploy and manage virtual machines and services across multiple hypervisor platforms, including VMware vSphere hosts and vCenter servers.

- You can add vCenter and vSphere hosts to the VMM fabric.

- VMM integrates directly with VMware vCenter Server. Through the VMM console, you can manage the day-to-day operations of VMware vSphere hosts and clusters, such as the discovery and management of hosts.

- VMM provides the ability to create, manage, store, place, and deploy virtual machines on vSphere hosts. You can import VMware templates.

- You can associate host adapters with VMM logical networks. More advanced management takes place on the vCenter Server, for example, configuring port groups, standard and distributed virtual switches (or **vSwitches**), vMotion, and Storage vMotion.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
- You can convert VMware VMs to Hyper-V.
:::moniker-end
:::moniker range="sc-vmm-2025"
- You can [convert VMware VMs to Hyper-V](vm-convert-vmware.md).
:::moniker-end

## Before you start

- VMM supports the management of hosts and clusters running VMware. [Learn more](system-requirements.md) for supported versions of VMware.
- You need a vCenter server in your deployment. vSphere hosts and host clusters must be managed by a vCenter server, which, in turn, is managed by VMM.
- The following features are supported by VMM when hosts and clusters are managed with a vCenter server:
 - VMM command shell (same shell across all hypervisors).
 - VM placement based on host ratings when you create, deploy, or migrate VMware VMs. Includes concurrent VM deployment during service deployment.
 - You can deploy VMM services to vSphere hosts. You can't deploy vApps.
 - You can make vSphere host resources available to a VMM cloud by creating clouds from host groups in which vSphere hosts are located or by creating a cloud from a VMware resource pool.

   >[!NOTE]
   >VMM doesn't integrate with VMware vCloud.

 - You can use dynamic optimization and power optimization for vSphere hosts. VMM can load balance virtual machines on vSphere clusters using live migration. With power optimization, you can configure VMM to turn vSphere hosts on and off for power management.
 - You can transfer VMware resources using live migrating between hosts in a cluster (uses vMotion) and live storage migration (uses storage vMotion). Resources supported for transfer include network migration to and from the library and between hosts.

   >[!NOTE]
   >VMware thin provision disks become thick when you migrate a disk to the VMM library.

 - You can place vSphere hosts managed by VMM into and out of maintenance mode.
 - You can organize and store VMware VMs, VMDK files, and VMware templates in the VMM library. You can create new VMs from templates.

   >[!NOTE]
   >VMM doesn't support older VMDK disk types. These disk types are supported:
   > - Regular VMDK files (VMFS and monolithic flat)
   > - VMDK files that are used to access physical disks (vmfsPassthroughRawDeviceMap)
   > - Snapshots (vmfssparse)

 - You can create templates using .vmdk files stored in the library. You can also import templates stored on vSphere hosts (only template metadata is imported to VMM).
 - VMM supports existing standard and distributed vSwitches and port groups. vSwitches and port groups must be configured with the vCenter server.
 - You can do regular VMM networking tasks, including assigning logical networks, static IP address, and MAC address to Windows-based VMs running on VMware.
 - VMM supports and recognizes VMware Paravirtual SCSI (PVSCSI) storage adapters.
 - VMM doesn't support VMware VM with virtual hard disks connected to an IDE bus.
 - VMM supports VMware thin provision hard disk through the dynamic disk type.

   >[!NOTE]
   >If you create and deploy a VM to a vSphere host configured to use a dynamic disk, the disk will be thin provisioned. If a VM was created as a thin provisioned disk, out-of-band VM will display it as dynamic. If you save a thin provisioned disk to the library, VMM will save it as thick. It remains thick if you create a VM from it.

 - All storage must be added to vSphere hosts outside VMM.
 - Communication between VMM and the vCenter server is SSL encrypted. You'll need a certificate to identify the vCenter server. You can use a self-signed certificate for a vCenter server or a non-Microsoft verified certificate.
 - If you're using a self-signed certificate for authenticating the vCenter server to VMM, you can manually import the certificate to the Trusted People certificate store on the VMM management server before adding the vCenter server. If you don't, you'll be prompted to do this during deployment.
 - You'll need an account with admin permissions for the vCenter server (local or Active Directory account) and an account with admin permissions for the vSphere hosts. You can create Run As accounts before you begin. If you don't, you'll need to create accounts during the deployment procedure.
 - You can decide whether you want VMM to communicate with the vSphere hosts managed by the vCenter server over a secure connection. If so, you'll need a certificate to authenticate communications on each vSphere host or cluster. You can either use the self-signed certificate that VMware created when vSphere was installed on the host, or a certificate from a trusted CA. If you're using a self-signed certificate, you can  import it from each vSphere host to the VMM management server before you begin deployment
 - Before you configure network settings for vSphere hosts, ensure that you've created logical networks that you want to associate with the physical network adapters on the hosts.

## Add a vCenter server

1. Select **Fabric** > **Servers** > **vCenter servers** > **Add** > **Add Resources** > **VMware vCenter Server**.
2. In **Add VMware vCenter Server**, specify the name (FQDN, NetBIOS, or IP address) of the vCenter server. Add the port needed to connect to the vCenter server (443 by default).
3. In **Run As account**, select the Run As account with admin permissions for the vCenter server. Select **Create Run As Account** if you don't have one.
4. In **Security**, select or clear **Communicate with VMware ESX hosts in secure mode**. We recommend you keep the setting checked. If selected, you'll need a certificate and public key for each vSphere host managed by the vCenter server.
5. If you're using a self-signed certificate to communicate with the vCenter server and you haven't manually copied it to the Trusted People certificate store, the **Import Certificate** dialog will appear. Select **Import** to add the certificate to the store.
6. In **Jobs**, wait until the job has a Completed status and then check that the server appears in **Fabric** > **Servers** > **vCenter Server** with a **Responding** status.


## Add an ESX/ESXi host

1. Ensure that the vCenter server is managed by VMM before you start. When you add the vCenter server, vSphere hosts for the server are discovered automatically.
2. Select **Fabric** > **Add Resources** > **VMware ESX Hosts and Clusters**.
2. In the **Add Resource Wizard** > **Credentials**, select the Run As account that has admin permissions on the vSphere hosts you want to add. Create a Run As account if you don't have one.
3. In **Target Resources**, select the vCenter server. If the hosts are clustered, they'll be listed together with the cluster nodes.
3. In **Computer Name**, select the hosts or clusters you want to add or **Select All**.
4. In **Host Settings**, select the host group to which you want to assign the host or cluster. You don't need to add VM placement paths.
5. In **Summary**, verify the settings and select **Finish**. Wait until the Jobs dialog shows a **Completed** status.
6. Select **Fabric** > **Servers**> **All Hosts** and in the host group, check the status of each host or cluster. The **Host Status** should be either **OK** or **OK (limited)**.
7. If the status is limited, it means you've enabled the setting **Communicate with VMware ESX hosts in secure mode** but haven't yet imported a certificate from each vSphere host. To modify the security setting, right-click the vCenter server > **Properties** > **Security**.
5. To import the certificate, select each relevant host name > **Properties** > **Management** > **Retrieve** > **OK**. The host status must be **OK** after the import.

## Associate host adapters with logical networks

By default, when you added vSphere hosts to VMM, VMM automatically created logical networks that match the virtual network switch name.

   >[!NOTE]
   >VMM doesn't automatically create port groups, so you'll need to configure port groups with the necessary VLANs that correspond to network sites on the vCenter server.

Associate the logical network with the physical network adapter (for an external virtual network) as follows:

1. Select **Fabric** > **Servers** > **All Hosts** > vSphere host > **Host** > **Properties** > **Hardware**.
2. In **Network Adapters**, select the physical network adapter on the host. In **Logical network connectivity**, select the logical networks you want to associate with the adapter.

   >[!NOTE]
   >Only logical networks available to the host group are available.

3. Select **Advanced** > **Advanced Network Adapter Properties** to see IP subnets and VLANs available for a logical network. By default, for a logical network, the subnets and VLANs are scope to the host group or inherited via a parent host group. If none appears, it indicates that no network site exists for the logical network. If **Unassigned** is available, select it to view VLANS to which the physical adapter is connected but that isn't included in a network site.
4. View virtual network settings in the host properties > **Virtual Networks**. View compliance information in **Fabric** > **Networking** > **Logical Networks** > **Hosts** > **Logical Network Information for Hosts** > **Compliance**. A status of **Fully compliant** indicates that all subnets and VLAN that are in the network site are assigned to the network adapter.


## Import templates from vCenter

You can import VMware templates from the vCenter server to the VMM library. VMM copies only the metadata associated with the template and not the .vmdk file. This means that VMM is dependent on the vCenter server to use the template.

1. Select **Library** > **Home** > **Import** > **Import VMware template**.
2. In **Import VMware Templates**, select each template you want to import and select **OK**.
3. Verify the templates in **Library** > **Templates** > **VM Templates**.

## Set up a servicing window for a VMware host

Servicing windows provide a method for scheduling servicing outside VMM. You can associate a servicing window with individual hosts, virtual machines, or services. Before using other applications to schedule the maintenance tasks, you can use Windows PowerShell scripts or custom applications to query the object and determine if it's currently in a servicing window. Servicing windows don't interfere with the regular use and functionality of VMM. Set up a servicing window as follows:

1. In the VMM console, select **Settings** > **Create** > **Create Servicing Window**.
2. In **New Servicing Window**, specify a name and optional description for the window.
3. In **Category**, enter or select the category of servicing window.
4. In **Start time**, enter the date, time of day, and time zone for the maintenance window.
5. In **Duration**, specify the number of hours or minutes in the servicing window.
6. Under **Recurrence pattern**, select the frequency (Daily, Weekly, or Monthly), and then schedule the occurrences within that frequency.
7. After the window is set up, you can assign it to a host or VM. To assign to a host, select the host properties > **Servicing Window** > **Manage**, and select the window you want to add to the host.
