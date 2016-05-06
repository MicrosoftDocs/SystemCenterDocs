---
title: How to create an updated service template in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9a7e2c9-03a0-4a3e-80f3-ed2b1798027f
---
# How to create an updated service template in VMM
To update a deployed service in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], you must first make a copy of the service template on which the deployed service is based. After you have made a copy of the service template, you will need to provide a new release value for the service template and you will need to make the necessary updates to the service template.

Use the following procedure to copy a service template for the purpose of updating an existing service.

### To create an updated service template

1.  In the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] console, open the Library workspace, expand the **Templates** node, and then click **Service Templates**.

2.  In the **Templates** pane that lists the available service templates, select the service template that you want to copy.

    > [!TIP]
    > When you select a service template, the detail pane displays the services that have been deployed using that service template.

3.  On the **Service Template** tab, in the **Create** group, click **Copy**.

    A copy of the service template is made and appears in the **Templates** pane. The new service template has the same name as the service template that you copied, but the release value is set to "Copy of <*original release value*>."  For example, if the original service template had a release value of **1.0**, the release value of the new service template would be **Copy of 1.0**.

4.  In the **Templates** pane, right\-click the new service template, and then click **Properties**.

5.  In the **Properties** dialog box, on the **General** page, enter a new release value \(for example, type **2.0**\), and then click **OK**.

At this point, make the necessary updates to the new service template by using the Service Template Designer. For more information about configuring a service template, see [Creating service templates in VMM](Creating-service-templates-in-VMM.md).

> [!NOTE]
> If you are working in the Service Template Designer and you try to save changes to a service template that is being used as the basis for a deployed service, you will be prompted to save the service template with a new release value.

## See Also
[Updating services in VMM](Updating-services-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


