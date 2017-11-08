---
ms.assetid: aa903de4-1f46-407b-a340-8b07abdaeda7
title: User Roles for Application Performance Monitoring
description: This article describes the user roles for the Application Performance Monitoring feature of Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# User Roles for Application Performance Monitoring
  
## .NET Application Performance Monitoring tasks and user roles  

This table shows the System Center 2016 - Operations Manager .NET Application Performance Monitoring tasks and the user roles with their permissions.  
  
Legend:  
  
-   Yes = Can always use the feature  
  
-   No = Cannot use the feature unless the user also belongs to a group that grants access to functionality.  


| -                                     | Administrator | Author | Advanced Operator | Application Monitoring Operator | Operator | Read-Only Operator | Report Operator | Report Security Administrator |
|---------------------------------------|---------------|--------|-------------------|---------------------------------|----------|--------------------|-----------------|-------------------------------|
| Run APM Wizard or change APM settings | Yes           | No     | No                | No                              | No       | No                 | No              | No                            |
| Access Application Diagnostics        | Yes           | No     | No                | Yes                             | No       | No                 | No              | No                            |
| Access Application Advisor            | Yes           | No     | No                | Yes                             | No       | No                 | Yes             | Yes                           |  


> [!NOTE]  
> The Application Monitoring Operator role and Report Operator role are both required to access Application Advisor.  
  
