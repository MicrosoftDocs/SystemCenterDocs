---
title: How to create a service template in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1efb6377-be9f-46e7-8101-f4258f92d76e
---
# How to create a service template in VMM
In [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application. In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you use the Service Template Designer to create a service template, which defines the configuration of the service. After you create the service template, you can add tiers and networking components to the service template. For more information, see [Overview: creating and deploying services in VMM](../Topic/Overview--creating-and-deploying-services-in-VMM.md).

## Create a new service template
Use the following procedure to create and save a new service template.

**Account requirements:** Services templates can be created by administrators, by delegated administrators, and by members of self\-service user roles that have the **Author** action in their scope.

#### To create a new service template by using the Service Template Designer

1.  In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create Service Template**.

3.  In the **New Service Template** dialog box, do the following:

    -   In the **Name** text box, provide a name for the service template.  For example, type **Finance Application**.

    -   In the **Release** text box, provide a value to indicate the version of the service template.  For example, type **1.0** or type **Beta**.

        The release value is important for when you update a service. The release value helps you to identify the version of the service template. For more information about updating a service, see [Updating services in VMM](../Topic/Updating-services-in-VMM.md).

    -   Under **Patterns**, select the pattern on which you want to base your service template. For example, if you select **Two Tier Application**, your service template will begin with two tiers.

    After you complete your selections, click **OK**.

    Depending on the pattern that you selected, the canvas area of the Service Template Designer may be empty or may contain some default tiers. For information about adding tiers and networking components to the service template, see the following topics:

    -   [How to add a tier to a service template](../Topic/How-to-add-a-tier-to-a-service-template.md)

    -   [How to add networking components to a service template](../Topic/How-to-add-networking-components-to-a-service-template.md)

4.  On the **Home** tab, in the **Service Template** group, click **Save and Validate** to save the service template.

    If there are any validation errors, a warning icon will appear on the element of the service template that caused the validation error and a message that describes the issue will appear in the properties pane in the Service Template Designer window.

    After you save the service template, it is added to the Service Templates node in the Library workspace. To open an existing service template in the Service Template Designer, select the service template in the Library workspace, and then on the **Service Template** tab, in the **Actions** group, click **Open Designer**.

    > [!IMPORTANT]
    > If you try to save changes to a service template that is used as the basis for a deployed service, you need to save the service template with a new release value. The name of the service template will remain the same. In the Service Templates node in the Library workspace, you will see separate entries for the two versions of the service template.

After you create the service template and add the necessary tiers and network components, you can configure the properties of the elements of the service template. For more information, see [How to configure the properties of a service template](../Topic/How-to-configure-the-properties-of-a-service-template.md).

## See Also
[How to configure the properties of a service template](../Topic/How-to-configure-the-properties-of-a-service-template.md)
[Creating service templates in VMM](../Topic/Creating-service-templates-in-VMM.md)
[Overview: creating profiles and templates in VMM](../Topic/Overview--creating-profiles-and-templates-in-VMM.md)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

