---
ms.assetid: 832b1205-0ab2-4a35-9c08-6489bed33aad
title: Set up Hyper-V virtual Fibre Channel in the VMM storage fabric
description: This article describes how to set up Hyper-V virtual Fibre Channel in the VMM storage fabric
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---
# Set up Hyper-V virtual Fibre Channel in the VMM storage fabric



Read this article to set up Hyper-V virtual Fibre Channel in the System Center Virtual Machine Manager (VMM) storage fabric.

Virtual Fibre Channel provides Hyper-V VMs with direct connectivity to Fibre Channel-based storage. Hyper-V provides Fibre Channel ports within guest operating systems so that you can virtualize applications and workloads that have dependencies on Fibre Channel storage. You can also cluster guest operating systems over Fibre Channel.

## Before you start

- VMM supports the following virtual Fibre Channel deployments:
  - Single storage array connected to a single fabric (comprised of single or multiple switches) connected to a single virtual SAN (vSAN). A vSAN is a named group of physical Fibre Channel Host Bus Adapter (HBA) ports on a host computer that VMs connect to access Fibre Channel storage devices.
  - Single storage array connected to multiple fabrics (comprised of single or multiple switches per fabric) that are connected to a single vSAN.
  - Multiple storage arrays connected to a single fabric (comprised of single or multiple switches) that is connected to a single vSAN.
  - Multiple storage arrays connected to multiple fabrics (comprised of single or multiple switches per fabric) that are connected to multiple vSANs. This configuration provides dual-redundant paths to storage arrays.

Here's what you need:

- One or more vSANs can be created for each host computer. A vSAN can only contain HBAs from a single fabric.
- Storage arrays, switches, and HBAs must have the latest firmware and drivers installed.
- Ensure that storage arrays can present logical units (LUs).
- Enable NPIV on Fibre Channel switches and HBAs.
::: moniker range="sc-vmm-2016"
- Hyper-V hosts must be running Windows Server 2012 or later.
::: moniker-end
::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
- Hyper-V hosts must be running Windows Server 2016 or later.
::: moniker-end
::: moniker range="sc-vmm-2025"
- Hyper-V hosts must be running Windows Server 2019 or later.
::: moniker-end
- Ensure that an SMI-S provider is installed. VMM manages Fibre Channel fabrics and SAN devices using the SMI-S provider. Remember not to install the SMI-S provider on the VMM server, but on a server that the VMM server can connect to with an FQDN or IP address.

## Deploy virtual Fibre Channel

To deploy virtual Fibre Channel, follow these steps:

1. Discover and classify Fibre Channel fabrics.
2. Create vSANs for each host computer by grouping host HBA ports.
3. Create a VM that can access the virtual Fibre Channel storage.
4. Create zones that connect each host or VM vHBA to a storage array. Zones are used to connect a Fibre Channel array to a host computer VM.
5. Create LUNs and register them for a host, VM, or service tier.
6. Create a service template and add VM templates to it. For each vHBA, specify dynamic or static WWN assignments and select the classification. Create and deploy a service tier based on the service template to access Virtual Fibre Channel storage. Zone a Fibre Channel array to the tier, add a disk, create a LUN, and register the LUN to the tier.

## Discover and classify Fibre Channel fabrics

