---
title: Manage and use the analysis libraries
description: Explains how to manage and use the analysis libraries in the Service Manager console.
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
ms.assetid: 5f3e94e5-6706-4ef4-a511-a21c5d6b98f8
---

# Manage and use the analysis libraries in the Service Manager console

You can use the following procedure to manage the analysis libraries in the Service Manager console in Service Manager. The analysis libraries are file storage areas, such as network shares, Universal Naming Convention \(UNC\) paths, and Microsoft SharePoint. The libraries are used to house Microsoft Excel data files, which are generated from Microsoft Online Analytical Processing \(OLAP\) data cubes. When they are saved to an analysis library, you can easily access Excel files and the cube data they connect to without having to open the Service Manager console. Instead, you can open the storage location directly or from the Reporting workspace.  

 You might want to create many analysis library folders for different departments in your organization.  

 In order to add a new analysis library folder, the underlying shared folder or other sharing location must already exist and you must have permission to write to it.  

## Manage an analysis library folder  

1.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Analysis Libraries**.  
2.  In the **Tasks** pane, click **Add Library Folder**.  
3.  In the **Add Library Folder** dialog box under **Name**, type a name for the new analysis library folder. For example, type **Incident Management Analysis Library**.  
4.  Under **Description**, type a description that identifies the type of information that the folder will contain. For example, type **This folder contains saved incident management\-related workbooks**.  
5.  Under **UNC Path**, type the path that represents the library folder. An example might resemble **\\\\computer1\\IncidentManagmentReports\\**. You can also click **Browse** to search for a location.  

## Use the analysis library in the Reporting workspace


You can use the following procedure in Service Manager to view Microsoft Excel workbooks that connect to Microsoft Online Analytical Processing \(OLAP\) data cubes by using the **Analysis Library** node in the Reporting workspace. Workbooks are saved to the Analysis Library by Service Manager so that report users can easily access the workbooks.  

### To use the analysis library  

1.  In the Service Manager console, click **Reporting**, expand the **Analysis Library** node, and then navigate to the folder that contains an Excel workbook that you want to open.  
2.  Select the Excel workbook that you want to open, and then in the **Tasks** list, click **Open Excel File**.  
3.  In the Excel workbook, you can refresh the data from the data warehouse. For example, click the **Data** tab and then click **Refresh All** to update the workbook.  

## Next steps

- [Create and deploy dashboards](deploy-dashboards.md) to manage SharePoint dashboards and their elements to measure, monitor, and manage business performance with live data from the Service Manager data warehouse.
