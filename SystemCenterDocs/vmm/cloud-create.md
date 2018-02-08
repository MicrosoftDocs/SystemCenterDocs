---
ms.assetid: 8e171d54-0071-48fb-803e-26895dfefe93
title: Create a private VMM cloud
description: This article provides instructions for creating a private cloud in the VMM fabric
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 02/05/2018
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---


# Scenario: Create a private cloud

This article provides instructions for creating a private cloud in System Center - Virtual Machine Manager (VMM).

You can create a private cloud from a host group, or from a VMware resource pool. Host groups can contain a single host type or a mix of Hyper-V and VMware ESX hosts.

> [!NOTE]
> You must be a VMM administrator, or a member of the delegated Administrators user group, with a scope that includes the host groups you'll use for the cloud.

## Before you start

  - You need to have the VMM fabric in place. [Learn more](plan-compute.md).
  - You should have one or more [Hyper-V](hyper-v-hosts.md) or [VMware](manage-vmware-hosts.md) virtualization hosts in the fabric. If you're creating a cloud from a VMware resource pool, a vCenter Server and the VMware ESX host or host cluster that contains the VMware resource pool must be available in the VMM fabric.
    - If you want to provide [self-service users](self-service.md) the ability to store virtual machines to the VMM library, then create a library share, or create a folder in a library share that will serve as the storage location. [Learn more](manage-library-server.md).

        > [!NOTE]
        > Self-service users must have the **Store and re-deploy** permission to store their virtual machines.

    - You can add independently created library shares as read-only library shares in the VMM when you run the Create Cloud Wizard. For example, outside the VMM, you cannot create the **\\\VMMServer01\Finance\StoredVMs** path, and then add the **\\\VMMServer01\Finance** library share to the VMM library.
    - The self-service user role data path is specified when you create a self-service user role or modify the properties of a self-service user role.
    - If you want to assign read-only shares to the private cloud, where administrators can store read-only resources such as .iso files that they want to make available to self-service users, make sure that one or more library shares exists that you can assign as the read-only library shares.

        > [!NOTE]
        > Self-service users must have the **Author** permission to access the resources.

    - The library shares that you designate as read-only resource locations for the private cloud must be unique when compared to the library share or shares that are used for stored virtual machines and for the user role data path that is specified for a self-service user role. For example, if the user role data path for a self-service user role is **\\\VMMServer01\Finance**, you cannot create a stored virtual machine path of **\\\VMMServer01\Finance\StoredVMs**. However, if the user role data path is **\\\VMMServer01\Finance\FinanceUserRoleData**, you could specify **\\\VMMServer01\Finance\StoredVMs** as the stored virtual machine path, as the full path is unique. You could also create entirely separate library shares.

## Create a private cloud from a host group

1. Click **VMs and Services** > **Create** > **Create Cloud**, to open the Create Cloud Wizard.
2. In **General**, specify a **Name** and optional description for the cloud.
3. Specify whether the cloud will support shielded VMs.
4. In **Resources** > **Host groups**, select the groups you want to add to the cloud. Then click **Next**.
5. In **Logical Networks**, select each logical network that you want to make available to the private cloud, and then click **Next**.

    **Note**: Only logical networks that are associated with the physical network adapters on hosts in the selected host groups appear in the list.

6. In **Load Balancers**, select each load balancer that you want to make available to this private cloud, and then click **Next**.

    **Note**: Only load balancers that are associated with the selected host groups appear in the list.

7. In **VIP Templates**, select each VIP template that you want to make available to the private cloud, and then click **Next**.
8. In **Port Classifications**, select each port classification that you want to make available to the cloud, and then click **Next**.
9. In **Storage**, if you have storage managed by VMM, select each storage classification that you want to make available to the private cloud, and then click **Next**.

    **Note**: Only storage classifications for storage pools that are assigned to the selected host groups appear in the list.
