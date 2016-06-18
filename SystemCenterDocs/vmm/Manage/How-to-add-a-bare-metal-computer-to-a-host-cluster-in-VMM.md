---
title: How to add a bare-metal computer to a host cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94c20d10-4e0d-4b68-8812-c7e134fbd62d
---
# How to add a bare-metal computer to a host cluster in VMM
This article describes how to add a bare metal computer to a Hyper-V cluster.


If you created the cluster from bare metal, you can use the same physical computer profile, PXE server, and other similar elements that you used when creating the cluster.


1. Open the **Fabric** > **Servers** > **All Hosts**. Right-click the host cluster and click **Add Cluster Node**.
2. On the **Resource Type** page, select **Physical computers to be provisioned**, then fill in the options:

	- Specify the Administrator Run As account that VMM will use.
	- Select the physical computer profile \(which will provide the administrator Run As account and domain name\).
	- Next to the **BMC Run As account** box, click **Browse**, select a Run As account that has permissions to access the BMC, and then click **OK**.
	- In the **Out\-of\-band management protocol** list, click the protocol that your BMCs use. If you want to use Data Center Management Interface \(DCMI\), click **Intelligent Platform Management Interface \(IPMI\)**. Although DCMI 1.0 is not listed, it is supported. Check that the correct port is selected.
	- If the **Skip cluster validation** option appears, and you do not require support from Microsoft for this cluster, you can skip validation.
	
3. In **Discovery Scope** specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range. Deep discovery provides detailed information about a computer \(for example, MAC addresses of network adapters\) but restarts the computer, and requires additional time. You can allow or skip deep discovery.
4. If you are adding a single computer, you can either specify a single IP address, or specify an IP address range that both starts and ends with the intended IP address. If you specify a single IP address, and allow deep discovery, when you click **Next**, the computer will be restarted. If you specify an IP address range, when you click **Next**, information about the computer will be displayed, and you can confirm that you specified the computer that you meant to.
5. If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs \(identified by IP addresses\), and select the ones you want to include in the cluster. If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**.
6. In **Deployment Customization**  review the list of computers again, and provide information for each computer that you want to include. If you see a computer that you don't want to include, select the BMC \(identified by IP address\) and then click **Remove**.
7. Configure the computers. Click the BMC IP address. In the **Computer name** box, type a unique name, without any wildcard characters.
8. Select or clear **Skip Active Directory check for this computer name**. The Active Directory check prevents deployment if the computer account already exists in Active Directory Domain Services \(AD DS\). This helps prevent deploying a computer with the same name as an existing computer. f you skip the Active Directory check, and there is an existing computer account in AD DS other than the Run As account that was specified in the physical computer profile, the deployment process will fail to join the computer to the domain.
9. For the computer you are configuring, click a network adapter \(on the left\). You can leave the displayed configuration unchanged, or fill in more information by clicking the button on the right, labeled either with **Configure** or with an ellipsis \(**...**\). If you click the button in the **Network Adapter IP Configuration** box you can specify:

	- The MAC address of the managed NIC which can be used to communicate with the VMM server.
	- If you select **Specify static IP addresses for the network adapter**, select a logical network and \(if applicable in that logical network\) an IP subnet. If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that is in within the logical network or its subnet. If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the hosts and to the network that the adapter is connected to. Otherwise, deployment may fail.
10.  Repeat the configuration process for each network adapter. Note that if the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now \(for example, if physical hardware needs to be installed or uninstalled\), you can select the computer's BMC IP address from the list and then click **Remove**.
11. Repeat the entire process for each BMC IP address in the list.
12. On the **Summary** page, confirm the settings, and then click **Finish** to provision the computers and add them to the cluster under VMM management.
13. To confirm that the node was added to the cluster click **Fabric** > **Servers** > **All Hosts** and locate and click the host cluster. In the **Hosts** pane, in the **Host Status** column, verify that the new nodes are **OK**. To view detailed status information for a host cluster, including a link to the cluster validation test report, right\-click the cluster, click **Properties**, and then click the **Status** tab.
14. On a host cluster, you can perform cluster validation at any time. To do this, click the cluster and then on the ribbon, click **Validate Cluster**. Cluster validation begins immediately.

  

