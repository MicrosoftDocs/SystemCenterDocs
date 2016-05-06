---
title: How to create VIP templates for Network Load Balancing (NLB) in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b224c157-4a93-42d1-9eaa-898ef7e2a1dd
---
# How to create VIP templates for Network Load Balancing (NLB) in VMM
You can use the following procedure to create a virtual IP \(VIP\) template for Microsoft Network Load Balancing \(NLB\) in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. A VIP template contains load balancer\-related configuration settings for a specific type of network traffic. For example, you could create a template that specifies the load balancing behavior for HTTPS traffic on port 443.

When a user creates a service, they can select a VIP template to use when they want to load balance a service tier. For more information, see [Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md).

> [!NOTE]
> Service tiers running Linux or VM networks configured with network virtualization cannot use NLB. If load balancing is needed for such networks, use hardware load balancing. For more information about hardware load balancing, see [Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md).

### To create a virtual IP template for NLB

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **VIP Templates**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  On the **Home** tab, in the **Create** group, click **Create VIP Template**.

    The Load Balancer VIP Template Wizard starts.

5.  On the **Name** page, enter the following information, and then click **Next**.

    1.  The template name and description.

    2.  The virtual IP port to use. The virtual IP port is the port that is used for the type of network traffic that you want to load balance.

    For example, enter the name **Web tier \(HTTPS traffic\-NLB\)**, and a description of **Uses NLB to load balance HTTPS traffic to production Web servers**. Enter the virtual IP port **443**.

6.  On the **Type** page, do the following, and then click **Next**:

    1.  Click **Specific**.

    2.  In the **Manufacturer** list, click **Microsoft**.

        By default, in the **Model** list, **Network Load Balancing \(NLB\)** is listed.

7.  On the **Protocol** page, click the protocol that you want to create the virtual IP template for, and then click **Next**. You can select **TCP**, **UDP** or **Both TCP and UDP**.

8.  On the **Persistence** page, you can select the **Enable persistence** check box to enable session persistence \(also known as affinity\). If you enable persistence, the load balancer will always try to direct the same client to the same virtual machine that is behind the load balancer. This is based on the source IP address and the subnet mask.

    If you select the **Enable persistence** check box, accept the default value of **Source IP** in the **Persistence type** list. In the **Subnet mask to apply** list, click either of the following options:

    -   **Single**. If you select this option, NLB directs multiple requests from the same client IP address to the same host in the NLB cluster.

    -   **Network**. If you select this option, NLB directs multiple requests from the same TCP\/IP Class C address range to the same host in the NLB cluster. This setting ensures that clients that use multiple proxy servers to access the NLB cluster have their TCP or UDP connections directed to the same host in the NLB cluster.

    > [!NOTE]
    > When you deploy a service where a tier is configured to use NLB, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically creates the NLB host cluster.

    When you are finished, click **Next**.

9. On the **Summary** page, review the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

10. Verify that the VIP template that you added appears in the **VIP Templates** pane.

## See Also
[Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


