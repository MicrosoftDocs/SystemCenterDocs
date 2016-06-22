---
title: How to create a private cloud from a VMware resource pool in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4660c9cf-9d5d-4dbf-bdab-73035f7d023b
---
# How to create a private cloud from a VMware resource pool in VMM
You can use this procedure to create a private cloud from a VMware resource pool in Virtual Machine Manager \(VMM\).

**Account requirements** You must perform this procedure as a member of the Administrator user role or as a member of the Delegated Administrator user role where the administrative scope includes the host group where the ESX host or host cluster that contains the VMware resource pool resides.

## Prerequisites
Before you create a private cloud from a VMware resource pool, make sure that the following prerequisites are met:

-   Configure the fabric by using the procedures in [Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md). The fabric resource examples in this procedure use examples from the “Preparing the Fabric in VMM” section.

    > [!NOTE]
    > You cannot discover and manage storage for VMware ESX hosts through VMM.

-   In VMware vCenter Server, one or more resource pools must be configured. A vCenter Server and the VMware ESX host or host cluster that contains the VMware resource pool must be under VMM management. For information about how to add vCenter Server and ESX hosts to VMM management, see [VMM support for VMware](VMM-support-for-VMware.md).

-   If you want to provide self\-service users the ability to store virtual machines to the VMM library, create a folder in an existing library share that will serve as the storage location. Note that self\-service users must have the **Store and re\-deploy** permission to store their virtual machines.

    > [!IMPORTANT]
    > The library share location that you designate for stored virtual machines must be different from the shares that you designate as read\-only resource locations for the private cloud. Also, the path or part of the path must be unique when compared to the user role data path that is specified for a self\-service user role. For example, if the user role data path for a self\-service user role is \\\\VMMServer01\\Marketing, you cannot create a stored virtual machine path of \\\\VMMServer01\\Marketing\\StoredVMs. However, if the user role data path is \\\\VMMServer01\\Marketing\\MarketingUserRoleData, you could specify \\\\VMMServer01\\Marketing\\StoredVMs as the stored virtual machine path, as the full path is unique. You could also create entirely separate library shares.
    > 
    > Note that you configure the stored virtual machine path and read\-only library shares when you run the Create Cloud Wizard. The self\-service user role data path is specified when you create a self\-service user role or modify the properties of a self\-service user role.

    For example, you could create the **VMMServer01\\Marketing\\StoredVMs** path.

-   If you want to assign read\-only shares to the private cloud, where administrators can store read\-only resources such as .iso files that they want to make available to self\-service users, make sure that one or more library shares exists that you can assign as the read\-only library shares. Note that self\-service users must have the **Author** permission to access the resources.

    > [!IMPORTANT]
    > The library shares that you designate as read\-only resource locations for the private cloud must be unique when compared to the library share or shares that are used for stored virtual machines and for the user role data path that is specified for a self\-service user role.

    For example, you could use library shares called **SEALibrary** and **NYLibrary**.

    > [!NOTE]
    > For more information about self\-service user permissions, see [How to create a Self-Service User role in VMM](How-to-create-a-Self-Service-User-role-in-VMM.md).

#### How to create a private cloud from a VMware resource pool

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create Cloud**.

    The Create Cloud Wizard opens.

3.  On the **General** page, enter a name and description for the private cloud, and then click **Next**.

    For example, you could enter the name **Marketing**, and the description **Private cloud for virtual machines and services in the marketing department**.

4.  On the **Resources** page, click **VMware resource pools**, click an available VMware resource pool, and then click **Next**.

    > [!NOTE]
    > For the resource pool to be available for selection, the VMware ESX host or host cluster that contains the VMware resource pool must be under VMM management.

5.  On the **Logical Networks** page, select each logical network that you want to make available to the private cloud, and then click **Next**.

    For example, you might select a logical network called **Tenants**.

6.  On the **Load Balancers** page, select each load balancer that you want to make available to the private cloud, and then click **Next**.

    For example, you might select a load balancer called **LoadBalancer01.contoso.com**.

    > [!TIP]
    > When you complete the wizard, if you do not have a fabric resource configured, you can click **Next** to move to the next page. Note that you can add or remove private cloud resources and modify other private cloud settings after you complete the wizard. To do this, right\-click the private cloud, and then click **Properties**.

7.  On the **VIP Profiles** page, select each VIP template that you want to make available to the private cloud, and then click **Next**.

    For example, you might select a VIP template called **Web tier \(HTTPS traffic\)**.

8.  On the **Storage** page, click **Next**.

    > [!NOTE]
    > You cannot use VMM to manage or assign storage classifications for storage that is assigned to ESX hosts.

