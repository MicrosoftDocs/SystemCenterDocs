---
title: How to add an existing Scale-Out File Server to storage in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0b304e6-34d8-4316-a132-6cc6aec764d1
---
# How to add an existing Scale-Out File Server to storage in VMM
This topic describes how to add an existing Windows\-based Scale\-Out File Server to storage in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. For information about how to use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to create the Scale\-Out File Server and add it at the same time, see the links at the end of this topic.

When you add a file server, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] automatically discovers all the shares that are currently present on the server.  For information about the steps to take after adding the Scale\-Out File Server, see [Overview: configuring storage using Scale-Out File Servers in VMM](../Topic/Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a member of the Delegated Administrator user role.

You will need a Run As account with administrator permissions on the Scale\-Out File Server. You can create the Run As account before or during the procedure in this topic. For more information, see [How to create a Run As account in VMM](../Topic/How-to-create-a-Run-As-account-in-VMM.md).

### To add a Scale\-Out File Server to storage in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  On the **Home** tab, click **Add Resources**, and then click **Storage Devices** to start the Add Storage Devices Wizard.

4.  Fill in the wizard pages as follows:

    |Page|Action|
    |--------|----------|
    |**Select Provider Type**|Select  **Windows\-based file server**.|
    |**Specify Discovery Scope**|-   Specify the **Provider IP address or FQDN** of the Scale\-Out File Server \(this is the name or address of the file server, not the underlying cluster\). For example, you could specify a name such as **SOFS1.contoso.com**.<br />-   If the file server is in a domain that is not trusted by the domain of the Hyper\-V hosts, select **This computer is in an untrusted Active Directory domain**.<br />-   Click **Browse**, select a Run As account that has administrator permissions on the Scale\-Out File Server, and then click **OK**. Or, to create a new Run As account for accessing the file server, click **Browse**, and then click **Create Run As Account**.|
    |**Gather Information**|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] tries to discover and import information about the Scale\-Out File Server. If the discovery process succeeds, confirm that the display lists the correct file server, and then click **Next**.|
    |**Select Storage Devices**|Select the file shares that you want [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to manage. You will be able to perform additional configuration steps on the file server, such as creating storage pools and adding shares, after finishing the wizard.|

5.  On the **Summary** page, confirm the settings, and then click **Finish**.

    Depending on your settings, the **Jobs** dialog box might appear. Ensure that the job has a status of **Completed**, and then close the dialog box.

6.  To verify the newly discovered storage information, in the **Fabric** workspace, on the **Home** tab, click **Fabric Resources**. In the **Fabric** pane, expand **Storage** and click **File Servers**.

    After you add the Scale\-Out File Server, you can perform additional configuration steps as described in [Overview: configuring storage using Scale-Out File Servers in VMM](../Topic/Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

## See Also
[Creating a host cluster in VMM from existing Windows servers](../Topic/Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](../Topic/Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[Managing Scale-Out File Servers with VMM](../Topic/Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

