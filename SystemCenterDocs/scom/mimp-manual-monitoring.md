---
ms.assetid: 29b787f9-5c1f-4d08-a9a0-9c0a9b9075e1
title: Manual Monitoring Template
description: This article explains how to configure manual monitoring template in Management Pack for Azure SQL Managed Instance
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Manual Monitoring Template

This template allows you to add the selected instances to the monitoring list by specifying connection strings manually.

## Configuring Manual Monitoring Template

To configure monitoring using the manual monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Manual**, and select **Add Monitoring Wizard…**.

    ![Run Add Monitoring Wizard](./media/mimp/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Manual**, and click **Next**.

    ![Select monitoring type](./media/mimp/selecting-monitoring-type-manual.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** drop-down list, select a management pack that you want to use to store the template.

    ![Select destination management pack](./media/mimp/destination-management-pack-manual.png)

    You can also create a new management pack by clicking **New**.

    ![Create new management pack](./media/mimp/new-management-pack.png)

4. At the **Service Details** step, click **Add Instances**.

    ![Configure service details](./media/mimp/service-details.png)

5. In the **Add Instances** window, select a Run As Account with appropriate SQL credentials, and specify data sources and (or) connection strings. Follow the instructions provided in the wizard to avoid errors.

    ![Add instances](./media/mimp/add-instance-credentials.png)

    Use the standard security connection string format to specify connection settings:

    ```
    Server=\<ServerAddress>;Database=\<DatabaseName>;
    ```
    
    You can get a connection string for a managed instance using the Azure portal.

    To create a Run As account from the connection string, use the following format:  

    ```
    Server=\<ServerAddress>;Database=\<DatabaseName>;User Id=\<UserName>;Password=\<Password>;
    ```
    
    You can also create a new Run As account by clicking **New** and specifying an account name and connection credentials to access the managed instance.

    ![Configure Run As account](./media/mimp/new-run-as-account-manual.png)

    After you click **OK** in the **Add Instances** window, a connection test will be performed.

    ![Connection test](./media/mimp/connection-test.png)

    After the connection test is complete, you can view and edit properties of the added instance. For that, select an instance and click **Edit Instance**.

    >[!NOTE]
    >The monitoring template wizard may show the following error: "An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process" or the “Monitoring error” exception while checking connection. For more information, see [Known Issues and Troubleshooting](mimp-known-issues-and-troubleshooting.md)

    ![Edit instasnce parameters](./media/mimp/editing-instance.png)

6. At the **Summary** step, review monitoring settings and click **Create**.

    ![Review summary](./media/mimp/manual-summary.png)