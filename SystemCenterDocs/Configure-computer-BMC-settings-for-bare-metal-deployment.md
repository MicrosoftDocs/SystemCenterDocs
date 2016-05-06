---
title: Configure computer BMC settings for bare-metal deployment
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15b8e1cc-d5b1-4e23-a485-fa3b06b29bfe
---
# Configure computer BMC settings for bare-metal deployment
Using a Baseboard Management Controller \(BMC\), you can manage a computer remotely independent of the operating system, and control system functions such as the ability to turn the computer off or on.
[!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] uses BMCs to restart computers during bare\-metal provisioning processes, and when optimizing power usage.

You can configure BMC settings and use the BMC   through [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] using the following procedures:

-   [Configuring BMC settings](#BKMK_ConfigBMC)

-   [Powering a computer on or off through VMM](../Topic/How-to-configure-computer-BMC-settings-in-VMM.md#BKMK_power)

In order for [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to use a BMC, the BMC must meet the following requirements:

-   The BMC must use one of the supported out\-of\-band management protocols, and the management protocol must be enabled in the BMC settings. The BMC must use one of the following management protocols:

    -   Intelligent Platform Management Interface \(IPMI\) versions 1.5 or 2.0

    -   Data Center Management Interface \(DCMI\) version 1.0

    -   System Management Architecture for Server Hardware \(SMASH\) version 1.0 over WS\-Management \(WS\-Man\)

    -   Custom protocols such as Integrated Lights\-Out \(iLO\)

-   The BMC should use the latest version of firmware for the BMC model.

-   The BMC must be configured with logon credentials and must use either static IP addressing or Dynamic Host Configuration Protocol \(DHCP\). If you use DHCP, we recommend that you configure DHCP to assign a constant IP address to each BMC, for example by using DHCP reservations.

-   The [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server must be able to access the network segment on which the BMCs are configured.

**Account requirements.** You can create a Run As account before you begin the procedure, or during the procedure. The Run As account must have permissions to access the BMC. For example, the Run As account could be called **BMC Administrator**. For information, see [How to create a Run As account in VMM](../Topic/How-to-create-a-Run-As-account-in-VMM.md).

## <a name="BKMK_ConfigBMC"></a>To configure BMC settings

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  In the **Hosts** pane, click the host that you want to configure.

4.  On the **Host** tab, in the **Properties** group, click **Properties**.

5.  In the *Host Name* **Properties** dialog box, click the **Hardware** tab.

6.  Under **Advanced**, click **BMC Setting**.

7.  To enable out\-of\-band management, do the following:

    1.  Select **This physical machine is configured for OOB management with the following settings**.

    2.  In the **This computer supports the specified OOB power management configuration provider** list, click the out\-of\-band management protocol that the BMC supports.

    3.  In the **BMC address** box, enter the IP address of the BMC.

    4.  In the **BMC port** box, accept the default. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] automatically populates the box with the port number for the selected out\-of\-band management protocol.

    5.  Next to the **Run As account** box, click **Browse**, click a Run As account that has permissions to access the BMC, and then click **OK**.

        > [!NOTE]
        > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

        For example, if you had a Run As account called **BMC Administrator**, you could click that account.

    6.  When you are finished, click **OK**.

## <a name="BKMK_power"></a>To power a computer on or off

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then click **All Hosts**.

3.  In the **Hosts** pane, click the host that you want to configure.

4.  On the **Host** tab, in the **Host** group, click **Power On** or **Power Off**. \(Additional options that are available with out\-of\-band power management include **Shutdown** and **Reset**.\)

    > [!NOTE]
    > -   If BMC settings are not configured, these options will not be available.
    > -   Information about power on and power off events is available in the BMC logs. To view BMC log information for a host, open the host properties, click the **Hardware** tab, and then under **Advanced**, click **BMC Logs**.
    > -   On HP computers, after the System Event Log is full, logging of new events stops and BMC logs display older events only.

## See Also
[Configuring Hyper-V host properties in VMM](../Topic/Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing VMware ESX hosts and vCenter servers with VMM](../Topic/Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[Deploying Scale-Out File Servers from bare metal with VMM](../Topic/Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing infrastructure resources with VMM](../Topic/Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