10. In **Library** > **Stored VM path**, browse and select the library share you want to use for the self-service users to store VMs. Click **OK**.
11. In **Read-only library shares** >  **Add**, select one or more library shares where administrators can provide read-only resources to cloud users. Click **OK** and then click **Next**.
12. In **Capacity**, set capacity limits for the private cloud, and then click **Next**. You can either accept the default values, or clear the **Use Maximum** check boxes and set quotas for the following resources:

    **Quota Type** | **Description**
    --- |---
    **Virtual CPUs**  |Sets a limit on processing capacity within the private cloud that is equivalent to the capacity that can be provided by a specified number of CPUs. Applied against running virtual machines. Setting a CPU quota does not guarantee contiguous capacity; it only guarantees total CPU capacity available among hosts in the private cloud.
    **Memory** | Sets a quota on memory (in gigabytes) that is available for virtual machines that are deployed on the private cloud. Applied against running virtual machines only. Setting a memory quota does not guarantee contiguous capacity. For example, the private cloud might have 2 GB of memory available on one host and 2 GB of memory on the other.
    **Storage**  |Sets a quota on storage capacity (in gigabytes) that is available to virtual machines that are deployed on the private cloud. For dynamic virtual hard disks, quota calculations are based on maximum size.
    **Custom quota (points)** | Sets a quota on virtual machines that are deployed on the private cloud based on the total quota points that are assigned to the virtual machines through their virtual machine templates. Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated size of the virtual machines. Custom quotas are provided for backward compatibility with self-service user roles that were created in VMM 2008 R2.
    **Virtual machines** | Limits the total number of virtual machines that can be deployed on the private cloud.

13. In **Capability Profiles**, select each virtual machine capability profile that you want to add, and then click **Next**. Select the capability profiles that match the type of hypervisor platforms that are running in the selected host groups. The built-in capability profiles represent the minimum and maximum values that can be configured for a virtual machine for each supported hypervisor platform.
14. In **Replication Groups**, select the replication groups for the private cloud, and click **Next**.

15. In **Summary** page, confirm the settings, and then click **Finish**.

View status in **Jobs** and ensure the job is complete.

To verify that the private cloud was created, check **VMs and Services** > **Clouds**. You can also verify in **Library** > **Cloud Libraries**, to view the read-only library shares.

::: moniker range="sc-vmm-1801"

### Assign Storage QoS Policies while creating  a cloud

