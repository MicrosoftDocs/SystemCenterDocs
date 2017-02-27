---
ms.assetid: 2c302d36-facc-4f91-bcc1-72f583ede872
title: Add a new node to an existing cluster in VMM 2016
description: This article describes how to add a new node to an existing host cluster in your VMM.
author:  Jyothirmai Suri
ms.author: v-jysur
manager:  riyazp
ms.date:  27/02/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Add a new node to an existing host cluster in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

## Before you start

Ensure the following:
- A Windows Server 2016 virtual hard disk (with latest updates installed) is available in the VMM library in VHD or VHDX format. Ensure you set the **Operating system** and **Virtualization platform values** for this VHD/VHDX. 
-  Update the PCP VHD path to the VHD/VHDX that you added to the VMM library.  To do this, edit the **Properties** of the PCP under **Library** > **Profiles** > **Physical Computer Profiles**. 
- PXE server has the latest WINPE image.  
To update the PE image, select the PXE server under **Fabric** > **Infrastructure** and click **Update WinPE image**. Ensure the job is complete.

## Add a new node to a existing  cluster in VMM

**Note**: 
- This procedure assumes that Two physical NICs are available on the host. For any other configuration, modify the PCP properties in the WSSD deployment and the PCP **Day100ScenarioSettings.ps1** file in the VMM library, as required. 
- Make sure the new node’s next boot option is set to **PXE**.  To do this, use the vendor specific user’s interface and related documentation for the BMC host.
 
**Use the following steps**:
1. In the VMM console, select **VMs and Services**, expand **All Hosts**.
2. Right-click an existing cluster and click **Add Cluster Node**.
3. On **Resource type** page, select the **Run as account** that has the domain admin privileges to add a node. 

    **Note**: If a domain admin Run as account is not available, create one.

4. Under **Physical computers to be provisioned**, select the physical computer profile (that has a prefix as provided for WSSD deployment - ends with PCP for non- premium and SDNPCP for premium deployments) and the BMC Run as account.   
**Note**: If a BMC Run as account is not available, create one.
5. On **Discovery scope** page, provide the BMC IP of the new host. Click **Next**.
6. On **Deployment customization** page, provide a computer name for the node. 
7. Under **Network adapters**, select the Two physical adapters (displayed as unknown) and enter the MAC addresses of the Two physical NICs that are present on the host.
For the first virtual adapter, browse under **Management NIC** and specify the name for the network adapter as **ManagementSwitch**. Select the Configure a static IPV4 address for this network adapter check box and click **OK**. 

    **Note**: To specify a different name for the virtual adapters, modify the **day100scenariosettings.ps1** PCP file, accordingly.
8. Repeat the steps for rest of the virtual adapters.  Specify the names for these as **Storage1Switch** and **Storage2Switch**, select **Configure a static IPV4 address for this network adapter** check box and click **OK**. 
9. On the **Summary** page, review the details and click **Finish**.

Once the job is complete without any errors, the newly added node appears under the selected cluster.
