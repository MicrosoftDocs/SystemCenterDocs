---
title: How to share resources as a self-service user in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f6dd371-2b40-4e1c-85e9-ab229d30ddca
---
# How to share resources as a self-service user in VMM
If you are a self\-service user in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], you can use the following procedure to share resources. Before you can share the resources, you must own the resources, and an administrator in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] must assign the **Share** action to your self\-service user role in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. The administrator must also assign the **Receive** action to the self\-service user with whom you want to share resources.

When the necessary steps have been taken by the administrator in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can share resources that you own with other members of your self\-service user role. You can also share with everyone in another self\-service user role, or with an individual member of another self\-service user role. For example, if you are a member of a self\-service user role called “Application Developers,” you might share your service template with everyone in a self\-service user role called “Application Testers.”

If you are an administrator and want enable to resource sharing between self\-service user roles in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], see [How to enable self-service users to share resources in VMM](../Topic/How-to-enable-self-service-users-to-share-resources-in-VMM.md).

> [!NOTE]
> This procedure also can be performed by administrators. The **Access** tab for a resource lists resources that self\-service user roles can access either through sharing or through assignment. To perform this procedure, a delegated administrator must have the resource and the self\-service user role in the scope of their user role. After an administrator assigns a resource to a self\-service user role, the resource is added to the **Resources** tab of the self\-service user role.

### To share a resource as a self\-service user in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]

1.  Open the **Library** workspace.

2.  On the **Library** pane, navigate to the template or physical resource that you want to share.

3.  On the results pane, right\-click the resource and then click **Properties**.

    The **Properties** dialog box opens.

4.  Open the **Access** tab.

    The **Owner** option displays the owner of the resource and the self\-service user role under which it was created. The **Users** list displays the names of self\-service users and self\-service user roles that are sharing the resource.

5.  Under **Users**, click **Add**.

    The **Select Users** dialog box opens.

    1.  To share the resource with another member of your own self\-service user role, use the **Select** button beside **User** to select the user account.

    2.  To share the resource with other self\-service user roles, under **User Role**, select each self\-service user role that should receive the resource. Only user roles that have the **Receive** action assigned to them are available.

    3.  To share the resource with an individual user of another self\-service user role, select the user and the user role. Only the selected role member will have access to the shared resource.

    4.  Click **OK**.

6.  Click **OK** to save the updated properties.

## See Also
[Managing a self-service environment for tenants](../Topic/Managing-a-self-service-environment-for-tenants.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

