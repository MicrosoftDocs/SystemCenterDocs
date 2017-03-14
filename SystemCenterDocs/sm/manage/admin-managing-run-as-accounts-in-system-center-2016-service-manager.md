---
title: Manage Run As accounts
description: Describes how to manage Run As accounts in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 556f240e-d032-406a-ba10-2404fb591d04
---

# Manage Run As accounts in Service Manager

>Applies To: System Center 2016 - Service Manager

During the setup of Service Manager, you specified credentials for the workflow and service accounts, for Microsoft SQL Server Analysis Services, and for SQL Server Reporting Services (SSRS). If, because of the configurations of password security requirements used in your organization, these passwords expire, you must update the new passwords in Service Manager. In addition, if you decide that the user names must change, you also must change them in Service Manager. This section describes how to make those changes.

It is a best practice never to delete Run As accounts from the Service Manager console. The Service Manager management pack monitors Run As accounts. At regular intervals, the Health service attempts to log on as the Run As accounts. If this fails, Event ID 7000 is invoked that causes an alert. The best way to avoid this issue is never to delete Run As accounts from the Service Manager console. You can reuse existing Run As accounts by changing their name or credentials. If you want to stop using a Run As account, you can change its credentials to Local System and change the name to something easy to remember, such as *Inactive*.
