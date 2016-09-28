---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Change the Credentials for SQL Server Reporting Services Account
ms.technology:  service-manager
ms.assetid:  c06e8cf9-b739-483d-bcf1-abab60f3ec23
---

# How to Change the Credentials for SQL Server Reporting Services Account

>Applies To: System Center 2016 - Service Manager

If the account that is used for the SQL Server Reporting Services account changes in Service Manager, you must change the credentials for the account. Use the following procedure to change the credentials for the SQL Server Reporting Services account.

### To change the credentials for the SQL Server Reporting Services account

1.  On the computer hosting SQL Server Reporting Server (SSRS), start a browser, and connect to `http://<server name>/reports`.

2.  On the **SQL Server Reporting Services Home** page, double-click **Service Manager**, and then double-click **DWStagingAndConfig**.

3.  In the **Connect using** area, click **Credentials stored securely in the report server**, type the current credentials in the **User name** and **Password** boxes, and then click **Apply**.

4.  In the browser tool bar, click the **Back** button to return to the **Service Manager** page.

5.  Repeat steps 2 and 3 for the remaining Service Manager data sources.



