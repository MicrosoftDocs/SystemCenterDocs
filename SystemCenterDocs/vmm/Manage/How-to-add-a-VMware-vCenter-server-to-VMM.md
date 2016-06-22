---
title: How to add a VMware vCenter server to VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6c8942f-84f6-4ebf-9d5a-be30d3b92892
---
# How to add a VMware vCenter server to VMM
You can use the following procedure to add a VMware vCenter Server to Virtual Machine Manager (VMM). You must add the vCenter Server before you can add VMware ESX hosts.

## Prerequisites
Before you begin this procedure, make sure that the following prerequisites are met:

-   The server that you want to add must be running a supported version of vCenter Server. For more information, see [VMM support for VMware](VMM-support-for-VMware.md).

-   For communications between the VMM management server and the vCenter Server, encryption using Secure Sockets Layer (SSL) requires a certificate to verify the identity of the vCenter Server. You can either use a self-signed certificate for the vCenter Server, or a third-party, verified certificate. If you are using a self-signed certificate, you can manually import the certificate to the Trusted People certificate store on the VMM management server before you add the vCenter Server, or you can import the certificate during this procedure when you are prompted to do this.

    > [!NOTE]
    > If you are using a third-party, verified certificate, you do not have to import the certificate to the Trusted People certificate store.

-   Although it is not a required prerequisite, as you can create a Run As account when you add the vCenter Server, you can create a Run As account beforehand. The credentials that you specify for the Run As account must have administrative permissions on the vCenter Server. You can use a local account or an Active Directory domain account, as long as the account has local administrative rights on the operating system of the vCenter Server.

    For example, create a Run As account that is named **VMware vCenter**.

    > [!NOTE]
    > You can create a Run As account in the **Settings** workspace. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

#### To add a vCenter Server

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then click **vCenter Servers**.

3.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **VMware vCenter Server**.

    The Add VMware vCenter Server dialog box opens.

4.  In the **Add VMware vCenter Server** dialog box, do the following:

    1.  In the **Computer name** box, enter the fully qualified domain name (FQDN), NetBIOS name, or IP address of the vCenter Server.

    2.  In the **TCP/IP port** box, enter the port to use to connect to the vCenter Server. By default, VMM uses TCP/IP port 443 to connect to the server through Secure Socket Layer (SSL).

    3.  Next to the **Run As account** box, click **Browse**, click the Run As account that has administrative access to the vCenter Server, and then click **OK**.

        For example, if you created the Run As account that is described in the Prerequisites section of this topic, click the **VMware vCenter** Run As account.

        > [!NOTE]
        > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

    4.  In the **Security** area, select or clear the **Communicate with VMware ESX hosts in secure mode** check box. By default, this check box is selected (recommended). If selected, a certificate and public key are required for each ESX or ESXi host that is managed by the vCenter Server. If you clear the check box, only Run As account credentials are required for communication.

    5.  When you are finished, click **OK**.

5.  If you are using a self-signed certificate for the vCenter Server, and you have not manually copied the certificate into the Trusted People certificate store on the VMM management server, the **Import Certificate** dialog box appears. In the **Import Certificate** dialog box, review the VMware certificate information, and then click **Import** to add the certificate to the Trusted People certificate store.

    > [!NOTE]
    > This step is not required if the certificate is a third-party, verified certificate.

    The **Jobs** dialog box appears. Make sure that the job to add the vCenter Server has a status of **Completed**, and then close the dialog box.

6.  To verify that the vCenter Server was added, in the **Fabric** workspace, expand **Servers** and then click **vCenter Servers**.

    In the **vCenter Servers** pane, verify that the vCenter Server is listed, with a status of **Responding**.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[How to add VMware ESX hosts to VMM](How-to-add-VMware-ESX-hosts-to-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


