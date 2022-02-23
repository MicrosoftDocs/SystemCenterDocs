---
ms.assetid: 1a7d9146-5782-4cad-8bb5-c69511b578d1
title: Azure SQL Database Run As accounts in Management Pack for Azure SQL Database
description: This article explains how to configure Azure SQL Database run as accounts in Management Pack for Azure SQL Database
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Azure SQL Database Run As Accounts

To monitor Azure SQL Database servers, create one or more **Simple** or **Basic** Run As accounts. For more information about Run As accounts, see [Managing Run As accounts and profiles](manage-security-maintain-runas-profiles.md).

To create Run As accounts, perform the following steps:

1. In the System Center Operations Manager console, right-click the **Administration | Run As Configuration | Accounts** node, and select **Create Run As Account**.

    ![Create Run As Accounts](./media/azure-sql-management-pack/creating-run-as-accounts.png)

2. At the **Introduction** step, click **Next**.

3. At the **General Properties** step, from the **Run As account type** drop-down list, select **Simple Authentication**, enter a display name and optional description, and click **Next**.

    ![General properties](./media/azure-sql-management-pack/configuring-general-properties-run-as.png)

4. At the **Credentials** step, specify credentials that you want to use to connect to Azure SQL Database and click **Next**. For more information, see [Low-Privilege Configuration](azure-sql-management-pack-low-privilege-configuration.md).

    ![Set credentials](./media/azure-sql-management-pack/configuring-credentials.png)

5. At the **Distribution Security** step, select the **More secure** option and click **Create**.

    You can use the **Less secure** option and skip steps 7 – 8 if your environment is secure.

6. Click **Close** to close the window.

7. Right-click the newly created account and select **Properties**.

    ![Account properties](./media/azure-sql-management-pack/account-properties.png)

8. Open the **Distribution** tab and add a System Center Operations Manager agent that you want to use as a watcher node to monitor Azure SQL Database.

    ![Add agent](./media/azure-sql-management-pack/adding-agent.png)