---
title: Configuration Items in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8981397f-fc36-43ee-ae14-db1833ce48ed
---
# Configuration Items in System Center 2012 - Service Manager
Configuration items are a way to store information about services, computers, software, software updates, users and other undefined imported objects in the Service Manager database in [!INCLUDE[smlong12](../Token/smlong12_md.md)]. You can then select configuration items when you submit forms, such as an incident form, a change request form, or a work item form.

A service is a special kind of configuration item that includes both technical and business data. It supports troubleshooting and impact analysis by showing critical dependencies, settings, and areas of responsibility to other configuration items. The key benefit of using services is that you can easily see when incidents affect configuration items because services are viewed as a map, or hierarchy, of items. A service also identifies service owners, key customers, and users. Because a service maps the relationships between configuration items and work items, you should use services to help manage work items.

You can use connectors to import a large number of configuration items from Active Directory Domain Services \(AD DS\), [!INCLUDE[sccmlongname](../Token/sccmlongname_md.md)] Service Pack 1 \(SP1\), and Operations Manager 2007, or you can manually create single CIs. You can also use the Operations Manager CI connector to import distributed applications in [!INCLUDE[om12short](../Token/om12short_md.md)] as a service. For more information about importing configuration items, see [About Importing Data from System Center Configuration Manager](../Topic/About-Importing-Data-from-System-Center-Configuration-Manager.md) and [About Importing Data from Active Directory Domain Services](../Topic/About-Importing-Data-from-Active-Directory-Domain-Services.md).

> [!NOTE]
> When you open a view to display a large number of items—typically, more than 5,000—the view can take a few minutes to display complete results.

## Configuration Items Topics

-   [Creating Configuration Items](../Topic/Creating-Configuration-Items.md)

    Describes how to manually create configuration items, how to create a server, and how to create a view for imported configuration items.

-   [Deleting Configuration Items](../Topic/Deleting-Configuration-Items.md)

    Describes the two\-step process required to delete configuration items.

-   [Managing Configuration Items](../Topic/Managing-Configuration-Items.md)

    Describes how to add, browse, and delete related configuration items and how to manually add a user.

## Other Resources for This Component

-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)

-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)

-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)

-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)

