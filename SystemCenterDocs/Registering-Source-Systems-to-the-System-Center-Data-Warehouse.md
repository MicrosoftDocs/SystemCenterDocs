---
title: Registering Source Systems to the System Center Data Warehouse
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f48a1c7-dc88-447d-8bde-8af76783e2d3
---
# Registering Source Systems to the System Center Data Warehouse
The data warehouse in Service Manager retrieves data from one or more data sources. These data sources are the transactional processing systems that produce and govern data that you will eventually want to measure and analyze. For example, incidents and change requests are created and managed in [!INCLUDE[smshort](Token/smshort_md.md)], software updates and power policies are managed in Configuration Manager, and other systems produce and govern other data sets.

Registering the data warehouse creates a relationship between the data warehouse server and the source system so that information can flow between them. In [!INCLUDE[smshort](Token/smshort_md.md)], you can register to [!INCLUDE[smshort](Token/smshort_md.md)], [!INCLUDE[om12short](Token/om12short_md.md)], and Configuration Manager directly. You can also use the updated software development kit \(SDK\) layer on top of the data warehouse, which enables you to push data into the data warehouse directly from other sources. For example, you might want to push data from your Human Resources computer system in the data warehouse.


