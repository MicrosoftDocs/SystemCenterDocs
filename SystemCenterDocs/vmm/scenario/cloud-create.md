---
ms.assetid: 8e171d54-0071-48fb-803e-26895dfefe93
title: Create a private VMM cloud
description: This article provides instructions for creating a private cloud in the VMM fabric
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/16/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: virtual-machine-manager
---


# Scenario: Create a private cloud

>Applies To: System Center 2016 - Virtual Machine Manager

This article provides instructions for creating a private cloud in System Center 2016 - Virtual Machine Manager (VMM).

You can create a private cloud from a host groups, or from a VMware resource pool. Host groups can contains a single host type or a mix of Hyper-V and VMware ESX hosts.


## Before you start

 - You need to be a VMM administrator, or a member of the Delegated Administrator user group, with a scope that includes the host groups you'll use for the cloud.
 - You need to have the VMM fabric in place. [Learn more](../plan/plan-fabric.md)
 - You should have one or more [Hyper-V](../manage/manage-compute-hyper-v-overview.md) or [VMware](../manage/manage-compute-add-vmware.md) virtualization hosts in the fabric. If you're creating a cloud from a VMware resource pool,  a vCenter Server and the VMware ESX host or host cluster that contains the VMware resource pool must be in the VMM fabric.
-   If you want to provide [self-service users](../manage/manage-self-service.md) the ability to store virtual machines to the VMM library, then create a library share, or create a folder in a library share that will serve as the storage location. [Learn more](../manage/manage-library-overview.md). Note that self-service users must have the **Store and re-deploy** permission to store their virtual machines.
- If you configure the stored virtual machine path and read-only library shares when you run the Create Cloud Wizard. The self-service user role data path is specified when you create a self-service user role or modify the properties of a self-service user role. For example, outside VMM, you could create the **\\\VMMServer01\Finance\StoredVMs** path, and then add the **VMMServer01\Finance** library share to the VMM library.
- If you want to assign read-only shares to the private cloud, where administrators can store read-only resources such as .iso files that they want to make available to self-service users, make sure that one or more library shares exists that you can assign as the read-only library shares. Note that self-service users must have the **Author** permission to access the resources.
- The library shares that you designate as read-only resource locations for the private cloud must be unique when compared to the library share or shares that are used for stored virtual machines and for the user role data path that is specified for a self-service user role. For example, if the user role data path for a self-service user role is **\\\VMMServer01\Finance**, you cannot create a stored virtual machine path of **\\\VMMServer01\Finance\StoredVMs**. However, if the user role data path is **\\\VMMServer01\Finance\FinanceUserRoleData**, you could specify **\\\VMMServer01\Finance\StoredVMs** as the stored virtual machine path, as the full path is unique. You could also create entirely separate library shares.



## Create a private cloud from a host group

1. Click **VMs and Services** > **Create** > **Create Cloud**, to open the Create Cloud Wizard.
2. In **General**, specify a name and optional description for the cloud.
3. Specify whether the cloud will support shielded VMs.
4. In **Resources** > **Host groups**, select the groups you want to add to the cloud. Then click **Next**.
5. In **Logical Networks**, select each logical network that you want to make available to the private cloud, and then click **Next**. Only logical networks that are associated with physical network adapters on hosts in the selected host groups appear in the list.
6. In **Load Balancers**, select each load balancer that you want to make available to the private cloud, and then click **Next**. Only load balancers that are associated with the selected host groups appear in the list.
7. In **VIP Profiles**, select each VIP template that you want to make available to the private cloud, and then click **Next**.
8. In **Port Classifications**, select each port classification that you want to make available to the cloud, and the click **Next**.
9. In **Storage**, if you have storage managed by VMM, select each storage classification that you want to make available to the private cloud, and then click **Next**. Only storage classifications for storage pools that are assigned to the selected host groups appear in the list.
10. In **Library** > **Stored VM path**, click the library share you want to use for self-service uers to store VMs. Then click **OK**.
11. In **Read-only library shares** >  **Add**, select one or more library shares where administrators can provide read-only resources to cloud users. Click **OK** > **Next**.
12. In **Capacity**, set capacity limits for the private cloud, and then click **Next**. You can either accept the default values, or clear the **Use Maximum** check boxes and set quotas for the following resources:

    **Quota Type** | **Description**
    --- |---
    **Virtual CPUs**  |Sets a limit on processing capacity within the private cloud that is equivalent to the capacity that can be provided by a specified number of CPUs. Applied against running virtual machines. Setting a CPU quota does not guarantee contiguous capacity; it only guarantees total CPU capacity available among hosts in the private cloud.
    **Memory** | Sets a quota on memory (in gigabytes) that is available for virtual machines that are deployed on the private cloud. Applied against running virtual machines only. Setting a memory quota does not guarantee contiguous capacity. For example, the private cloud might have available 2 GB of memory on one host and 2 GB of memory on another.
    **Storage**  |Sets a quota on storage capacity (in gigabytes) that is available to virtual machines that are deployed on the private cloud. For dynamic virtual hard disks, quota calculations are based on maximum size.
    **Custom quota (points)** | Sets a quota on virtual machines that are deployed on the private cloud based on total quota points that are assigned to the virtual machines through their virtual machine templates. Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated size of the virtual machines. Custom quotas are provided for backward compatibility with self-service user roles that were created in VMM 2008 R2.
    **Virtual machines** | Limits the total number of virtual machines that can be deployed on the private cloud.

