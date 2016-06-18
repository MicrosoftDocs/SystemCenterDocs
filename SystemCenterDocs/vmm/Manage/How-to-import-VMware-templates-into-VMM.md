---
title: How to import VMware templates into VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee39fd79-6eab-493a-98dd-09304108c1fb
---
# How to import VMware templates into VMM
You can use the following procedure to import a VMware template to the Virtual Machine Manager \(VMM\) library.

For you to complete this procedure, a VMware template must exist. Make sure that the server that is running vCenter Server, and that contains the template, is under VMM management. For more information, see [How to add a VMware vCenter Server to VMM](How-to-add-a-VMware-vCenter-Server-to-VMM.md).

> [!NOTE]
> You cannot install VMware Tools through VMM. Therefore, we recommend that you install the tools for Windows\-based guest operating systems on the virtual machine before you use vCenter Server to create the template.

### To import a template from vCenter Server

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Import** group, click **Import VMware Template**.

3.  In the **Import VMware Templates** dialog box, select the check box next to each VMware template that you want to import, and then click **OK**.

4.  To verify that the template was added, in the **Library** pane, expand **Templates**, and then click **VM Templates**.

    In the **Templates** pane, verify that the template appears.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)


