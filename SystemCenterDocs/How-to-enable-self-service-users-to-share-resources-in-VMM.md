---
title: How to enable self-service users to share resources in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 542e8138-0f15-4efe-9a39-12ee9d9186d5
---
# How to enable self-service users to share resources in VMM
Use the following procedures if you are an administrator and you want to enable resource sharing between self\-service user roles in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. For a list of other procedures related to configuring self\-service, see [Managing a self-service environment for tenants](../Topic/Managing-a-self-service-environment-for-tenants.md).

If you are a self\-service user, see [How to share resources as a self-service user in VMM](../Topic/How-to-share-resources-as-a-self-service-user-in-VMM.md).

In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], a member of a self\-service user role can share the resources that she owns with other members of her self\-service user role, with another self\-service user role, or with an individual member of another self\-service user role. For example, a member of an Application Developers self\-service user role might share his service template with an Application Testers self\-service user role for pre\-production testing.

To share a resource with a member of another self\-service user role, the following conditions must be met:

-   The self\-service user who shares the resource must be the owner of the resource.

-   The resource owner must belong to a self\-service user role that has been assigned the **Share** action.

-   The resource receiver must belong to a self\-service user role that has been assigned the **Receive** action.

### To enable self\-service user roles to share resources

1.  Open the **Settings** workspace.

2.  In the **Settings** pane, expand **Security**, and click **User Roles**.

3.  In the **User Roles** pane, click the self\-service user role for which you want to enable the sharing of resources.

4.  On the **Home** tab, in the **User Role** group, click **Properties**.

    The user role **Properties** dialog box opens.

5.  On the **Actions** tab, select **Share**, and then click **OK**.

    Members of this self\-service user role can now share their own resources with members of any self\-service user role that has the **Receive** action assigned to it. Now, configure the other self\-service user role to receive resources.

6.  Open the properties of the other self\-service user role. \(In the **User Roles** pane, right\-click the user role and click **Properties**.\)

7.  On the **Actions** tab, select **Receive**, and then click **OK**.

## See Also
[Managing a self-service environment for tenants](../Topic/Managing-a-self-service-environment-for-tenants.md)
[How to share resources as a self-service user in VMM](../Topic/How-to-share-resources-as-a-self-service-user-in-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

