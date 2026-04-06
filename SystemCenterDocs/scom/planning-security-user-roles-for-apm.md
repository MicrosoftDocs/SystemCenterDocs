---
ms.assetid: aa903de4-1f46-407b-a340-8b07abdaeda7
title: User Roles for Application Performance Monitoring
description: This article describes the user roles for the Application Performance Monitoring feature of Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# User Roles for Application Performance Monitoring



## .NET Application Performance Monitoring tasks and user roles  

This table shows the System Center Operations Manager .NET Application Performance Monitoring tasks and the user roles with their permissions.  

Legend:  

- Yes = Can always use the feature  

- No = Cannot use the feature unless the user also belongs to a group that grants access to functionality.  

| -                                     | Administrator | Author | Advanced Operator | Application Monitoring Operator | Operator | Read-Only Operator | Report Operator | Report Security Administrator |
|---------------------------------------|---------------|--------|-------------------|---------------------------------|----------|--------------------|-----------------|-------------------------------|
| Run APM Wizard or change APM settings | Yes           | No     | No                | No                              | No       | No                 | No              | No                            |
| Access Application Diagnostics        | Yes           | No     | No                | Yes                             | No       | No                 | No              | No                            |
| Access Application Advisor            | Yes           | No     | No                | Yes                             | No       | No                 | Yes             | Yes                           |  

> [!NOTE]  
> The Application Monitoring Operator role and Report Operator role are both required to access Application Advisor.  
