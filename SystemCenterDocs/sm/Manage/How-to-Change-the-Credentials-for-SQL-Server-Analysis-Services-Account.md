---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Change the Credentials for SQL Server Analysis Services Account
ms.technology:  service-manager
ms.assetid:  f8a1be01-4c9e-4e47-bd5e-d9614ec045bc
---

# How to Change the Credentials for SQL Server Analysis Services Account

>Applies To: System Center 2016 Technical Preview - Service Manager

If the account that is used for the SQL Server Analysis Services account changes in Service Manager, you must also change the credentials for the account. Use the following procedure to change the credentials for the SQL Server Analysis Services account.

### To change the credentials for the SQL Server Analysis Services account

1.  On the computer hosting SQL Server Analysis Server (SSAS), open **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, complete these steps:

    1.  In the **Server Type** list, click **Analysis Services**.

    2.  In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.

3.  In **Microsoft SQL Server Management Studios**, in the **Object Explorer** pane, expand **Databases**, expand **DWASDataBase**, expand **Data Sources**, and then double-click **DWDataMart**.

4.  In **Data Source Properties - DWDataMart**, under **Security Settings**, click the ellipsis button (...) next to **ImpersonateAccount**.

5.  In the **Impersonation Information** window, select **Use a specific Windows user name and password**, type the credentials for the new account, and then click **OK**.

6.  Click **OK** to close **Data Source Properties - DWDataMart**, and then close Microsoft SQL Server Management Studio.