9. On the **Library** page, do the following:

    1.  Next to the **Stored VM path** box, click **Browse**. In the **Select Destination Folder** dialog box, expand the library server, click the library share or the folder in a library share that you want to use as the location for self\-service users to store virtual machines, and then click **OK**.

        For example, you might click the **StoredVMs** folder that you created in the **VMMServer01\\Marketing** library share.

    2.  In the **Read\-only library shares** area, click **Add**, select one or more library shares to use as the location where administrators can store read\-only resources that they want to make available to self\-service users, click **OK**, and then click **Next**.

        For example, you might select library shares called **SEALibrary** and **NYLibrary**.

10. On the **Capacity** page, set capacity limits for the private cloud, and then click **Next**. You can either accept the default values, or clear the **Use Maximum** check boxes and set quotas for the following resources:

    |Quota Type|Description|
    |--------------|---------------|
    |**Virtual CPUs**|Sets a limit on processing capacity within the private cloud that is equivalent to the capacity that can be provided by a specified number of CPUs. Applied against running virtual machines. Setting a CPU quota does not guarantee contiguous capacity; it only guarantees total CPU capacity available among hosts in the private cloud.|
    |**Memory**|Sets a quota on memory \(in gigabytes\) that is available for virtual machines that are deployed to the private cloud. Applied against running virtual machines only. Setting a memory quota does not guarantee contiguous capacity. For example, the private cloud might have available 2 GB of memory on one host and 2 GB of memory on another.|
    |**Storage**|Sets a quota on storage capacity \(in gigabytes\) that is available to virtual machines that are deployed to the private cloud. For dynamic virtual hard disks, quota calculations are based on maximum size.|
    |**Custom quota \(points\)**|Sets a quota on virtual machines that are deployed to the private cloud based on total quota points that are assigned to the virtual machines through their virtual machine templates. Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated size of the virtual machines. Custom quotas are provided for backward compatibility with self\-service user roles that were created in VMM 2008 R2.|
    |**Virtual machines**|Limits the total number of virtual machines that can be deployed to a private cloud.|

11. On the **Capability Profiles** page, select **ESX Server**, and then click **Next**. The built\-in capability profiles represent the minimum and maximum values that can be configured for a virtual machine for each supported hypervisor platform.

    > [!TIP]
    > In the **Library** workspace, you can also create custom capability profiles to limit the resources that are used by virtual machines that are created in the private cloud. To view the settings that are associated with a built\-in capability profile or to create a custom capability profile, open the **Library** workspace, expand **Profiles**, and then click **Capability Profiles**. You can view the properties of existing profiles, or to create a new profile, on the **Home** tab, in the **Create** group, click **Create** > **Capability Profile**. If you do create a custom capability profile for ESX, make sure that fabric compatibility is set to **ESX Server**.

12. On the **Summary** page, confirm the settings, and then click **Finish**.

    The **Jobs** dialog box appears. Make sure that the job has a status of **Completed**, and then close the dialog box.

13. To verify that the private cloud was created, in the **VMs and Services** workspace, expand **Clouds**.

    The private cloud that you created should appear.

    > [!TIP]
    > To view information about used and available resources in the private cloud, in the **VMs and Services** workspace, expand **Clouds**, and then click the private cloud. On the **Home** tab, in the **Show** group, click **Overview**. In the **Show** group, you can also click **VMs** or **Services** to view information about virtual machines and services that are deployed to the private cloud.

14. To verify that the private cloud library was created, open the **Library** workspace, and then expand **Cloud Libraries**. A private cloud library is listed that matches the private cloud name. If you expand the private cloud library, depending on what you configured, the read\-only library shares are listed together with a **Stored Virtual Machines and Services** node.

After you create a private cloud, you can assign the private cloud to one or more user roles. To assign the private cloud to an existing user role, or to assign the private cloud and create a user role at the same time, in the **VMs and Services** workspace, click the private cloud that you want to assign. Then, on the **Home** tab, in the **Cloud** group, click **Assign Cloud** to open the **Assign Cloud** dialog box. If you select an existing user role, you can modify the properties of the user role. If you select **Create a user role and assign this cloud**, the Create User Role Wizard opens.

<<<<<<< HEAD
=======
For information about how to create a self\-service user role, see [How to create a Self-Service User role in VMM](How-to-create-a-Self-Service-User-role-in-VMM.md).

## See Also
[Creating a Private Cloud in VMM](assetId:///6fbce258-d10e-4bc0-91fc-de4f5e00905f)
[Overview: creating a private cloud with VMM](Overview--creating-a-private-cloud-with-VMM.md)
[Managing private clouds with VMM](Managing-private-clouds-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)
>>>>>>> cbd5a0248f8f546ef51e06ea65d5578a2007427e


