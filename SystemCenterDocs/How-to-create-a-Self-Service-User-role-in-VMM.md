---
title: How to create a Self-Service User role in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89a2e056-439c-41a0-b5da-b5153da63c6a
---
# How to create a Self-Service User role in VMM
You can use this procedure to create a Self\-Service User role in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)].

**Account requirements** Administrators and delegated administrators can create Self\-Service User roles. Delegated administrators can create Self\-Service User roles for private clouds that are in the scope of their user role.

### To create a Self\-Service User role

1.  In the **Settings** workspace, on the **Home** tab, in the **Create** group, click **Create User Role**.

2.  In the **Create User Role Wizard** on the **Name and description** page, enter a name and optional description of the Self\-Service User role, and then click **Next**.

3.  On the **Profile** page, click **Self\-Service User**, and then click **Next**.

4.  On the **Members** page, add user accounts and Active Directory groups to the role, and then click **Next**.

    > [!NOTE]
    > If you want all role members to share ownership of all virtual machines that any member creates, create a security group in Active Directory and assign that group to the user role. An alternate method for sharing resources among Self\-Service User role members is to use the **Share** and **Receive** actions, discussed later, which enable resource owners who are self\-service users to share individual resources with one or all members of a Self\-Service User role.
    > 
    > If you plan to use this user role to test deploying virtual machines and services to a private cloud, be sure to add yourself as a member.

5.  On the **Scope** page, select at least one private cloud for the Self\-Service User role, and then click **Next**.

6.  On the **Quotas** page, set quotas for each private cloud that is in the scope of the user role, and then click **Next**. If multiple private clouds are assigned to a Self\-Service User role, you will see a **Quotas** page for each private cloud.

    > [!NOTE]
    > Each quota sets an individual limit for each member of the user role. If you want all role members to share overall quotas, create a security group in Active Directory and assign that group to the user role.

    ### Quota types supported for self\-service in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

    |Quota type|Description|
    |--------------|---------------|
    |**Virtual CPUs**|Limits the total number of virtual machine CPUs that can be consumed from the private cloud.|
    |**Memory \(MB\)**|Limits the amount of virtual machine memory \(in megabytes\) that can be consumed from the private cloud.|
    |**Storage \(GB\)**|Limits the amount of virtual machine storage \(in Gigabytes\) that can be consumed from the private cloud.|
    |**Custom quota \(points\)**|Sets a quota on virtual machines deployed on the private cloud based on total quota points assigned to the virtual machines via their virtual machine templates.<br /><br />Quota points are an arbitrary value that can be assigned to a virtual machine template based on the anticipated "size" of the virtual machines. Custom quotas are provided for backward compatibility with self\-service user roles created in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] 2008 R2.|
    |**Virtual machines**|Limits the total number of virtual machines that can be deployed on a private cloud.|

    Quotas only apply to deployed virtual machines. If a Self\-Service User role has permission to store virtual machines, the quota does not apply to virtual machines that are stored in the library.

7.  On the **Resources** page, click **Add** to open the **Add Resources** dialog box. Assign hardware profiles, operating system profiles, virtual machine templates, application profiles, SQL server profiles, and service templates for the self\-service users to use during virtual machine creation.

8.  Under **Specify user role data path**, use the **Browse** button to select a path on a library share where user role members can upload and share their own resources. The user data path also is a good place to store prepared resources that should be shared only with members of this Self\-Service User role.

    Click **Next** to continue.

9. On the **Actions** page, select the actions that the self\-service users need to perform on their own virtual machines and services, and then click **Next**. To select all actions, click **Select all**.

    ### Actions available to Self\-Service User roles in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

    |Action|Description|
    |----------|---------------|
    |**Author**|Grants members permission to author templates and profiles. Users with authoring rights can create hardware profiles, operating system profiles, application profiles, SQL Server profiles, virtual machine templates and service templates.|
    |**Checkpoint**|Grants members permission to create, edit, and delete checkpoints for their own virtual machines and to restore their virtual machine to a previous checkpoint. **Note:** [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support checkpoint actions on services.|
    |**Checkpoint \(restore only\)**|Grants members permission to restore their own virtual machines to a checkpoint but not to create, edit, and delete checkpoints.|
    |**Deploy**|Grants members permission to deploy virtual machines and services from templates and virtual hard disks that are assigned to their user role. However, they do not have the right to author templates and profiles. \(Expanded in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to include creation of services\)|
    |**Deploy \(from template only\)**|Grants members permission to deploy virtual machines and services from templates that are assigned to their user role. However, they do not have any authoring rights. \(Expanded in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to include creation of services\)|
    |**Local Administrator**|Grants members permission to serve as a local Administrator on their own virtual machines. **Important:** Be sure to select the **Local Administrator** action on any Self\-Service User role that has the **Deploy \(From Template\)** action selected. This action enables those users to set the local Administrator password during virtual machine and service deployment. Self\-service users who are granted the **Deploy** action do not need this action to be able to set local Administrator credentials.|
    |**Pause and resume**|Grants members permission to pause and resume their own virtual machines and services.|
    |**Receive**|Allows members to receive resources that are shared by members of other Self\-Service User roles.|
    |**Remote connection**|Grants members permission to connect to their virtual machines from the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console or App Controller. For information about App Controller, see [App Controller](http://technet.microsoft.com/library/hh546834.aspx).|
    |**Remove**|Grants members permission to remove their own virtual machines and services.|
    |**Save**|Grants members permission to save their own virtual machines and services.|
    |**Share**|Allows members to grant resources that they own to other Self\-Service User roles. Sharable resources include hardware profiles, operating system profiles, application profiles, SQL Server profiles, virtual machine templates, virtual machines, service templates, and services. A self\-service user must be the owner of a resource to share it. The Self\-Service User role that receives the shared resource must be assigned the **Receive** action.|
    |**Shut down**|Grants members permission to perform an orderly shutdown of their own virtual machines and services.|
    |**Start**|Grants members permission to start their own virtual machines and services.|
    |**Stop**|Grants members permission to stop their own virtual machines and services.|
    |**Store and re\-deploy**|Grants members permission to store their own virtual machines in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library, and re\-deploy those virtual machines. Virtual machines stored in the library do not count against a user's virtual machine quotas. **Note:** [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not support storing services.|

10. If you selected the **Author** action, the **Run As accounts** page opens. Select Run As accounts for the Self\-Service User role to use in the templates and profiles that they use to create virtual machines and services, and then click **Next**.

11. Review the settings you have entered on the **Summary** page, and then click **Finish**.

After you create a Self\-Service User role, you can change settings using the **Properties** dialog box for the user role.

## See Also
[Managing a self-service environment for tenants](../Topic/Managing-a-self-service-environment-for-tenants.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

