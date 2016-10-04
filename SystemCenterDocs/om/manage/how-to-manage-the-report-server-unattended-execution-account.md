---
ms.assetid: e0fe4a01-8964-402b-95e9-76bc5940606a
title: How to Manage the Report Server Unattended Execution Account in Operations Manager
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Manage the Report Server Unattended Execution Account in Operations Manager

>Applies To: System Center 2016 - Operations Manager

The Operations Manager Report Server unattended execution account is used to query data from the Reporting data warehouse. Be sure to use an account that has minimum permissions (read-only access with network connection permissions is sufficient). This account is not managed from within the Operations Manager user interface. Use this procedure to change the user name or password for this account.  
  
### To manage the Report Server unattended execution account  
  
1.  From the Windows start screen, type **Reporting** and select **Reporting Services Configuration Manager** from the search results.
  
2.  The Reporting Services Configuration Connection dialog box appears so that you can select the report server instance you want to configure. Select **Connect**.

3.  In **Server Name**, specify the name of the computer on which the report server instance is installed. The name of the local computer appears by default, but you can type the name of a remote SQL Server instance if you want to connect to a report server that is installed on a remote computer.  

4. In **Report Server Instance**, select the SQL Server Reporting Services instance that you want to configure. 

4.  On the **Execution Account** page, type in a new user name or password as required.  
  
5.  Click **Apply**, and then click **Exit**.  
  
## Next steps

- To understand how to create a Run As account, how to modify an existing Run As account, and how to configure a Run As profile to use a Run As account see, [How to Create a Run As Account and Associate with a Run As Profile](How-to-Create-a-Run-As-Account-and-associate-to-a-profile.md).

- If you need to create new credentials for the management server action account, see [How to Create a New Action Account in Operations Manager](How-to-Create-a-New-Action-Account-in-Operations-Manager.md).

- Review [Implementing User Roles](implementing-user-roles.md) to understand the profiles defined in Operations Manager to manage authorization and security, and configure user roles to perform administration and access to operational data in the management group. 

  
