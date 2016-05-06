---
title: How to update a service template to use an updated resource in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7c5d2f9-62fa-4c65-9065-4e04b9078a4d
---
# How to update a service template to use an updated resource in VMM
When a resource is updated in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] and it is referenced by a service template, you must copy and update the service template so that it uses the updated resource.

Use the following procedure to update a service template when one of its dependent resources has been updated.

### To update a service template to use an updated resource

1.  In the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, open the Library workspace, expand the **Templates** node, and then click **Service Templates**.

2.  In the **Templates** pane that lists the available service templates, locate the service template that you want to update.

    Service templates referencing outdated resources display “Outdated” in the **Update Status** column.

3.  Confirm the dependent resources that need updating by right\-clicking the service template and then selecting **View Updated Resources**.

    > [!NOTE]
    > This option is unavailable if dependent resources have not been updated.

    The **View Updated Resources** dialog box opens and displays the most recent version of resources used by this service template.

4.  In the **Templates** pane of the Library workspace, right\-click the service template that you want to update, and then select **Copy and Update**.

    > [!NOTE]
    > This option is unavailable if dependent resources have not been updated.

    A copy of the current service template is created and the outdated resource is replaced with the most recent release from the same family.

5.  Publish the updated service template and then apply the updated template to the deployed service. For instructions, see [How to apply updates to a deployed service in VMM](How-to-apply-updates-to-a-deployed-service-in-VMM.md).

## See Also
[Updating services in VMM](Updating-services-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


