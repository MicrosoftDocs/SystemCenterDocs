---
ms.assetid: e0fe4a01-8964-402b-95e9-76bc5940606a
title: Manage the Report Server Unattended Execution Account in Operations Manager
description: This topic describes how to configure the unattended execution account for the Operations Manager Reporting server.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Manage the Report Server Unattended Execution Account in Operations Manager



The Operations Manager Report Server unattended execution account is used to query data from the Reporting data warehouse. Ensure to use an account that has minimum permissions (read-only access with network connection permissions is sufficient). This account isn't managed from within the Operations Manager user interface. Use this procedure to change the user name or password for this account.  

### Manage the Report Server unattended execution account

To manage the Report Server unattended execution account, follow these steps:

1. From the Windows start screen, enter **Reporting** and select **Reporting Services Configuration Manager** from the search results.

2. The Reporting Services Configuration Connection dialog appears so that you can select the report server instance you want to configure. Select **Connect**.

3. In **Server Name**, specify the name of the computer on which the report server instance is installed. The name of the local computer appears by default, but you can enter the name of a remote SQL Server instance if you want to connect to a report server that is installed on a remote computer.  

4. In **Report Server Instance**, select the SQL Server Reporting Services instance that you want to configure.

5. On the **Execution Account** page, enter a new user name or password as required.  

6. Select **Apply**, and then select **Exit**.  

## Next steps

- To understand how to create a Run As account, how to modify an existing Run As account, and how to configure a Run As profile to use a Run As account, see [How to Create a Run As Account and Associate with a Run As Profile](~/scom/manage-security-create-runas-link-profile.md).

- If you need to create new credentials for the management server action account, see [Create a New Action Account in Operations Manager](~/scom/manage-security-create-runas-actionaccount.md).

- To understand the profiles defined in Operations Manager to manage authorization and security and configure user roles to perform administration and access to operational data in the management group, see [Implement User Roles](manage-security-overview.md).
