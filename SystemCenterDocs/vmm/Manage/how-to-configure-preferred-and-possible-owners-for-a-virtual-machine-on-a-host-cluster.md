---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to configure preferred and possible owners for a virtual machine on a host cluster
ms.technology:  virtual-machine-manager
ms.assetid:  b3395d9f-b75c-4b97-9a33-299dd2a84677
---

# How to configure preferred and possible owners for a virtual machine on a host cluster

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

If you deploy virtual machines on a host cluster, you can use Virtual Machine Manager (VMM) to configure preferred owners and possible owners for the virtual machines. By default, there are no preferred owners (there is no preference), and the possible owners include all nodes (servers) in the host cluster.

For information about other settings related to availability of virtual machines on a host cluster, see [Configuring availability options for virtual machines in VMM](Configuring-availability-options-for-virtual-machines-in-VMM.md).

**Account requirements** To complete this procedure you must be a member of the Administrator or Delegated Administrator user role, or a self-service user who has the **Deploy** action in the scope of their user role.

### To configure preferred and possible owners for a virtual machine

1.  In the **VMs and Services** workspace, navigate to the host on which the virtual machine is deployed. In the results pane, right-click the virtual machine, and then click **Properties**.

2.  Click the **Settings** tab and configure the options:

    -   To control which nodes (servers) in the cluster will own the virtual machine most of the time, configure the preferred owners list.

    -   To prevent a virtual machine from being owned by a particular node, configure the possible owners list, omitting only the nodes that should never own the virtual machine.

3.  In the properties sheet, click **OK**.

4.  To verify the settings, reopen the properties sheet.



