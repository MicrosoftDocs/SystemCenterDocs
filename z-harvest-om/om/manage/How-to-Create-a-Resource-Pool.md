---
title: How to Create a Resource Pool
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e1add1e-56df-435b-9b27-ba6eee74ace9
author:mgoedtel
manager:cfreemanwa
---
# How to Create a Resource Pool
A new feature in [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] is the *resource pool*. A resource pool is a collection of management servers used to distribute work amongst themselves and take over work from a failed member.  
  
You can use resource pools for:  
  
-   Monitoring network devices.  
  
-   Monitoring UNIX and Linux computers.  
  
Resource pools ensure the continuity of monitoring by providing multiple management servers that can take on monitoring workflows if one of the management servers becomes unavailable. You can create resource pools for specific purposes. For example, you might create a resource pool of management servers that are located in the same geographic area to provide network device monitoring.  
  
When [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] is installed, three resource pools are created: All Management Servers Resource Pool, Notifications Resource Pool, and AD Assignment Resource Pool. All management servers are automatically members of these resource pools. For information about removing a management server from the Notifications Resource Pool and AD Assignment Resource Pool, see [Modifying Resource Pool Membership](../../om/manage/How-to-Create-a-Resource-Pool.md#bkmk_modifyingresourcepoolmembership).  
  
> [!NOTE]  
> The membership of the All Management Servers Resource Pool is read\-only.  
  
For information about configuring resource pools with managed UNIX and Linux computers and for configuring certificates, see [Managing Resource Pools for UNIX and Linux Computers](../../om/manage/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md).  
  
## <a name="bkmk_tocreatearesourcepool"></a>To create a resource pool  
  
1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.  
  
2.  Click **Administration**.  
  
3.  In the navigation pane, click **Resource Pools**.  
  
4.  In the **Tasks** pane, click **Create Resource Pool**.  
  
5.  In the **Create Resource Pool** wizard, on the **General Properties** page, enter a name and, optionally, a description for the resource pool, and then click **Next**.  
  
6.  On the **Pool Membership** page, click **Add**.  
  
7.  In the **Member Selection** window, enter text to filter the search results if desired, and then click **Search**. If you click **Search** without entering anything in the filter field, all available management servers will be displayed.  
  
8.  In **Available items**, select the servers that you want in the resource pool, click **Add**, and then click **OK**.  
  
9. Click **Next**.  
  
10. On the **Summary** page, review the settings and then click **Create**.  
  
11. When the wizard completes, click **Close**.  
  
## <a name="bkmk_modifyingresourcepoolmembership"></a>Modifying Resource Pool Membership  
When you view the resource pools in the **Administration** workspace, you will see that resource pools that you create have a manual membership type and resource pools created when Operations Manager was installed have an automatic membership type, as shown in the following image.  
  
![](3ec2b1a6-ee6d-454e-8dc6-52ae6a8d41f0)  
  
By default, all management servers are members of the resource pools created when Operations Manager is installed, and any management servers added to the management group are automatically added to the resource pools that have an automatic membership type. You can remove individual management servers from those resource pools, however that will change the membership type to manual. If you add a management server to a management group after the membership type of the resource pools created when Operations Manager was installed is changed to manual, you must add the management server to the resource pool manually.  
  
#### To remove a member from an automatic resource pool  
  
1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.  
  
2.  Click **Administration**.  
  
3.  In the navigation pane, click **Resource Pools**.  
  
4.  In the results pane, click the resource pool that you want to modify.  
  
5.  In the **Tasks** pane, click **Manual Membership**, and then click **Yes** in the **Manual Membership** message.  
  
    > [!IMPORTANT]  
    > When you click **Yes**, the membership type of the selected resource pool changes to manual. Even if you make no changes to the resource pool membership and cancel the properties dialog box, the membership type will remain manual after this step.  
  
6.  On the **General Properties** page for the resource pool, click **Next**.  
  
7.  On the **Pool Membership** page, click the management servers that you want to remove from the resource pool, click **Remove**, and then click **Next**.  
  
8.  On the **Summary** page, click **Save**.  
  
## See Also  
[General Tasks in Operations Manager_1](../Topic/General%20Tasks%20in%20Operations%20Manager_1.md)  
[Managing Alerts](../../om/manage/Managing-Alerts.md)  
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](../../om/manage/How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)  
[Creating and Managing Groups](../../om/manage/Creating-and-Managing-Groups.md)  
[Running Tasks in Operations Manager](../../om/manage/Running-Tasks-in-Operations-Manager.md)  
[Connecting Management Groups in Operations Manager](../../om/manage/Connecting-Management-Groups-in-Operations-Manager.md)  
[Managing Resource Pools for UNIX and Linux Computers](../../om/manage/Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)  
[Using Operations Manager Shell](../../om/manage/Using-Operations-Manager-Shell.md)  
  
