---
ms.assetid: 832b1205-0ab2-4a35-9c08-6489bed33aad
title: Set up Hyper-V virtual fibre channel in the VMM 2016 storage fabric
description: This article describes how to set up Hyper-V virtual fibre channel in the VMM storage fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  08/04/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---
# Set up Hyper-V virtual fibre channel in the VMM storage fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to set up Hyper-V virtual fibre channel in the System Center 2016 - Virtual Machine Manager (VMM) storage fabric.

Virtual fibre channel provides Hyper-V VMs with direct connectivity to fibre channel-based storage. Hyper-V provides fibre channel ports within guest operating systems, so that you can virtualize applications and workloads that have dependencies on fibre channel storage. You can also cluster guest operating systems over fibre channel.

## Before you start

- VMM supports the following virtual fibre channel deployments:
  - Single storage array connected to a single fabric (comprised of single or multiple switches) connected to a single virtual SAN (vSAN). A vSAN is a named group of physical fibre channel Host Bus Adapter (HBA) ports on a host computer that VMs connect to access fibre channel storage devices.
  - Single storage array connected to multiple fabrics (comprised of single or multiple switches per fabric) that are connected to a single vSAN.
  - Multiple storage arrays connected to a single fabric (comprised of single or multiple switches) that is connected to a single vSAN.
  - Multiple storage arrays connected to multiple fabrics (comprised of single or multiple switches per fabric) that are connected to multiple vSANs. This configuration provides dual-redundant paths to storage arrays.

Here's what you need:

- One or more vSANs can be created for each host computer. A vSAN can only contain HBAs from a single fabric.
- Storage arrays, switches and HBAs must have the latest firmware and drivers installed.
- Make sure that storage arrays can present logical units (LUs).
- Enable NPIV on fibre channel switches and HBAs.
- Hyper-V hosts must be running at least Windows Server 2012.
- Ensure that an SMI-S provider is installed. VMM manages fibre channel fabrics and SAN devices using the SMI-S provider. Remember not to install the SMI-S provider on the VMM server, but on a server that the VMM server can connect to with an FQDN or IP address.

## Deploy virtual fibre channel

Here's what you need to do:

1. Discover and classify fibre channel fabrics.
1. Create vSANs for each host computer by grouping host HBA ports.
1. Create a VM that can access the virtual fibre vhannel storage.
1. Create zones that connect each host or VM vHBA to a storage array. Zones are used to connect a fibre channel array to a host computer VM.
1. Create LUNs and register them for a  host, VM, or service tier.
1. Create a service template, add VM templates to it. For each vHBA specify dynamic or static WWN assignments and select the classification. Create and deploy a service tier based on the service template, to access Virtual Fibre Channel storage. You zone a fibre channel array to the tier, add a disk, create a LUN and register the LUN to the tier.

## Discover and classify fibre channel fabrics

