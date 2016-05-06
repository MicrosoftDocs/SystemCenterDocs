---
title: User Roles for Application Performance Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21f4a15d-de90-4bd0-aa38-682d8038ce50
---
# User Roles for Application Performance Monitoring

## .NET Application Performance Monitoring Tasks and User Roles
This table shows the [!INCLUDE[om12long](./Token/om12long_md.md)] .NET Application Performance Monitoring tasks and the user roles with their permissions.

Legend:

-   Yes \= Can always use the feature

-   No \= Cannot use the feature unless the user also belongs to a group that grants access to functionality.

||Administrator|Author|Advanced Operator|Application Monitoring Operator|Operator|Read\-Only Operator|Report Operator|Report Security Administrator|
|-|-----------------|----------|---------------------|-----------------------------------|------------|-----------------------|-------------------|---------------------------------|
|Run APM Wizard or change APM settings|Yes|No|No|No|No|No|No|No|
|Access Application Diagnostics|Yes|No|No|Yes|No|No|No|No|
|Access Application Advisor|Yes|No|No|Yes\*|No|No|Yes\*|Yes|

> [!NOTE]
> \* The Application Monitoring Operator role and Report Operator role are both required to access Application Advisor.