1. Select **Fabric** > **Storage** > **Add Resources** > **Storage Devices**.
2. In **Add Storage Devices Wizard** > **Select Provider Type**, select **Fibre Channel fabric discovered and managed by an SMI-S provider**.
3. In **Specify Discovery Scope**, specify the IP address or FQDN and the port number of the provider.
4. If you're using SMI-S, specify whether the provider uses **SMI-S CIMXML** or **SMI-S WMI**, and add the IP address/FQDN and port used to connect to the provider on the remote server. If you're using CIMXML, you can enable SSL.
5. Specify an account for connecting to the provider.
6. In **Gather Information**, VMM automatically discovers and imports the Fibre Channel fabric information. If the discovery process succeeds, the discovered fabric name, switches, and fabric World Wide Node Names (WWNN) are listed on the page. When the process successfully completes, select **Next**. To retry the discovery process for an unsuccessful attempt, select **Scan Provider**.
7. If you selected the option to use an SSL connection for an SMI-S provider, ensure that:
    - During discovery, the **Import Certificate** dialog appears. Check settings and select **Import**. By default, the certificate's common name (CN) is verified. Storage discovery can fail if there's no CN or it doesn't match.
    - If discovery fails because the CN disables CN verification in the registry on the VMM server, in the registry, go to **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Storage Management/** and create a new DWORD value - **DisableHttpsCommonNameCheck**. Set the value to 1.
8. On the **Fibre Channel Fabrics** page, do the following for each storage fabric that requires a classification:
    1. In the **Storage Device** column, select the checkbox next to a Fibre Channel fabric that you want VMM to manage.
    2. In the **Classification** column, select the classification that you want to assign to the fabric. The fabric classification task is separate from that for storage classification, although the concept is similar.
9. On the **Summary** page, confirm the settings and select **Finish**.

## Create vSANs and assign HBAs

You can create vSANs and assign HBAs to it. One or more vSANs can be created for each host computer. Each vSAN can only contain HBAs that are from the same fabric.

Virtual Host Bus Adapters (vHBAs) represent the virtualization of Fibre Channel HBAs and are used by VMs to connect with vSANs. Each vHBA has a World Wide Node Name (WWNN), which is different from the host HBA WWNN. Using N_Port ID Virtualization (NPIV), a host computer HBA can map to multiple vHBAs. HBA ports assigned to a vSAN can be added or removed as needed.

1. Select **Fabric** and right-click the applicable host >  **Properties** > **Hardware** > **New Virtual SAN**.
2. In **New Virtual SAN**, specify a name and optional description. In **Fibre Channel adapters**, select the checkboxes next to the Fibre Channel HBAs that you want to assign to the vSAN. Select **OK**.
3. If you want to edit vSAN port assignments, in **Properties** > **Hardware** > **FC Virtual SAN** > **Fibre Channel adapter details**, select or unselect the HBA ports.
4. If you want to add a new vHBA and assign it to a vSAN, select **Properties** > **Hardware Configuration** > **New** > **Fibre Channel Adapter**. In **Virtual SAN name**, select a vSAN to assign it. Specify whether you want to assign port settings for the vHBA statically or dynamically.
5. If you want to change the global default port settings for vHBA, select **Properties** > **Hardware** > **Global Settings** and modify settings in **Fibre Channel adapter details**. 

   >[!NOTE]
   >Changing these settings does not affect vHBA ports that have already been created. To apply a new setting to an existing vHBA port, recreate the port by removing it and then adding it again.

## Create a VM template

vHBAs are used by VMs to connect with vSANs. For vHBAs to connect to vSANs, they must be first added to the hardware profile of a VM template.

1. Use the **Create Virtual Machine Wizard** to create a new VM, and then add a new Fibre Channel adapter (vHBA) to the **Configure Hardware** page of the VM template. For each vHBA that you create, specify dynamic or static WWPN assignments and select the fabric classification.
2. Still using the **Create Virtual Machine Wizard**, place and deploy the VM to a destination host. Ensure that the host contains a virtual SAN that matches the storage fabric.

After you deploy the VM to a host, you can zone a virtual Fibre Channel storage array to the VM. Then you create a LUN and register (unmask) it to the VM.

## Create zones

Zones are used to connect a Fibre Channel array to a host or virtual machine (VM). The storage array target ports are mapped to the HBA ports on the host or to the virtual HBA (vHBA) ports for the VM. You can create zones for a host, a VM, or both. For Hyper-V failover clusters, a zone is needed for each host in the cluster. Ensure that:

- Zones are grouped into zonesets, which use common Fibre Channel fabric devices. When all zones in a zoneset have been added, modified, or removed as needed, the zoneset must be activated. Zoneset activation pushes information for each zone down to the Fibre Channel switches in the selected fabric.
- Only members of the same zone can communicate with each other.
- You'll need to create new zones and then activate the zoneset. Activating a zoneset can cause some downtime in the fabric as information is propagated to all the switches.
- If you want to add a storage array to a Hyper-V cluster, you need to zone the array to each host computer first. Similarly, if you want to add an array to a guest cluster, you need to zone the array to each VM first.

Set up zones as follows:

1. Select **VMs and Services** > **Services**, right-click the applicable VM, > **Properties** > **Storage**  > **Add** > **Add Fibre Channel Array**.
2. In **Add Fibre Channel Array** > **Properties** page > **Create New Zone**, specify a zone name, select a storage array, and in **Fabric**, select a switch. In **Storage array target ports**, select the applicable WWPM port or ports. In **Virtual machine initiator**, select the applicable WWPM port or ports. Select **Create**. Select **Show aliases** to view the available zone aliases.
3. To activate the zoneset, select **Fabric** > **Name**, and select the inactive zoneset > **Activate Zoneset**.
4. You can view the zonesets for a fabric in **Fabric** > **Fibre Channel Fabric** > **Name**; right-click the applicable fabric > **Properties** > **Zonesets**.
5. If you want to modify zoning for a storage array, select **VMs and Services** > applicable host > **Properties** > **Storage** > **Fibre Channel Arrays** > **Edit** > applicable array and modify the zoning settings.

## Create and register LUNs

For a host computer, VM, or computer service tier to access storage array resources, LUNs must be created and then registered (unmasked) to the host, VM, or tier.

1. Select **Fabric** > **Storage** > **Classifications and Pools**. Under **Name**, select the applicable storage device > **Create Logical Unit**.
2. In the **Create Logical Unit**, select a storage pool, and specify a name and description and LUN size. Specify whether you want to create a thin or fixed size LUN.
3. To register the LUN, in **VMs and Services** pane, right-click the applicable VM > **Properties** > **Add** > **Add Disk**.
4. In **Create Logical Unit**, select a storage pool, name, and size. Select **OK** to register the LUN.

## Create and deploy a service tier

1. Using the **Service Template Designer**, create a service template and add the applicable VM templates you previously created to the service template.
2. Add a new virtual Fibre Channel Adapter (vHBA) to the **Configure Hardware** page of the service template. For each vHBA that you create, specify dynamic or static WWPN port assignments and select the fabric classification.
3. Create service tier from the service template and assign the service tier to a computer tier.
4. Deploy the tier.
5. After you deploy it, you can zone a virtual Fibre Channel storage array to the service tier. Then create a LUN for the array and register (unmask) it to the tier.

## Next steps

[Set up storage](hyper-v-storage.md) for Hyper-V hosts and clusters.
