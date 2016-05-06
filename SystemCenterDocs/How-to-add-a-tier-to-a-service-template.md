---
title: How to add a tier to a service template
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46a482f6-f2c5-4d2b-96e4-0550ec00e58c
---
# How to add a tier to a service template
In [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], a service is a set of virtual machines that are configured and deployed together and are managed as a single entity—for example, a deployment of a multi\-tier line\-of\-business application. The service template \(which you use to create a service\) can contain multiple tiers. You can add a tier to a service template in the Service Template Designer by doing either of the following:

-   By dragging a virtual machine template on to the canvas area

-   By using the Create Machine Tier Template wizard

The simplest way to add a tier to a service template is to drag a virtual machine template on to the canvas area. In the Service Template Designer, a list of available virtual machine templates appears in the left pane. Select the virtual machine template that you want to use to create a tier, and then drag the virtual machine template on to the canvas. A tier is created using the properties of the virtual machine template that you selected.

If you created a service template with a pattern that created default tiers for you, you can drag the virtual machine template on to one of those default tiers. The tier will be configured with the properties of that virtual machine template.

> [!IMPORTANT]
> No link or relationship is created between the virtual machine template and the tier that you create. Any subsequent changes that you make to the virtual machine template in [!INCLUDE[vmm12short](Token/vmm12short_md.md)] are not also made to the tier in the service template. And any configuration settings that you make to the tier are not also made to the virtual machine template.

For more information about creating a virtual machine template, see [How to create a virtual machine template](How-to-create-a-virtual-machine-template.md).

## Creating a tier by using a wizard
You can also use the Create Machine Tier Template wizard to add a tier to a service template. The wizard allows you to create a tier based on one of the following:

-   A copy of an existing virtual machine template

-   A customized copy of an existing virtual machine template

-   A virtual hard disk stored in the [!INCLUDE[vmm12short](Token/vmm12short_md.md)] library

#### To add a tier by using the Create Machine Tier Template wizard

1.  In the Service Template Designer, on the **Home** tab, in the **Service Template Components** group, click **Add Machine Tier**.

2.  On the **Select Source** page of the Create Machine Tier Template wizard, choose the source for your tier.

    If you are using a copy of an existing virtual machine template as the basis for your new tier, do the following:

    1.  Click **Browse**, select the virtual machine template you want to use, click **OK**, and then click **Next**.

    2.  On the **Additional Properties** page, configure the properties appropriate for this tier, and then click **Next**. For more information about configuring the properties of a tier, see [How to configure the properties of a service template](How-to-configure-the-properties-of-a-service-template.md).

    3.  On the **Summary** page, review your settings, and then click **Create**. A new tier based on that virtual machine template is added to the canvas of the Service Template Designer.

    If you are using a customized copy of an existing virtual machine template or you are using a virtual hard disk stored in the VMM library as the basis for your new tier, do the following:

    1.  Click **Browse**, select the virtual machine template you want to use, click **OK**, and then click **Next**.

    2.  On the **Additional Properties** page, configure the properties appropriate for this tier, and then click **Next**. For more information about configuring the properties of a tier, see [How to configure the properties of a service template](How-to-configure-the-properties-of-a-service-template.md).

    3.  On the **Configure Hardware** page, configure the hardware properties appropriate for this tier, and then click **Next**. For more information about configuring hardware properties, see [How to create a hardware profile](How-to-create-a-hardware-profile.md).

    4.  On the **Configure Operating System** page, configure the operating system properties appropriate for this tier, and then click **Next**. For more information about configuring operating system properties, see [How to create a guest operating system profile](How-to-create-a-guest-operating-system-profile.md).

    5.  On the **Configure Applications** page, if necessary, configure the application that you want to install for this tier, and then click **Next**. For more information about configuring application installations, see [How to create an application profile in a service deployment](How-to-create-an-application-profile-in-a-service-deployment.md).

    6.  On the **Configure SQL Server** page, if necessary, configure the installation of an instance of SQL Server for this tier, and then click **Next**. For more information about installing an instance of SQL Server, see [How to create a SQL Server profile in a service deployment](How-to-create-a-SQL-Server-profile-in-a-service-deployment.md).

    7.  On the **Summary** page, review your settings, and then click **Create**. A new tier is added to the canvas of the Service Template Designer.

## See Also
[Test Lab Guide for Creating a Service in VMM](http://www.microsoft.com/download/details.aspx?id=38837)
[Creating service templates in VMM](Creating-service-templates-in-VMM.md)
[Managing services with VMM](Managing-services-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


