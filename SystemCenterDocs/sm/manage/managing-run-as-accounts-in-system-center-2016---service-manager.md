---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Managing Run As Accounts in System Center 2016   Service Manager
ms.technology:  service-manager
ms.assetid:  556f240e-d032-406a-ba10-2404fb591d04
---

# Managing Run As Accounts in System Center 2016 - Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

During the setup of Service Manager, you specified credentials for the workflow and service accounts, for Microsoft SQL Server Analysis Services, and for SQL Server Reporting Services (SSRS). If, because of the configurations of password security requirements used in your organization, these passwords expire, you must update the new passwords in Service Manager. In addition, if you decide that the user names must change, you also must change them in Service Manager. This section describes how to make those changes.

It is a best practice never to delete Run As accounts from the Service Manager console. The Service Manager management pack monitors Run As accounts. At regular intervals, the Health service attempts to log on as the Run As accounts. If this fails, Event ID 7000 is invoked that causes an alert. The best way to avoid this issue is never to delete Run As accounts from the Service Manager console. You can reuse existing Run As accounts by changing their name or credentials. If you want to stop using a Run As account, you can change its credentials to Local System and change the name to something easy to remember, such as "Inactive".



