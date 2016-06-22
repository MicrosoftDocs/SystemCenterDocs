---
title: How to deploy Hyper-V hosts from bare metal in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0ad90c3-5e6f-4a69-83dd-983ee9a9e4c6
---
# How to deploy Hyper-V hosts from bare metal in VMM
You can use Virtual Machine Manager \(VMM\) to deploy fully\-managed Hyper\-V hosts, either to “bare\-metal computers” \(no operating system installed\), or computers with an installed operating system that will be overwritten during the process. For this deployment, VMM does the following:

1.  Discovers the physical computer through out\-of\-band management

2.  Deploys an operating system image on the computer through the physical computer profile

3.  Enables the Hyper\-V role on the computer

4.  Brings the computer under VMM management as a managed Hyper\-V host

### To deploy Hyper\-V hosts from bare metal in VMM

1.  Ensure that you have met the requirements in [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

2.  Open the **Fabric** workspace.

3.  In the **Fabric** pane, click **Servers**.

4.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Hyper\-V Hosts and Clusters**.

    The Add Resource Wizard opens.

5.  On the **Resource location** page, click **Physical computers to be provisioned as virtual machine hosts**, and then click **Next**.

6.  On the **Credentials and Protocol** page, do the following:

    1.  Click **Browse**, select a Run As account that has permissions to access the BMC, and then click **OK**. For example, if you had a Run As account called **BMC Administrator**, you could select that account.

        If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    2.  In the **Protocol** list, click the out\-of\-band management protocol that your BMCs use.

        > [!NOTE]
        > If you want to use Data Center Management Interface \(DCMI\), click **Intelligent Platform Management Interface \(IPMI\)**. Although DCMI 1.0 is not listed, it is supported.

    3.  Ensure that the correct **Port**is selected.

7.  On the **Discovery Scope** page, specify the IP address scope that includes the IP addresses of the BMCs. You can enter a single IP address, an IP subnet, or an IP address range.

    If you are provisioning a single computer, you can either specify a single IP address, or specify an IP address range that both starts and ends with the intended IP address. If you specify a single IP address, when you click **Next**, the computer will be restarted. If you specify an IP address range, when you click **Next**, information about the computer will be displayed, and you can confirm that you specified the computer that you meant to.

    To continue, click **Next**.

8.  If you specified a single IP address on the previous page, skip this step. Otherwise, the **Target Resources** page appears. Review the list of discovered BMCs \(identified by IP addresses\), and select the ones you want to provision as hosts.

    If you don't see all the BMCs that you expect, confirm that they are on a network accessible to the VMM server, and as needed, click **Refresh**. If BMCs still appear to be missing, review [Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md).

    When you have finished making selections, click **Next**.

9. On the **Provisioning Options** page, fill in the options.

    1.  Click a host group for the new Hyper\-V hosts.

        For example, there might be a host group called **New York\\Tier0\_NY**.

    2.  Select the physical computer profile.

        For example, there might be a physical computer profile called **WS12R2Ent Hyper\-V Hosts – DHCP**.

10. On the **Deployment Customization** page, review the list of computers again, and provide information for each computer that you want to include. If you see a computer that you don't want to include, select the BMC \(identified by IP address\) and then click **Remove**.

    > [!CAUTION]
    > Review the list carefully. On a computer that already has a deployed operating system, proceeding with deployment can overwrite the operating system.

    Configure computers as follows:

    1.  Click the BMC IP address.

    2.  In the **Computer name** box, type a unique name, without any wildcard characters. \(Until you type a computer name for the computer, a **Missing settings** warning appears.\)

        For example, type **Host05**.

    3.  Select or clear **Skip Active Directory check for this computer name**. The Active Directory check prevents deployment if the computer account already exists in Active Directory Domain Services \(AD DS\). This helps prevent deploying a computer with the same name as an existing computer.

        > [!CAUTION]
        > If you skip the Active Directory check, and there is an existing computer account in AD DS other than the Run As account that was specified in the physical computer profile, the deployment process will fail to join the computer to the domain.

    4.  For the computer you are configuring, click a network adapter \(on the left\). You can modify the configuration, or fill in more information by clicking the button on the right, labeled either with **Configure** or with an ellipsis \(**...**\).

        If you click the button, in the **Network Adapter IP Configuration** box, you can specify the following:

        -   **MAC address**: If this is the management NIC for the host, and you want to configure it as a virtual network adapter, type a MAC address.

            > [!NOTE]
            > This is not the MAC address of the BMC. It is the MAC address of the management NIC, which can be used to communicate with the VMM management server.

        -   **Specify static IP settings for this network adapter**: If you check this box, select a logical network and \(if applicable in that logical network\) an IP subnet. If the selected IP subnet includes IP address pool, you can check **Obtain an IP address corresponding to the selected subnet**. Otherwise, type an IP address that is in within the logical network or its subnet.

            > [!IMPORTANT]
            > If you select an IP subnet, make sure that it corresponds to the physical location where you are deploying the host and to the network that the adapter is connected to. Otherwise, deployment may fail.

    5.  Repeat the configuration process for each network adapter in a computer.

        > [!IMPORTANT]
        > If the number of physical network adapters in a computer does not match the number of physical network adapters that are defined in the physical computer profile, you must specify any information that is missing for the adapters. If you decide not to provision this computer right now \(for example, if physical hardware needs to be installed or uninstalled\), you can select the computer's BMC IP address from the list and then click **Remove**.

    6.  Repeat the entire process for each BMC IP address in the list.

    When you have filled in needed information for all the computers you want to provision, click **Next**.

11. On the **Summary** page, confirm the settings, and then click **Finish** to deploy the new Hyper\-V hosts and bring them under VMM management.

    Depending on your settings, the **Jobs** dialog box might appear. Make sure that all steps in the job have a status of **Completed**, and then close the dialog box.

12. To confirm that the host was added, follow these steps:

    1.  Open the **Fabric** workspace.

    2.  In the **Fabric** pane, expand **Servers**, expand **All Hosts**, and then expand the host group that you specified.

    3.  Verify that the new Hyper\-V host or hosts appear in the host group.

> [!TIP]
> After deployment of a Hyper\-V host, to run additional scripts on that host, right\-click it, and then click **Run Script Command**.
> 
> In the advanced script command settings, note that the **Restart the computer or virtual machine if the specified exit code is returned** setting is ignored when you run the script on a host.

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Configuring Hyper-V host properties in VMM](Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)


