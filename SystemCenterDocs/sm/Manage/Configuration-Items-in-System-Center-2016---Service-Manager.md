---
title: Configuration Items in System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e6ab64c-c752-4cee-9057-e4b4413e571d
---
# Configuration Items in System Center 2016 - Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

Configuration items are a way to store information about services, computers, software, software updates, users and other undefined imported objects in the Service Manager database in System Center 2016 Technical Preview - Service Manager. You can then select configuration items when you submit forms, such as an incident form, a change request form, or a work item form.

A service is a special kind of configuration item that includes both technical and business data. It supports troubleshooting and impact analysis by showing critical dependencies, settings, and areas of responsibility to other configuration items. The key benefit of using services is that you can easily see when incidents affect configuration items because services are viewed as a map, or hierarchy, of items. A service also identifies service owners, key customers, and users. Because a service maps the relationships between configuration items and work items, you should use services to help manage work items.

You can use connectors to import a large number of configuration items from Active Directory Domain Services (AD DS), Configuration Manager, and Operations Manager, or you can manually create single CIs. You can also use the Operations Manager CI connector to import distributed applications in Operations Manager as a service. 
> [!NOTE]
> When you open a view to display a large number of items—typically, more than 5,000—the view can take a few minutes to display complete results.



