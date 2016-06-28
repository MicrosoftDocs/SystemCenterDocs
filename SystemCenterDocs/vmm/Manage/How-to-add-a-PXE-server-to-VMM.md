---
title: How to add a PXE server to VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0f97147-d9b7-43b3-ad1a-9a5b2c138ab5
---
# How to add a PXE server to VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedure to add a pre-boot execution environment (PXE) server to Virtual Machine Manager (VMM). The PXE server is used to initiate operating system installations on bare-metal computers, as described in [Overview: creating hosts or host clusters from bare metal with VMM](Overview--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md) and [Overview: creating Scale-Out File Servers from bare metal in VMM](Overview--creating-Scale-Out-File-Servers-from-bare-metal-in-VMM.md).

If you have an existing PXE server in your environment configured with Windows Deployment Services, you can add that server to VMM. Then you can use it for provisioning in VMM (and VMM will recognize only the resulting servers). All other requests will continue to be handled by the PXE server according to how it is configured.

If you do not have an existing PXE server, you can deploy the Windows Deployment Services role on a server running a supported operating system. When you install Windows Deployment Services, consider the following:

-   If you are using VMM in System Center 2016 Technical Preview you can use one of the following operating systems for the PXE server:

    -   Windows Server 2008 R2

    -   Windows Server 2012

    -   Windows Server 2012 R2

    -   Windows Server Technical Preview

-   During installation of the Windows Deployment Services role, install both the **Deployment Server** and the **Transport Server** options.

-   When you configure Windows Deployment Services, you do not have to add images to Windows Deployment Services. During host deployment, VMM uses a virtual hard disk that you have created and stored in the VMM library.

-   You do not have to configure the settings on the **PXE Response** tab in Windows Deployment Services. VMM ignores these settings because VMM uses its own PXE provider.

For information about how to deploy Windows Deployment Services, including the required permissions, see the [Windows Deployment Services Getting Started Guide for Windows Server 2012](http://technet.microsoft.com/library/jj648426.aspx).

**Account requirements:** When you add a PXE server, you must specify account credentials for an account that has local administrator permissions on the PXE server. You can enter a user name and password or specify a Run As account. If you want to use a Run As account, you can create the Run As account before you begin this procedure, or create it during the procedure.

For example, you could create a Run As account called **PXE Administrator**. For more information, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

### To add a PXE server to VMM

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Servers**.

3.  On the **Home** tab, in the **Add** group, click **Add Resources** > **PXE Server**.

4.  In the **Add PXE Server** dialog box, do the following:

    1.  In the **Computer name** box, enter the computer name of the PXE server.

        For example, enter **PXEServer01.contoso.com**.

    2.  Enter the credentials for an account that has local administrator permissions on the PXE server.

        You can specify an existing Run As account or manually enter user credentials in the format *domain_name*\\*user_name*.

        > [!NOTE]
        > If you do not already have a Run As account, click **Browse**, and then in the **Select a Run As Account** dialog box, click **Create Run As Account**.

        For example, if you created the example **PXE Administrator** Run As account that is described in the Prerequisites section of this topic, you would click **Browse**, click the **PXE Administrator** Run As account, and then click **OK**.

    3.  Click **Add**.

        The **Jobs** dialog box opens. Verify that the job has a status of **Completed**, and then close the dialog box. The job sets up the new PXE server, installs the VMM agent on the PXE server, imports a new Windows Preinstallation Environment (Windows PE) image, and adds the machine account for the PXE server to VMM.

5.  To verify that the PXE server was added, perform these steps:

    1.  In the **Fabric** pane, expand **Servers**, and then click **PXE Servers**.

    2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

    3.  In the **PXE Servers** pane, verify that the PXE server appears with an agent status of **Responding**.

## See Also
[Prerequisites: creating hosts or host clusters from bare metal with VMM](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing infrastructure resources with VMM](Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



