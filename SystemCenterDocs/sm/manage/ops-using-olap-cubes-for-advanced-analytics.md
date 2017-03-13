---
title: Overview of OLAP cubes for advanced analytics
description: Provides an overview of Service Manger OLAP cubes for advanced analytics.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36e556eb-3db1-4900-be1a-a44dc0073d3e
---

# Overview of Service Manger OLAP cubes for advanced analytics

>Applies To: System Center 2016 - Service Manager

In Service Manager, data that is present in the data warehouse can be consolidated from various sources. It is presented through Service Manager by using predefined and customized Microsoft Online Analytical Processing \(OLAP\) data cubes. In short, advanced analytics in Service Manager consist of publishing, viewing, and manipulating cube data, usually in either Microsoft Excel or Microsoft SharePoint. Excel is primarily used by itself to view and manipulate data. SharePoint is used primarily as a means of publishing and sharing cube data.  

 Service Manager includes a System Center-wide data warehouse. Therefore, data from Operations Manager, Configuration Manager, and Service Manager can be consolidated into the data warehouse, where you can easily use multiple data views to get any information that you might want. This is also an interface where you can put data into the same data warehouse from your own custom sources, such as SAP applications or a third\-party human resources application. This consolidation creates a common data model and enables enriched analyses to help you build a data warehouse across your Information Technology \(IT\) organization that can serve all your business intelligence and reporting needs.  

 When your data is in a common model, you can manipulate information and have common definitions and a common taxonomy for your whole enterprise. You can do this by deploying OLAP data cubes and accessing the information from the cubes, using standard tools such as Excel and SharePoint. This makes it possible for your users to employ skills that they already know. You control the definition of your business logic in a centralized manner. For example, you can define key performance indicators, such as the incident time\-to\-resolution thresholds, and which values for the thresholds are green, yellow, or red. You can control these choices in a centralized manner and empower your users to easily use the data, yet have the common definition appear in their Excel reports or their SharePoint dashboards.  