1. Click **Fabric** > **Storage** > **Add Resources** > **Storage Devices**.
1. In **Add Storage Devices Wizard** > **Select Provider Type**  select **Fibre Channel fabric discovered and managed by a SMI-S provider**.
1. In **Specify Discovery Scope** specify the IP address or FQDN, and the port number of the provider.
1. If you're using SMI-S specify whether the provider uses **SMI-S CIMXML** or **SMI-S WMI** and add the IP address/FQDN and port used to connect to the provider on the remote server. You can enable SSL if you're using CIMXML.
1. Specify an account for connecting to the provider.
1. In **Gather Information** VMM automatically discovers and imports the fibre channel fabric information. If the discovery process succeeds, the discovered fabric name, switches and fabric World Wide Node Names (WWNN) are listed on the page. When the process successfully completes, click **Next**. To retry the discovery process for an unsuccessful attempt, click **Scan Provider**.
1. If you selected the option to use an SSL connection for an SMI-S provider note that:
    - During discovery, the **Import Certificate** dialog box appears. Check settings and click **Import**. By default the certificate common name (CN) will be verified. This might cause storage discovery to fail if there's no CN or it doesn't match.
    - If discovery fails because the CN disable CN verification in the registry on the VMM server. In the registry go to **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Storage Management/** and create a new DWORD value - **DisableHttpsCommonNameCheck**. Set the value to 1.
1. On the **Fibre Channel Fabrics** page, do the following for each storage fabric that requires a classification:
    1. In the **Storage Device** column, select the check box next to a fibre channel fabric that you want VMM to manage.
    1. In the **Classification** column, select the classification that you want to assign to the fabric. Note that the fabric classification task is separate from that for storage classification, although the concept is similar.
1. On the **Summary** page, confirm the settings, and then click **Finish**.

## Create vSANs and assign HBAs

You can create vSANs and assign HBAs to it. One or more vSANs can be created for each host computer. Each vSAN can only contain HBAs that are from the same fabric.

Virtual Host Bus Adapters (vHBAs) represent the virtualization of fibre channel HBAs, and are used by VMs to connect with vSANs. Each vHBA has a World Wide Node Name (WWNN), which is different than the host HBA WWNN. Using N_Port ID Virtualization (NPIV), a host computer HBA can map to multiple vHBAs. HBA ports assigned to a vSAN can be added or removed as needed.

1. Click **Fabric** right-click the applicable host >  **Properties** > **Hardware** > **New Virtual SAN**.
1. In **New Virtual SAN** specify a name and optional describes. In **Fibre Channel adapters**, select the check boxes next to the fibre channel adapters (HBAs) that you want to assign to the vSAN. Click **OK**.
1. If you want to edit vSAN port assignments, in **Properties** > **Hardware** > **FC Virtual SAN** > **Fibre Channel adapter details** select or unselect the HBA ports.
1. If you want to add a new vHBA and assign it to a vSAN, click **Properties** > **Hardware Configuration** > **New** > **Fibre Channel Adapter**. In **Virtual SAN name** select a vSAN to assign it. Specify whether you want to assign port settings for the vHBA statically or dynamically.
1. If you want to change the global default port settings for vHBA click **Properties** > **Hardware** > **Global Settings** and modify settings in **Fibre Channel adapter details**. Note that changing these settings does not affect vHBA ports that have already been created. To apply a new setting to an existing vHBA port, recreate the port by removing it and then adding it again.

## Create a VM template

vHBAs are used by VMs to connect with vSANs. In order for vHBAs to connect to vSANs, they first must be added to the hardware profile of a VM template.

1. Use the **Create Virtual Machine Wizard** to create a new VM, and then add a new fibre channel adapter (vHBA) to the **Configure Hardware** page of the VM template. For each vHBA that you create, specify dynamic or static WWPN assignments and select the fabric classification.
1. Still using the **Create Virtual Machine Wizard**, place and deploy the VM to a destination host. Make sure the host contains a virtual SAN that matches the storage fabric. .

After you deploy the VM to a host, you can zone a virtual fibre channel storage array to the VM. Then, you create a LUN and register (unmask) it to the VM.

## Create zones

Zones are used to connect a fibre channel array to a host or virtual machine (VM). The storage array target ports are mapped to the HBA ports on the host or to the virtual HBA (vHBA) ports for the VM. You can create zones for a host, a VM, or both. For Hyper-V failover clusters, a zone is needed for each host in the cluster. Note that:

- Zones are grouped into zonesets, which use common fibre channel fabric devices. When all zones in a zone set have been added, modified, or removed as needed, the zoneset must be activated. Zoneset activation pushes information for each zone down to the fibre channel switches in the selected fabric.
- Only members of the same zone can communicate with each other.
- You'll need to create new zones and then activate the zoneset. Activating a zoneset may cause some downtime in the fabric as information is propagated to all the switches.
- If you want to add a storage array to a Hyper-V cluster, you need to zone the array to each host computer first. Similarly, if you want to add an array to a guest cluster, you need to zone the array to each VM first.

Set up zones as follows:

1. Click **VMs and Services** > **Services**, right-click the applicable VM, > **Properties** > **Storage**  > **Add** > **Add Fibre Channel Array**.
1. In **Add Fibre Channel Array** > **Properties** page > **Create New Zone** specify a zone name, select a storage array, and in **Fabric** select a switch. In **Storage array target ports**, select the applicable WWPM port or ports. In **Virtual machine initiator**, select the applicable WWPM port or ports. Then click **Create**. Click **Show aliases** to view the available zone aliases.
1. To activate the zoneset, click **Fabric** > **Name**, select the inactive zoneset > **Activate Zoneset**.
1. You can view the zonesets for a fabric in **Fabric** > **Fibre Channel Fabric** > **Name**, right-click the applicable fabric >  **Properties** > **Zonesets**.
1. If you want to modify zoning for a storage array click **VMs and Services** > applicable host > **Properties** > **Storage** > **Fibre Channel Arrays** > **Edit** > applicable array and modify the zoning settings.

## Create and register LUNs

For a host computer, VM, or computer service tier to access storage array resources, LUNs must be created and then registered (unmasked) to the host, VM, or tier.

1. Click **Fabric** > **Storage** > **Classifications and Pools**. Under **Name**, click the applicable storage device > **Create Logical Unit**.
1. In the **Create Logical Unit** select a storage pool, specify a name and description, and LUN size. Specify whether you want to crate a thin or fixed size LUN.
1. To register the LUN, in **VMs and Services** pane, right-click the applicable VM > **Properties** > **Add** > **Add Disk**.
1. In **Create Logical Unit** select a storage pool, name, and size. Click **OK** to register the LUN.

## Create and deploy a service tier

1. Using the **Service Template Designer**, create a service template and add the applicable VM templates you previously created to the service template.
1. Add a new virtual fibre channel adapter (vHBA) to the **Configure Hardware** page of the service template. For each vHBA that you create, specify dynamic or static WWPN port assignments and select the fabric classification.
1. Create service tier from the service template and assign the service tier to a computer tier.
1. Deploy the tier.
1. After you deploy it, you can zone a virtual fibre channel storage array to the service tier. Then create a LUN for the array and register (unmask) it to the tier.

## Next steps

[Set up storage](hyper-v-storage.md) for Hyper-V hosts and clusters.
