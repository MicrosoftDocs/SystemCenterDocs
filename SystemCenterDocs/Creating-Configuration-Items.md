---
title: Creating Configuration Items
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5eaf4196-7623-480f-b132-2431ab520681
---
# Creating Configuration Items
This section provides an overview of configuration items, describes how to manually create computer configuration items, how to create a service, and how to create a view for imported configuration items in Service Manager.

Configuration items are a way to store information about services, computers, software, software updates, users, and other undefined imported objects in the [!INCLUDE[smshort](Token/smshort_md.md)] database in Service Manager. You can then select configuration items when you submit forms, such as an incident form, a change request form, or a work item form.

A service is a special kind of configuration item that includes both technical and business data. It supports troubleshooting and impact analysis by showing critical dependencies, settings, and areas of responsibility to other configuration items. The key benefit of using services is that you can easily see when incidents affect configuration items because services are viewed as a map, or hierarchy, of items. A service also identifies service owners, key customers, and users. Because a service maps the relationships between configuration items and work items, you should use services to help you manage work items.

You can use connectors to import a large number of configuration items from Active Directory Domain Services \(AD DS\), Configuration Manager, and Operations Manager, or you can manually create single configuration items. You can also use the Operations Manager CI connector to import distributed applications in Operations Manager as a service. For more information about importing configuration items, see [Using Connectors to Import Data into System Center 2012 - Service Manager](Using-Connectors-to-Import-Data-into-System-Center-2016---Service-Manager.md).


