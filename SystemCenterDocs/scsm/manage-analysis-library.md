---
title: Manage and use the analysis libraries
description: Explains how to manage and use the analysis libraries in the Service Manager console.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 5f3e94e5-6706-4ef4-a511-a21c5d6b98f8
---

# Manage and use the analysis libraries in the Service Manager console



You can use the following procedure to manage the analysis libraries in the Service Manager console in Service Manager. The analysis libraries are file storage areas, such as network shares, Universal Naming Convention \(UNC\) paths, and Microsoft SharePoint. The libraries are used to house Microsoft Excel data files, which are generated from Microsoft Online Analytical Processing \(OLAP\) data cubes. When they're saved to an analysis library, you can easily access Excel files and the cube data they connect to without having to open the Service Manager console. Instead, you can open the storage location directly or from the Reporting workspace.  

 You might want to create many analysis library folders for different departments in your organization.  

 In order to add a new analysis library folder, the underlying shared folder or other sharing location must already exist and you must have permission to write to it.  

## Manage an analysis library folder  

1. In the Service Manager console, select **Data Warehouse**, expand the **Data Warehouse** node, and select **Analysis Libraries**.  
2. In the **Tasks** pane, select **Add Library Folder**.  
3. In the **Add Library Folder** dialog under **Name**, enter a name for the new analysis library folder. For example, enter **Incident Management Analysis Library**.  
4. Under **Description**, enter a description that identifies the type of information that the folder will contain. For example, enter **This folder contains saved incident management\-related workbooks**.  
5. Under **UNC Path**, enter the path that represents the library folder. An example might resemble **\\\\computer1\\IncidentManagmentReports\\**. You can also select **Browse** to search for a location.  

## Use the analysis library in the Reporting workspace

You can use the following procedure in Service Manager to view Microsoft Excel workbooks that connect to Microsoft Online Analytical Processing \(OLAP\) data cubes by using the **Analysis Library** node in the Reporting workspace. Workbooks are saved to the Analysis Library by Service Manager so that report users can easily access the workbooks.  

### Use the analysis library  

1. In the Service Manager console, select **Reporting**, expand the **Analysis Library** node, and then navigate to the folder that contains an Excel workbook that you want to open.  
2. Select the Excel workbook that you want to open, and then in the **Tasks** list, select **Open Excel File**.  
3. In the Excel workbook, you can refresh the data from the data warehouse. For example, select the **Data** tab and select **Refresh All** to update the workbook.  

## Next steps

- To manage SharePoint dashboards and their elements to measure, monitor, and manage business performance with live data from the Service Manager data warehouse, see [Create and deploy dashboards](deploy-dashboards.md).
