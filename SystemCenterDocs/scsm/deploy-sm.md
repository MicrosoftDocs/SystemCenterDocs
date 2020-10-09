---
title: Deploy System Center - Service Manager
description: This guide helps you deploy System Center - Service Manager in one of several different scenarios.
manager: carmonm
ms.prod: system-center
author: JYOTHIRMAISURI
ms.author: v-jysur
ms.date: 10/09/2020
ms.technology: service-manager
ms.topic: article
---

# Deploy System Center - Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

The sections in this article help you deploy System Center - Service Manager in one of several different scenarios. The scenarios range from a simple, one\-computer scenario to a four\-computer scenario that is designed to support production\-type environments. In addition, this guide shows you how to register a Service Manager management group with the Service Manager data warehouse so that you can generate reports. You have the option of deploying the Self-Service Portal so you can provide access to Service Manager through a web browser. To improve performance and provide for redundancy, you can deploy additional secondary Service Manager management servers.  

> [!NOTE]  
>  It is assumed that you are installing Service Manager on a computer where no previous version of Service Manager is installed.

The sections in this article also describe how to find and read the Setup log if you encounter issues when you deploy Service Manager. And, finally, information about backing up Service Manager management server encryption keys is included. After you run Setup, the Encryption Key Backup and Restore Wizard start automatically.  

The following sections describe considerations you should read before you deploy Service Manager.

## Manage default language for SQL login accounts
We recommend English as the default language for the SQL users login accounts.

As date format is based on the language, if the language of SQL user login accounts is not English, then, few data Warehouse jobs, specially the jobs that use SQL *SET_DateFormat* function, fail. These jobs do  not push the data into the data warehouse from Service Manager or might send incorrect data into the data warehouse, leading to data corruption in the data warehouse.

You can set the default language for a new SQL login account or change the default language for an existing account. See the following sections for the steps to use.

**Use these steps**:

1. Open SQL Management Studio with elevated privileges and connect to SQL server where you want to create Service Manager or Data Warehouse databases.
2. Go to **Security** folder
3. Right-click **Logins** folder and then select **New Login** as shown below.

    ![New login account](./media/deploy-sm/new-login.png)

4. On the properties page, from the  **Default language** drop-down list, select **English**

    ![Default language for new login account](./media/deploy-sm/properties.png)


5. To change the default language for an existing login account, from the **Logins folder**, double-click the account, and then select **Properties** to edit  the **Default language** as English.

    ![change current language](./media/deploy-sm/change-existing-language.png)


## Avoid using Turkish language collations with Service Manager

This section applies only if you are considering deploying a Service Manager database or data warehouse database to a SQL&nbsp;Server that has been configured to use a Turkish language collation.  

 The installation of a Service Manager database is not supported on a computer running SQL&nbsp;Server that uses a Turkish language collation. This is true for both the Service Manager and data warehouse databases. If you specify a computer running SQL&nbsp;Server that contains a Turkish language collation during the deployment of a Service Manager database, the following warning message appears.

![Turkish Collation Warning](./media/deploy-sm/deploy-turkishcollationwarning.png)

 If you encounter this warning message during the deployment of any of the Service Manager databases, click **OK**. On the **Database Configuration** page, in the **Database server** box, type the name of a computer that is hosting an installation of SQL&nbsp;Server that is configured with a non\-Turkish collation, and then press the TAB key. When **Default** appears in the **SQL Server instance** box, click **Next**.  

## Use the Prerequisite checker before you deploy Service Manager

During installation, System Center - Service Manager Setup performs prerequisite checks for software and hardware requirements and returns one of the three following states:  

-   **Success**: Setup finds that all software and hardware requirements are met, and installation proceeds.  

-   **Warning**: Setup finds that all software requirements are met, but the computer does not meet minimum hardware requirements. Or, the requirements for optional software are missing. Installation proceeds.  

-   **Failure**: At least one software or hardware requirement is not met, and installation cannot proceed. An **Installation cannot continue** message appears.  

> [!NOTE]  
>  On the **Installation cannot continue** screen, there is no option to restart the prerequisite checker. You must click **Cancel** to restart the installation process. Make sure that the computer meets all hardware and software requirements before you run Setup again.

## Next steps

- Review [Deployment scenarios for Service Manager](deploy-scenarios.md) to learn about how to deploy Service Manager in one-server, two-server, and four-server topologies.
