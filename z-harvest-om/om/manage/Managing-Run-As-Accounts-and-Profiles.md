---
title: Managing Run As Accounts and Profiles
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2aa0a67f-6ef5-49b8-b607-95461d84fc33
author:mgoedtel
manager:cfreemanwa
---
# Managing Run As Accounts and Profiles
[!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] workflows, such as rules, tasks, monitors, and discoveries, require credentials to run on a targeted agent or computer. By default, workflows use the default action account for the agent or computer. The credentials for the default action account are configured when [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] is installed.  
  
When a workflow requires rights and privileges that the default action account cannot provide, the workflow can be written to use a Run As profile. A Run As profile can have multiple Run As accounts associated with it. The Run As accounts allow you to specify the necessary credentials for specific computers. Multiple workflows can use the same Run As profile. The following image illustrates the relationship between workflows, Run As profiles, and Run As accounts.  
  
![Workflows use Run As profile to use Run As account](../../om/manage/media/RunAsConcept.jpg "RunAsConcept")  
  
In the image, three workflows use the same Run As profile. The Run As profile has three associated Run As accounts. In this example, each workflow that uses the Run As profile will run on Computer A using the credentials for Run As account 1, on Computer B and C using the credentials for Run As account 2, and on Computer D using the credentials for Run As account 3.  
  
Run As profiles are defined in management packs by the management pack author. A Run As profile is used wherever its parent management pack is active. For example, the SQL Server&nbsp;2005 management pack contains the SQL Run As profile, so the SQL Run As profile would be active on all servers running SQL Server&nbsp;2005 that are monitored by the SQL Server&nbsp;2005 management pack. The Run As profile is an association of one or more Run As accounts and the managed objects that the Run As accounts should be applied to.  
  
In some cases, the Run As profile is imported into Operations Manager when the management pack that contains it is imported. In other cases, you may need to create it manually. In all cases, Run As profiles must be manually associated with a Run As account.  
  
A Run As account contains a single set of credentials which are stored in the Operations Manager&nbsp;operational database. Each Run As account has a security classification \(more secure or less secure\) that controls how the credentials are distributed for use. If you elect more secure credential distribution, you must configure the mapping of which computers the credentials are distributed to.  
  
## Managing Run As Accounts and Profiles topics  
  
-   [Distribution and Targeting for Run As Accounts and Profiles](../../om/manage/Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md)  
  
    This topic explains the difference between distribution and targeting, the options for distributing Run As accounts, and the options for selecting targets for Run As profiles.  
  
-   [How to Create a Run As Account](../../om/manage/How-to-Create-a-Run-As-Account.md)  
  
    This topic explains how to create a Run As account and how to modify an existing Run As account.  
  
-   [How to Associate a Run As Account to a Run As Profile](../../om/manage/How-to-Associate-a-Run-As-Account-to-a-Run-As-Profile.md)  
  
    This topic explains how to configure a Run As profile to use a Run As account.  
  
-   [How to Create a New Run As Account for Accessing the Operations Manager Database](../../om/manage/How-to-Create-a-New-Run-As-Account-for-Accessing-the-Operations-Manager-Database.md)  
  
    This topic explains how to create a Run As account that can access the operational database.  
  
-   [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](../../om/manage/How-to-Configure-Run-As-Accounts-and-Profiles-for-UNIX-and-Linux-Access.md)  
  
    This topic explains the Run As accounts you must create to monitor UNIX and Linux computers.  
  
## Other resources for Operations Manager  
  
-   [TechNet Library main page for Operations Manager](http://go.microsoft.com/fwlink/?LinkID=213297)  
  
-   [Operations Guide for System Center 2012 - Operations Manager](../../om/manage/Operations-Guide-for-System-Center-2012---Operations-Manager.md)  
  
-   [Managing Access in Operations Manager](../../om/manage/Managing-Access-in-Operations-Manager.md)  
  
-   [Run As Accounts for Network Monitoring in Operations Manager](../../om/manage/Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md)  
  
