---
title: How to create a port profile for virtual network adapters in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70c76400-7488-4d03-b555-f5e5f95fb261
---
# How to create a port profile for virtual network adapters in VMM
In [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], you can consistently configure identical capabilities for network adapters across multiple hosts by using port profiles and logical switches. Port profiles and logical switches act as containers for the properties or capabilities that you want your network adapters to have. Instead of configuring individual properties or capabilities for each network adapter, you can specify the capabilities in port profiles and logical switches, which you can then apply to the appropriate adapters.

> [!IMPORTANT]
> For information about prerequisites and settings for port profiles and logical switches, see the “Settings” section in [Overview: plan logical switches and port profiles in VMM](../Topic/Overview--plan-logical-switches-and-port-profiles-in-VMM.md). It is especially important to review the prerequisites if you plan to enable virtual machine queue \(VMQ\), IPsec task offloading, or single\-root I\/O virtualization \(SR\-IOV\) in your port profile for virtual network adapters.

The recommended sequence for creating port profiles and logical switches is to create the port profiles first.

Use the following procedure to create a port profile for virtual network adapters.

### To create a port profile for virtual network adapters

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking**, and then click **Port Profiles**.

4.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Hyper\-V Port Profile**.

    The wizard for creating port profiles opens.

5.  On the **General** page, enter a name and optional description for the port profile, click **Virtual network adapter port profile**, and then click **Next**.

6.  On the **Offload Settings** page, optionally select one or more of the following settings, and then click **Next**. For more information about the settings listed in this step or the next step, in [Overview: plan logical switches and port profiles in VMM](../Topic/Overview--plan-logical-switches-and-port-profiles-in-VMM.md), in the “Settings” section, see the “Native port profile for virtual network adapters” row in the table.

    -   **Enable virtual machine queue**

    -   **Enable IPsec task offloading**

    -   **Enable Single\-root I\/O virtualization**

7.  On the **Security Settings** page, optionally select one or more of the following settings, and then click **Next**.

    -   **Allow MAC spoofing**

    -   **Enable DHCP guard**

    -   **Allow router guard**

    -   **Allow guest teaming**

    -   **Allow IEEE priority tagging**

    -   **Allow guest specified IP addresses\(only available for virtual machines on Windows Server 2012 R2\)**

8.  On the **Bandwidth Settings** page, optionally specify bandwidth settings for the virtual network adapter.

    -   **Minimum bandwidth \(Mbps\)**: Specify the minimum bandwidth here in megabits per second \(Mbps\), or use the **Minimum bandwidth weight** option \(described later in this list\).

    -   **Maximum bandwidth \(Mbps\)**: Specify the maximum bandwidth, using a value no greater than 100,000 Mbps. A value of 0 Mbps means the maximum is not configured.

    -   **Minimum bandwidth weight**: Specify a weighted value from 0 to 100 that controls how much bandwidth the virtual network adapter can use in relation to other virtual network adapters.

    > [!NOTE]
    > Bandwidth settings are not used when SR\-IOV is enabled on the port profile and on the logical switch that specifies the port profile.

9. On the **Summary** page, review and confirm the settings, and then click **Finish**.

## See Also
[Overview: plan logical switches and port profiles in VMM](../Topic/Overview--plan-logical-switches-and-port-profiles-in-VMM.md)
[Configuring Networking in VMM](../Topic/Configuring-Networking-in-VMM.md)