13. In **Capability Profiles**, select each virtual machine capability profile that you want to add, and then click **Next**. Select the capability profiles that match the type of hypervisor platforms that are running in the selected host groups. The built-in capability profiles represent the minimum and maximum values that can be configured for a virtual machine for each supported hypervisor platform.
14. In **Replication Groups**, select the replication groups for the private cloud, and click **Next**.
15. In **Summary** page, confirm the settings, and then click **Finish**. View status in **Jobs**. To verify that the private cloud was created, check **VMs and Services** > **Clouds**. You can also verify in **Library** > **Cloud Libraries**, to view the read-only library shares.


## Create a private cloud from a VMware resource pool

1. Click **VMs and Services** > **Create** > **Create Cloud**, to open the Create Cloud Wizard.
2. In **General**, specify a name and optional description for the cloud.
3. In **Resources**, select **VMware resource pools** > **Next**.
4. In **Logical Networks**, select each logical network that you want to make available to the private cloud, and then click **Next**.
5. In **Load Balancers**, select each load balancer that you want to make available to the private cloud, and then click **Next**. Only load balancers that are associated with the selected host groups appear in the list.
6. In **VIP Profiles**, select each VIP template that you want to make available to the private cloud, and then click **Next**.
7. In **Storage**, click **Next**. VMM doesn't manage or assign storage classifications assigned to ESX hosts.
8. In **Library** > **Stored VM path**, click the library share you want to use for self-service users to store VMs. Then click **OK**.
9. In **Read-only library shares** >  **Add**, select one or more library shares where administrators can provide read-only resources to cloud users. Click **OK** > **Next**.
10. In **Capacity**, set capacity limits for the private cloud, and then click **Next**. You can either accept the default values, or clear the **Use Maximum** check boxes and set quotas for the following resources:

    **Quota Type** | **Description**
    --- |---
    **Virtual CPUs**  |Sets a limit on processing capacity within the private cloud that is equivalent to the capacity that can be provided by a specified number of CPUs. Applied against running virtual machines. Setting a CPU quota does not guarantee contiguous capacity; it only guarantees total CPU capacity available among hosts in the private cloud.
    **Memory** | Sets a quota on memory (in gigabytes) that is available for virtual machines that are deployed on the private cloud. Applied against running virtual machines only. Setting a memory quota does not guarantee contiguous capacity. For example, the private cloud might have available 2 GB of memory on one host and 2 GB of memory on another.
    **Storage**  |Sets a quota on storage capacity (in gigabytes) that is available to virtual machines that are deployed on the private cloud. For dynamic virtual hard disks, quota calculations are based on maximum size.
    **Custom quota (points)** | Sets a quota on virtual machines that are deployed on the private cloud based on total quota points that are assigned to the virtual machines through their virtual machine templates. Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated size of the virtual machines. Custom quotas are provided for backward compatibility with self-service user roles that were created in VMM 2008 R2.
    **Virtual machines** | Limits the total number of virtual machines that can be deployed on the private cloud.

11. In **Capability Profiles**, select **ESX Server**, and then click **Next**. The built-in capability profiles represent the minimum and maximum values that can be configured for a virtual machine for each supported hypervisor platform.
12. In **Summary** page, confirm the settings, and then click **Finish**. View status in **Jobs**. To verify that the private cloud was created, check **VMs and Services** > **Clouds**. You can also verify in **Library** > **Cloud Libraries**, to view the read-only library shares.

## Assign private clouds to user roles

After you create a private cloud, you can assign the private cloud to one or more user roles.

1. In **VMs and Services**, click the private cloud that you want to assign.
2. In **Cloud**, click **Assign Cloud**.
3. Select an existing user role, or click **Create a user role and assign this cloud** to create a new one.
