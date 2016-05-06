---
title: How to modify or delete a logical network in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2705c237-8576-44bb-9871-f5ba644d854e
---
# How to modify or delete a logical network in VMM
You can use the following procedures to modify or delete a logical network in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. For example, you may want to add or remove an associated network site, or modify an IP address pool.

**Account requirements** To complete this procedure, you must be a member of the Administrator or the Delegated Administrator user role.

### To modify a logical network

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Logical Networks and IP Pools** pane, do either of the following:

    1.  To modify the logical network name or associated network sites, click the logical network that you want to modify. On the **Home** tab, in the **Properties** group, click **Properties**.

        On the **Name** tab, you can modify the name, description, and options. To modify the network sites, click the **Network Site** tab. To modify a network site, click the network site that you want to modify, and then change any associated settings. You can also add and remove network sites.

        > [!NOTE]
        > You cannot remove a network site if it has a dependent resource, for example an associated static IP address pool.

    2.  To modify an associated IP address pool, in the **Logical Networks and IP Pools** pane, expand the logical network, and then click the IP address pool. On the **Home** tab, in the **Properties** group, click **Properties**.

        You can modify the name, description, the IP address range, virtual IP \(VIP\) address reservations, the default gateway, Domain Name System \(DNS\) information, and Windows Internet Name Service \(WINS\) information. On the **Inactive addresses** tab, you can also release inactive IP addresses back to the static IP address pool.

        > [!NOTE]
        > You can view but cannot modify network site information from the IP address pool properties. To modify network site information, open the properties of the logical network.

### To delete a logical network

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Logical Networks and IP Pools** pane, click the logical network that you want to delete.

5.  On the **Home** tab, in the **Dependencies** group, click **View Dependent Resources**.

    The **Show Dependencies** dialog box lists any items that depend on the logical network. The list can include objects such as network sites \(listed under **Type** as logical network definitions\), load balancers, IP address pools, hosts, virtual machines, services, and templates. Before you can delete the logical network, you must modify or delete the dependent items so that they do not reference the logical network.

6.  After you modify or remove all dependencies, with the logical network selected, on the **Home** tab, in the **Remove** group, click **Remove**.

7.  In response to the confirmation message, click **Yes** to remove the logical network.

## See Also
[Overview: plan logical networks, network sites, and IP address pools in VMM](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[Modifying logical networks and VM networks in VMM](./Modifying-logical-networks-and-VM-networks-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](./Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