1. Follow the steps until 14 in the [above procedure](#create-a-private-cloud-from-a-host-group).

2. In **Storage QoS Policies**, select the policies that you want to assign to this cloud.

3. Proceed with rest of the steps and complete the wizard.

::: moniker-end

## Create a private cloud from a VMware resource pool

1. Click **VMs and Services** > **Create** > **Create Cloud**, to open the Create Cloud Wizard.
2. In **General**, specify a **Name** and optional description for the cloud.
3. In **Resources**, select **VMware resource pools** > **Next**.
4. In **Logical Networks**, select each logical network that you want to make available to the private cloud, and then click **Next**.
5. In **Load Balancers**, select each load balancer that you want to make available to the private cloud, and then click **Next**. Only load balancers that are associated with the selected host groups appear in the list.
6. In **VIP Templates**, select each VIP template that you want to make available to the private cloud, and then click **Next**.
7. In **Storage**, click **Next**. VMM doesn't manage or assign storage classifications assigned to ESX hosts.
8. In **Library** > **Stored VM path**, browse and select the library share you want to use for self-service users to store VMs, click **OK**.
9. In **Read-only library shares** >  **Add**, select one or more library shares where administrators can provide read-only resources to cloud users. Click **OK** and then click **Next**.
10. In **Capacity**, set capacity limits for the private cloud, and then click **Next**. You can either accept the default values, or clear the **Use Maximum** check boxes and set quotas for the following resources:

    **Quota Type** | **Description**
    --- |---
    **Virtual CPUs**  | Sets a limit on processing capacity within the private cloud that is equivalent to the capacity that can be provided by a specified number of CPUs. Applied against running virtual machines. Setting a CPU quota does not guarantee contiguous capacity; it only guarantees total CPU capacity available among hosts in the private cloud.
    **Memory** | Sets a quota on memory (in gigabytes) that is available for virtual machines that are deployed on the private cloud. Applied against running virtual machines only. Setting a memory quota does not guarantee contiguous capacity. For example, the private cloud might have 2 GB of memory available on one host and 2 GB of memory on the other.
    **Storage**  | Sets a quota on storage capacity (in gigabytes) that is available to virtual machines that are deployed on the private cloud. For dynamic virtual hard disks, quota calculations are based on maximum size.
    **Custom quota (points)** | Sets a quota on virtual machines that are deployed on the private cloud based on total quota points that are assigned to the virtual machines through their virtual machine templates. Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated size of the virtual machines. Custom quotas are provided for backward compatibility with self-service user roles that were created in VMM 2008 R2.
    **Virtual machines** | Limits the total number of virtual machines that can be deployed on the private cloud.

11. In **Capability Profiles**, select **ESX Server**, and then click **Next**. The built-in capability profiles represent the minimum and maximum values that can be configured for a virtual machine for each supported hypervisor platform.
12. In **Summary** page, confirm the settings, and then click **Finish**.

View status in **Jobs** and ensure the job is complete.

To verify that the private cloud was created, check **VMs and Services** > **Clouds**. You can also verify in **Library** > **Cloud Libraries**, to view the read-only library shares.

::: moniker range="sc-vmm-1801"

## Assign storage QoS policies to a private cloud
System Center 1801 - Virtual Machine Manager (SCVMM) supports storage QoS policies on a private cloud.

The VMM fabric admin can now offer the storage QoS policies in the cloud. Tenant admins and self-service users can consume these while deploying the VMs and services. This will enable the cloud providers to guarantee and/or limit the amount of storage performance as per the subscription opted by the tenants.  

The fabric admin can now offer storage QoS policies, while authoring the VMM private clouds. After which, the authorized users (admin and self-service users) with access to this cloud can consume the available QoS policies for provisioning VMs and Services on the cloud.

> [!NOTE]

> A cloud with at least one QoS policy is offered, will not allow the deployment of disks without a policy. This helps in preventing the cloud consumers to pick infinite resources with a null policy. Also, the change in IOPS by self-service users will not be allowed after this release, to avoid the same scenario of selecting unauthorized performance.

**Storage QoS Policies** option in the **Create cloud** wizard helps the fabric admin to select the list of policies, which should be made available for the cloud consumers.


**follow these steps**:

1. Follow the [create a private cloud from a host group](#create-a-cloud-from-a-host-group) procedure until step 14.
2. In **Storage QoS Policies**, select the policies that you want to assign to this cloud.
3. proceed to step 15, complete the remaining steps.
4. Review the summary and click **Finish**.

> [!NOTE]

> This list contains only those policies that are available in scope of all the clusters selected in the Resources section of the cloud wizard. This helps the self-service user to choose between the available plans, even after the VM is placed .

 
**On Upgrade**
1.	After the upgrade, the existing clouds will not have any QoS policy in their offering. Admin needs to update the cloud with the policy offerings.
2.	The existing VMs on the cloud, which have disks with a QoS policy already assigned, will go to inconsistent state. Their policy stays intact, but the VMM UI displays it as blank. Admins can either remove those policies, or offer these   in the affected clouds.
3. Proceed with rest of the step and complete the wizard.

::: moniker-end

## Assign private clouds to user roles

After you create a private cloud, you can assign the private cloud to one or more user roles.

1. In **VMs and Services**, click the private cloud that you want to assign.
2. Right-click the selected cloud, click **Assign Cloud**.
3. Select an existing user role, or click **Create a user role and assign this cloud** to create a new one.
