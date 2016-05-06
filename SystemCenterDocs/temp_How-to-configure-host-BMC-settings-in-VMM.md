---
title: temp_How to configure host BMC settings in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ca3d2a4-3b04-463b-ab89-20bcadaca526
---
# temp_How to configure host BMC settings in VMM
If a computer is configured for out\-of\-band management through a Baseboard Management Controller \(BMC\), you can configure BMC settings through [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] by using the procedure that follows.

To control the computer through the BMC, see [Powering a computer on or off through VMM](./How-to-configure-computer-BMC-settings-in-VMM.md#BKMK_power), later in this topic.

The BMC settings are also used for power optimization, described in [Configuring dynamic optimization and power optimization in VMM](./Configuring-dynamic-optimization-and-power-optimization-in-VMM.md).

## Prerequisites
To complete this procedure, the host must have a BMC installed that supports one of the following out\-of\-band management protocols:

-   Intelligent Platform Management Interface \(IPMI\) versions 1.5 or 2.0

-   Data Center Management Interface \(DCMI\) version 1.0

-   System Management Architecture for Server Hardware \(SMASH\) version 1.0 over WS\-Management \(WS\-Man\)

You can create a Run As account before you begin the procedure, or during the procedure. The Run As account must have permissions to access the BMC. For example, the Run As account could be called **BMC Administrator**. For information, see [How to create a Run As account in VMM](./How-to-create-a-Run-As-account-in-VMM.md).

#### To configure BMC settings

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

    4.  In the **BMC port** box, accept the default. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically populates the box with the port number for the selected out\-of\-band management protocol.

    5.  Next to the **Run As account** box, click **Browse**, click a Run As account that has permissions to access the BMC, and then click **OK**.

        > [!NOTE]
        > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

        For example, if you had a Run As account called **BMC Administrator**, you could click that account.

    6.  When you are finished, click **OK**.

## <a name="BKMK_power"></a>Powering a computer on or off through VMM

#### To power a computer on or off

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then click **All Hosts**.

3.  In the **Hosts** pane, click the host that you want to configure.

4.  On the **Host** tab, in the **Host** group, click **Power On** or **Power Off**. \(Additional options that are available with out\-of\-band power management include **Shutdown** and **Reset**.\)

    > [!NOTE]
    > -   If BMC settings are not configured, these options will not be available.
    > -   Information about power on and power off events is available in the BMC logs. To view BMC log information for a host, open the host properties, click the **Hardware** tab, and then under **Advanced**, click **BMC Logs**.
    > -   On HP computers, after the System Event Log is full, logging of new events stops and BMC logs display older events only.

## See Also
[Configuring Hyper-V host properties in VMM](./Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing VMware ESX hosts and vCenter servers with VMM](./Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](./Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)


