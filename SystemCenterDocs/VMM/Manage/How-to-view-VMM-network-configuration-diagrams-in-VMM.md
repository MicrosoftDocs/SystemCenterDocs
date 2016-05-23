---
title: How to view VMM network configuration diagrams in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1aa1248d-4a73-4b55-b03d-278ff3820343
---
# How to view VMM network configuration diagrams in VMM
With [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc_threshold_1](../../Token/sc_threshold_1_md.md)], you can view diagrams that show the relationships among networking objects, such as logical networks and VM networks, that you have configured. You can view a diagram of the networking objects on a particular host system or the networking objects on a cloud. A diagram provides a graphical view of network configurations, which supplements the text\-based views that are available in the properties sheet for the host or the cloud.

### To view [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] network configuration diagrams

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, expand **All Hosts**, and then locate and click the host group that contains a host for which you want to view the network configuration.

3.  In the **Hosts** pane, select one of the hosts for which you want to view network diagrams.

4.  On the **Host** tab, in the **Window** group, click **View Networking**.

5.  As needed, select or clear check boxes for hosts, host groups, or clouds, until the items that you want to view are selected.

6.  In the **Show** group, click a view:

    -   **VM Networks**: This view shows VM networks and the virtual machines that are connected to them.

    -   **Host Networks**: This view shows the logical networks that are configured on the network adapters on the hosts.

    -   **Host\/VM Networks**: This view shows the logical networks that are configured on the network adapters on the hosts, plus the VM networks on each logical network and the virtual machines on the hosts.

    -   **Network Topology**: This view provides an overview of the logical networks, network sites, and VM networks that have been configured on the hosts.

7.  In the **Zoom** group and the **Orientation** group, adjust options for the display.

    To see information about an element in the diagram, hover over that item.

8.  If you want to document the configuration, you can capture the information in the display using one of the following methods:

    -   Press the **Print Screen** key, paste the screen image into a graphics application, and then save it.

    -   Use your preferred screen capture application.

    -   If Microsoft Visio is available for you to use, click the **File** tab \(in the upper corner\), and then click **Export to Visio**. Specify a path and file name for the Visio file, and then click **Save**.

## See Also
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


