---
title: How to configure Dynamic Optimization and Power Optimization in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e099462-8a49-4d5a-b8c0-ecc5c48cd840
---
# How to configure Dynamic Optimization and Power Optimization in VMM
Use the following procedures to enable Dynamic Optimization and Power Optimization for a host group in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] and to configure resource Power Optimization usage on a host group.

-   [To turn on Dynamic Optimization and Power Optimization for a host group](#BKMK_OnHG).

-   [To configure settings for Power Optimization](#BKMK_Settings). Use this procedure to change the thresholds for CPU, memory, disk I\/O, and network I\/O on hosts that govern how [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] performs Dynamic Optimization and Power Optimization within a host group. You do not need to perform this procedure unless you want to change the default thresholds.

For more information about Dynamic Optimization and Power Optimization, see [Configuring dynamic optimization and power optimization in VMM](Configuring-dynamic-optimization-and-power-optimization-in-VMM.md).

**Account requirements** Administrators and delegated administrators can configure Dynamic Optimization. Delegated administrators can configure Dynamic Optimization on host groups that are within the scope of their user role.

## <a name="BKMK_OnHG"></a>To turn on Dynamic Optimization and Power Optimization for a host group

1.  In the **Fabric** workspace, expand **Servers**, expand **All Hosts**, navigate to the host group that you want to configure.

2.  With the host group selected, on the **Folder** tab, in the **Properties** group, click **Properties**.

3.  In the host group properties, click **Dynamic Optimization** to open the **Specify dynamic optimization settings** page.

4.  To configure different settings than those of the parent host group, clear the **Use Dynamic Optimization settings from the parent host group** check box.

5.  In **Aggressiveness**, select **High**, **Medium**, or **Low**.

    Aggressiveness determines the amount of imbalance in virtual machine load on the hosts that is required in order to initiate a migration during Dynamic Optimization. When you configure frequency and aggressiveness for Dynamic Optimization, you should try to balance the resource cost of additional migrations against the advantages of balancing load among hosts in a host cluster. Initially, you might accept the default value of **Medium**. After you observe the effects of Dynamic Optimization in your environment, you can increase the aggressiveness.

    To help conserve energy by having [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] turn off hosts when they are not needed and turn them on again when they are needed, configure Power Optimization for the host group. Power Optimization is only available when virtual machines are being migrated automatically to balance load.

6.  To periodically run Dynamic Optimization on qualifying host clusters in the host group, enter the following settings:

    1.  Select the **Automatically migrate virtual machines to balance load** check box.

    2.  In **Frequency \(minutes\)**, specify how often to run Dynamic Optimization. You can enter any value between 10 minutes \(the default frequency\) and 1440 minutes \(24 hours\).

7.  To turn on Power Optimization on the host group, select the **Enable power optimization** check box.

8.  Click **OK** again to save your changes to the dynamic optimization settings.

## <a name="BKMK_Settings"></a>To configure settings for Power Optimization

1.  In the **Fabric** workspace, navigate to the host group and open its properties.

2.  Click **Dynamic Optimization** and, on the **Specify dynamic optimization settings** page, click **Settings**.

3.  In the **Customize Power Optimization Schedule** dialog box, change the settings for any of these resources: CPU, memory, disk input\/output \(I\/O\), or network I\/O.

4.  Under **Schedule**, select the hours when you want power optimization to be performed. Click a box to turn power optimization on or off for that hour.

    [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] applies the Power Optimization schedule locally according to the time zone of each host.

5.  Click **OK** to close the dialog box and **OK** again to close the group **Properties**.

## See Also
[Configuring dynamic optimization and power optimization in VMM](Configuring-dynamic-optimization-and-power-optimization-in-VMM.md)
[How to run Dynamic Optimization on a host cluster in VMM](How-to-run-Dynamic-Optimization-on-a-host-cluster-in-VMM.md)
[Managing host groups in VMM](Managing-host-groups-in-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


