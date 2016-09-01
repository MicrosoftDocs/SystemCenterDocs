---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  VMM networking reference  creating custom MAC address pools in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  173187c5-4a8b-4410-9d6e-a700a1184d7b
---

# VMM networking reference: creating custom MAC address pools in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following optional procedure to create custom media access control (MAC) address pools for virtual machines that are running on managed hosts. By using static MAC address pools, Virtual Machine Manager (VMM) can automatically generate and assign MAC addresses to new virtual network devices. You can use either the default MAC address pools or configure custom MAC address pools that are scoped to specific host groups.

> [!IMPORTANT]
> If you want to use the default MAC address pools, do not complete this procedure.

VMM uses the following default MAC address pool ranges.

|Default MAC Address Pool Name|Hypervisor Platform|Default MAC Address Pool Range|
|---------------------------------|-----------------------|----------------------------------|
|**Default MAC address pool**|Hyper-V|00:1D:D8:B7:1C:00 " 00:1D:D8:F4:1F:FF|
|**Default VMware MAC address pool**|VMware ESX|00:50:56:00:00:00 " 00:50:56:3F:FF:FF|

If you create custom MAC address pools, the following restrictions apply:

-   If you want to divide one of the default pools into smaller custom pools, you must first delete the default MAC address pool or the default VMware MAC address pool. You must delete the default pool to avoid duplicate MAC address assignments.

-   The first three octets of the beginning and ending MAC address must be the same.

-   You must enter a valid hexadecimal values between 00 and FF.

-   The ranges that you specify cannot overlap.

-   The address range must not have the multi-cast bit set to 1. For example, you cannot use addresses that start with *X*1, *X*3, *X*5, *X*7, *X*9, *X*B, *X*D, or *X*F, where *X* is any value.

-   To avoid conflicts with addresses reserved by Microsoft, VMware, and Citrix, do not use the following prefixes.

    |Reserved For|Prefixes|
    |----------------|------------|
    |Microsoft|00:03:FF<br /><br />00:0D:3A<br /><br />00:12:5A<br /><br />00:15:5D<br /><br />00:17:FA<br /><br />00:50:F2<br /><br />00:1D:D8 (except for the 00:1D:D8:B7:1C:00 " 00:1D:D8:F4:1F:FF range that is reserved for VMM)|
    |VMware|00:05:69<br /><br />00:0C:29<br /><br />00:1C:14<br /><br />00:50:56 (except for the 00:50:56:00:00:00 " 00:50:56:3F:FF:FF range that is the reserved as the default VMware static range)|
    |Citrix|00:16:3E|

> [!IMPORTANT]
> Only complete the "To delete a default MAC address pool (optional)" procedure if you do not want to use the default pools, or you want to divide a default pool into smaller pools.

### To delete a default MAC address pool (optional)

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **MAC Address Pools**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **MAC Pools** pane, click the default MAC address pool that you want to delete.

    For example, to delete the default pool for Hyper-V, click **Default MAC address pool**.

5.  On the **Home** tab, in the **Remove** group, click **Remove**.

6.  When prompted whether you want to remove the default MAC address pool, click **Yes**.

### To create custom MAC address pools

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **MAC Address Pools**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  On the **Home** tab, in the **Create** group, click **Create MAC Pool**.

    The Create MAC Address Pool Wizard opens.

5.  On the **Name and Host Group** page, do the following, and then click **Next**:

    1.  In the **MAC address pool name** and **Description** boxes, enter a name and optional description for the MAC address pool.

        For example, enter the following information:

        |||
        |-|-|
        |MAC pool name|**MAC pool - Seattle**|
        |Description|**MAC pool for Seattle and its child host groups (Hyper-V)**|

    2.  Under **Host groups**, select the check box next to each host group to which the MAC address pool will be available.

        For example, select the check box next to the **Seattle** host group. By default, all child host groups are selected.

6.  On the **MAC Address Range** page, specify the beginning and ending MAC address.

    For example, enter the following information, and then click **Next**.

    > [!NOTE]
    > This example assumes that you have deleted the default MAC address pool.

    |||
    |-|-|
    |Starting MAC address|**00:1D:D8:B7:1C:00**|
    |Ending MAC address|**00:1D:D8:B7:1F:E8**|

7.  On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

    The MAC address pool appears in the **MAC Pools** pane.

8.  Optionally, repeat this procedure to create custom MAC pools for other host groups.

    > [!NOTE]
    > If you are following the scenario examples, and have deleted the default MAC address pool, and then created a custom MAC address pool for Seattle, make sure that you create a custom MAC pool for the New York host group (and its child host groups).

> [!NOTE]
> You can use the Windows PowerShell cmdlets, [Get-SCMACAddress](http://technet.microsoft.com/library/jj613233.aspx) and [Get-SCMACAddressPool](http://technet.microsoft.com/library/jj654398.aspx), to view the states of the MAC addresses in a MAC address pool. Use the cmdlets with the following syntax, where `<MACAddressPool>` is the name of your MAC address pool:
> 
> `$MACpool=Get-SCMACAddressPool "Name <MACAddressPool>`
> 
> `Get-SCMACAddress "MACAddressPool $MACpool | Format-Table "property Address,VirtualNetworkAdapter,State`

From time to time, you might need to release MAC addresses that are in the pool but that are marked by VMM as "inactive." Releasing them makes them available for reassignment. For more information, see [How to release inactive IP or MAC addresses in VMM](How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md).

## See Also
[How to release inactive IP or MAC addresses in VMM](How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md)
[Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



