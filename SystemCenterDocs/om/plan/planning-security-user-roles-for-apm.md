---
title: User Roles for Application Performance Monitoring
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# User Roles for Application Performance Monitoring

>Applies To: System Center 2016 - Operations Manager
  
## .NET Application Performance Monitoring tasks and user roles  

This table shows the System Center 2016 - Operations Manager .NET Application Performance Monitoring tasks and the user roles with their permissions.  
  
Legend:  
  
-   Yes = Can always use the feature  
  
-   No = Cannot use the feature unless the user also belongs to a group that grants access to functionality.  


|-|Administrator|Author|Advanced Operator|Application Monitoring Operator|Operator|Read-Only Operator|Report Operator|Report Security Administrator|
|-|-------------|------|-----------------|-------------------------------|--------|--------------------|---------------|-----------------------------|
|Run APM Wizard or change APM settings|Yes|No|No|No|No|No|No|No|
|Access Application Diagnostics|Yes|No|No|Yes|No|No|No|No|
|Access Application Advisor|Yes|No|No|Yes|No|No|Yes|Yes|


| -                                     | Administrator | Author | Advanced Operator | Application Monitoring Operator | Operator | Read-Only Operator | Report Operator | Report Security Administrator |
|---------------------------------------|---------------|--------|-------------------|---------------------------------|----------|--------------------|-----------------|-------------------------------|
| Run APM Wizard or change APM settings | Yes           | No     | No                | No                              | No       | No                 | No              | No                            |
| Access Application Diagnostics        | Yes           | No     | No                | Yes                             | No       | No                 | No              | No                            |
| Access Application Advisor            | Yes           | No     | No                | Yes                             | No       | No                 | Yes             | Yes                           |


> [!NOTE]  
> The Application Monitoring Operator role and Report Operator role are both required to access Application Advisor.  
  
