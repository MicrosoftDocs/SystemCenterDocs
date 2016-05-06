---
title: About Creating Configuration Items
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da53ac14-7b24-40ab-a421-e4c42a7e933a
robots: noindex,nofollow
---
# About Creating Configuration Items
Configuration items are a way to store information about services, computers, software, software updates, users, and other undefined imported objects in the [!INCLUDE[smshort](../Token/smshort_md.md)] database in [!INCLUDE[smlong12](../Token/smlong12_md.md)]. You can then select configuration items when you submit forms, such as an incident form, a change request form, or a work item form.

A service is a special kind of configuration item that includes both technical and business data. It supports troubleshooting and impact analysis by showing critical dependencies, settings, and areas of responsibility to other configuration items. The key benefit of using services is that you can easily see when incidents affect configuration items because services are viewed as a map, or hierarchy, of items. A service also identifies service owners, key customers, and users. Because a service maps the relationships between configuration items and work items, you should use services to help you manage work items.

You can use connectors to import a large number of configuration items from Active Directory Domain Services \(AD DS\), [!INCLUDE[sccmlongname](../Token/sccmlongname_md.md)] Service Pack 1 \(SP1\), and Operations Manager 2007, or you can manually create single configuration items. You can also use the Operations Manager CI connector to import distributed applications in Operations Manager as a service. For more information about importing configuration items, see [Using Connectors to Import Data into System Center 2012 - Service Manager](../Topic/Using-Connectors-to-Import-Data-into-System-Center-2012---Service-Manager.md).

