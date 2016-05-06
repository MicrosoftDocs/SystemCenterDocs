---
title: How to create VIP templates for hardware load balancers in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 189f12a2-ee3b-49c1-ba78-7aa6d829da10
---
# How to create VIP templates for hardware load balancers in VMM
You can use the following procedure to create a virtual IP \(VIP\) template for a hardware load balancer in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. A VIP template contains load balancer\-related configuration settings for a specific type of network traffic. For example, you can create a template that specifies the load\-balancing behavior for HTTPS traffic on a specific load balancer by manufacturer and model. These templates represent the best practices from a load\-balancer configuration standpoint.

> [!NOTE]
> For information about how to create a VIP template for Microsoft Network Load Balancing \(NLB\), see [How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](./How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md).

When users create a service, they can select a VIP template to use when they want to load\-balance a service tier. For an overview of the load\-balancer and VIP workflow, see [Load balancer integration](./Configuring-load-balancing-in-VMM.md#BKMK_LoadBalancerIntegration) in the topic [Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md).

### To create a VIP template for a hardware load balancer

1.  In [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **VIP Templates**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  On the **Home** tab, in the **Create** group, click **Create VIP Template**.

    The Load Balancer VIP Template Wizard starts.

5.  On the **Name** page, enter the following information, and then click **Next**:

    1.  The template name and description.

    2.  The VIP port to use. The VIP port is the port that is used for the type of network traffic that you want to load balance.

    For example, enter the name **Web tier \(HTTPS traffic\)** and a description of **Use for HTTPS traffic to production Web servers**. Enter the VIP port **443**. When you are finished, click **Next**.

6.  On the **Type** page, do either of the following, and then click **Next**:

    -   Click **Generic** to create a VIP template that can be used on any supported hardware load balancer.

    -   Click **Specific** to create a VIP template that applies to a specific hardware load balancer, and then specify the manufacturer and model.

        > [!NOTE]
        > In the **Manufacturer** list, the **Microsoft** entry is for NLB. For information about creating a VIP template for NLB, see [How to create VIP templates for Network Load Balancing &#40;NLB&#41; in VMM](./How-to-create-VIP-templates-for-Network-Load-Balancing--NLB--in-VMM.md).

    Click either of the options, depending on your test environment, and then click **Next**.

7.  On the **Protocol** page, click the protocol for which you want to create the VIP template. You can select one of the following options:

    -   **HTTP**

    -   **HTTPS passthrough**

        If you click this option, encryption carries all the way through to the virtual machine, and it is not decrypted at the load balancer.

    -   **HTTPS terminate**

        If you select this option, the traffic is decrypted at the load balancer. When traffic is decrypted at the load balancer, the load balancer has access to more detailed information to direct traffic, such as cookies and header information. For this option to be used, a certificate must be loaded previously on the load balancer.

        In **Certificate subject name**, enter the subject name of the certificate, for example, **C\=US,ST\=WA,L\=Redmond,O\=Contoso,OU\=Test,CN\=www.contoso.com\/emailAddress\=contoso@contoso.com**.

        To help secure the traffic from the load balancer to the virtual machine, select the **Re\-Encrypt** check box. This action re\-encrypts the HTTPS traffic from the load balancer to the virtual machine.

    -   **Custom**

        If you select this option, enter a protocol name in the **Protocol name** list, or select one from the list \(if values are available\).

    For example, click either **HTTPS passthrough** or **HTTPS terminate**, depending on your test environment.

8.  On the **Persistence** page, you can select the **Enable persistence** check box to enable session persistence \(also known as affinity\). If you enable persistence, the load balancer will always try to direct the same client to the same virtual machine that is behind the load balancer. This is based on the source IP address and the subnet mask that you specify \(for example, 255.255.255.0\), the destination IP address, or other persistence types, such as cookie or Secure Sockets Layer \(SSL\) session ID. \(The options vary, depending on the selected protocol.\) You can also click **Custom** and then select a custom persistence type. For a custom persistence type, the persistence value is optional, depending on the load balancer manufacturer.

9. On the **Health Monitors** page, you can specify a request that will occur at regular intervals against the load balancer to verify that a load balancer is available. \(Adding a health monitor is optional.\) To add a health monitor, do the following:

    1.  Click **Insert**.

    2.  In the **Protocol** list, click the desired protocol to monitor.

    3.  Under the **Request** column, click the empty field, and then enter the request.

        For example, type **GET \/**. Typically, this command makes an HTTP GET request for the home page of the load balancer and checks for a header response, such as 200 OK.

    4.  To modify the response type, interval, timeout, and retries values, click the field in the desired column, and then enter a new value.

        For example, under **Response**, enter **200**.

        > [!NOTE]
        > The time\-out value should be less than the interval value. The interval and time\-out values are in seconds.

10. On the **Load Balancing** page, select the load balancing method to use for new connections, and then click **Next**. You can configure new connections to be directed to a server based on the least connections or on the fastest response time, or by using round robin, where each server takes a turn. You can also click **Custom**, and then in the **Custom method** list, click a custom method that your load balancer supports.

11. On the **Summary** page, review the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

12. Verify that the VIP template that you added appears in the **VIP Templates** pane.

## See Also
[Configuring load balancing in VMM](./Configuring-load-balancing-in-VMM.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)
[How to add hardware load balancers in VMM](./How-to-add-hardware-load-balancers-in-VMM.md)


