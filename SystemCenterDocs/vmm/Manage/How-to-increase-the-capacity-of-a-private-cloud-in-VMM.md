---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to increase the capacity of a private cloud in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  abc04f90-e31f-4696-9cec-56cc7895af0c
---

# How to increase the capacity of a private cloud in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use this procedure to increase the capacity of a private cloud in Virtual Machine Manager (VMM).

> [!NOTE]
> -   You can decidewhether to limit the placement of virtual machines to stay within the aggregate capacity of a particular cloud. For non-replica virtual machines, it is a best practice to stay within the aggregate capacity. If you have replica virtual machines, you might want to exceed the specified capacity of a preconfigured cloud. In other words, you might want to overcommit the cloud as you place replica virtual machines.
> 
>     For example, on a cloud where the **Memory** setting for **Total Capacity** is 32 GB, you could uncheck the **Use Maximum** box and set the **Assigned Capacity** to 64. After that, if you were placing replica virtual machines, you could choose that cloud as a placement option even if the aggregate load was greater than 32 GB (and less than 64 GB).
> -   If the capacity of the private cloud already equals the capacity of the underlying fabric, unless you are overcommitting capacity as described in the previous item, you must first add hosts or other fabric resources, make them available to the private cloud, and then increase private cloud capacity. To modify any private cloud resource settings, open the private cloud properties (as described in the following procedure), and then click the desired tab.

### To increase the capacity of a private cloud

1.  Before you increase private cloud capacity, you can view used and available resource information for private clouds and host groups. To do this, follow these steps:

    1.  Open the **VMs and Services** workspace.

    2.  In the **VMs and Services** pane, locate and then click a private cloud or host group for which you want to view usage information.

    3.  On the **Home** tab, in the **Show** group, click **Overview**.

        Usage information is displayed in the **Overview** pane.

2.  To increase capacity, in the **VMs and Services** pane, expand **Clouds**, and then click the private cloud for which you want to increase the capacity.

3.  On the **Folder** tab, click **Properties**.

4.  In the *Cloud Name* **Properties** dialog box, click the **Capacity** tab.

5.  Under **Cloud capacity**, modify the desired capacity settings, and then click **OK**.





