---
title: How to add VMware ESX hosts to VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a88e021c-e21f-4947-a98f-fb3ec68bbb59
---
# How to add VMware ESX hosts to VMM
You can use the following procedure to add a VMware ESX or ESXi host or host cluster to Virtual Machine Manager \(VMM\).

## Prerequisites
Before you begin this procedure, make sure that the following prerequisites are met:

-   The VMware vCenter Server that manages the ESX hosts that you want to add must already be under VMM management. For more information, see the topic [How to add a VMware vCenter Server to VMM](How-to-add-a-VMware-vCenter-Server-to-VMM.md).

-   The hosts that you want to add must be running a supported version of ESX. For more information, see [VMM support for VMware](VMM-support-for-VMware.md).

-   If when you added the vCenter Server you selected the option to communicate with the ESX hosts in secure mode, VMM requires a certificate and public key for each managed ESX\/ESXi host. This enables all supported management tasks. You can either use the self\-signed certificate that VMware created when ESX was installed on the hosts, or a certificate from a trusted certification authority. If you are using the self\-signed certificate, you can import the certificate from each ESX host to the VMM management server beforehand, or you can import the certificate during this procedure. If you are using a certificate from a trusted certification authority, you do not have to manually retrieve the certificate from each host.

-   Although it is not a required prerequisite, as you can create a Run As account when you add the ESX hosts, you can create a Run As account beforehand. The Run As account need not have root credentials on the ESX hosts that you want to add. The Run As account must be a local account on the ESX host that has administrator permissions on the ESX host. Domain accounts are not supported.

    For example, create a Run As account that is named **ESX Hosts**.

    > [!NOTE]
    > You can create Run As accounts in the **Settings** workspace. For more information about Run As accounts, see [old_How to create a Run As account in VMM](old_How-to-create-a-Run-As-account-in-VMM.md).

    > [!NOTE]
    > In VMM in System Center 2016 Technical Preview, you do not have to enable Secure Shell \(SSH\) root login on each ESX host. Also note that the use of a virtual machine delegate is not supported.

#### To add an ESX host or host cluster

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **VMware ESX Hosts and Clusters**.

    The Add Resource Wizard opens.

3.  On the **Credentials** page, next to the **Run As account** box, click **Browse**, click the Run As account credentials on the ESX hosts that you want to add, click **OK**, and then click **Next**.

    For example, if you created the Run As account that is described in the Prerequisites section of this topic, click the **ESX Hosts** Run As account.

    > [!NOTE]
    > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

4.  On the **Target resources** page, in the **VMware vCenter Server** list, click the vCenter Server that manages the ESX hosts that you want to add.

    The available ESX hosts for the selected vCenter Server are listed. If the ESX hosts are clustered, the cluster name is listed together with the cluster nodes.

5.  In the **Computer Name** column, select the check box next to each ESX host or host cluster that you want to add, or click **Select all**. When you are finished, click **Next**.

6.  On the **Host settings** page, in the **Location** list, click the host group where you want to assign the ESX hosts, and then click **Next**.

    > [!NOTE]
    > You do not have to add virtual machine placement paths.

7.  On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box opens to indicate the job status. Verify that the job has a status of **Completed**, and then close the dialog box.

8.  To verify that the ESX host or host cluster was added, in the **Fabric** workspace, expand **Servers**, expand **All Hosts**, and then expand the host group where you added the ESX host or host cluster. Click the host or host cluster, and then verify in the **Hosts** pane that each host has a status of either **OK** or **OK \(Limited\)**.

    If each host has a status of **OK**, you do not have to complete the rest of this procedure.

9. If the host status is **OK \(Limited\)**, you must provide security information for the host to enable all supported management tasks in VMM. The host status indicates **OK \(Limited\)** if you enabled secure mode, but have not yet imported a certificate and public key. To update the host status to **OK**, follow these steps:

    > [!TIP]
    > To view or change the secure mode setting, in the **Fabric** pane, expand **Servers**, and then click **vCenter Servers**. In the **vCenter Servers** pane, right\-click the vCenter Server, and then click **Properties**. The secure mode setting is under **Security**.

    1.  Right\-click an ESX host that has a status of **OK \(Limited\)**, and then click **Properties**.

    2.  In the *Host Name* **Properties** dialog box, click the **Management** tab.

    3.  To retrieve the certificate and public key for the host, click **Retrieve**.

    4.  To view the thumbprint details, click **View Details**.

    5.  To accept the certificate and public key, select the **Accept the certificate for this host** check box.

    6.  When you are finished, click **OK**.

    7.  In the **Hosts** pane, verify that the host status is **OK**.

Repeat this step for each host that has a status of **OK \(Limited\)**.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[How to add a VMware vCenter Server to VMM](How-to-add-a-VMware-vCenter-Server-to-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


