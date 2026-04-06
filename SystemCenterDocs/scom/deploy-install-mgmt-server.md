---
title: Install an Operations Manager Management Server
description: This article describes how to install an Operations Manager management server.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/19/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
ms.custom: engagement-fy23, engagement-fy24
ms.update-cycle: 365-days
---

# Install an Operations Manager management server

In System Center Operations Manager, the first feature that you install is the management server. The setup procedure creates the operational database and the data warehouse database.

The procedures that this article describes assume that you already installed a supported version of Microsoft SQL Server. If you're hosting the Operations Manager operational database and data warehouse database on a SQL Server Always On availability group (AG), be sure to use the node planned for the initial primary replica for initial installation of these databases.

After you install the first management server and create the management group, you can follow the steps for installing additional management servers. Additional management servers can help provide high availability and increased capacity for your monitoring workloads.

## Prerequisites

Ensure that your server meets the minimum [system requirements for Operations Manager](./system-requirements.md).

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range="sc-om-2016"

## Important considerations

If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 management server role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way that you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.

::: moniker-end

::: moniker range=">=sc-om-2022"

## Important considerations

You can set up and upgrade Operations Manager databases by using an existing SQL Server Always On setup, without any need for post-configuration changes.

::: moniker-end

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

## Install the first management server in the management group

1. Sign in to the server by using an account that has local administrative credentials.

1. On the Operations Manager installation media, run **Setup.exe**, and then select **Install**.

1. On the **Getting Started** > **Select features to install** page, select the **Management server** feature.

   You can also select any of the additional features listed. For example, to install the operations console, select **Operations console**. To read more about each feature and its requirements, select **Expand all** (or expand the button next to each feature). Then select **Next**.

1. On the **Getting Started** > **Select installation location** page, accept the default value. Or you can enter a new location or browse to one. Then select **Next**.

1. On the **Prerequisites** page, review and resolve any warnings or errors. Then select **Verify Prerequisites Again** to recheck the system.

   > [!IMPORTANT]  
   > You might receive a message that indicates that ASP.NET 4 isn't registered with Internet Information Services (IIS). To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command:
   >
   > `%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r`

1. If the prerequisites checker doesn't return any warnings or errors, the **Prerequisites** > **Proceed with Setup** page appears. Select **Next**.

1. On the **Configuration** > **Specify an installation option** page, select **Create the first Management server in a new management group**. Enter a name for your management group, and then select **Next**.

   > [!NOTE]  
   > After you set the management group, you can't change it.
   >
   > The name of the management group can't contain the following characters: ( ) ^ ~ : ; . ! ? " , ' ` @ # % \ / * + = $ | & [ ] < > { }. Also, it can't have a leading or trailing space.
   >
   > If you plan to connect several management groups together, we recommend ensuring that the name of the management group is unique within your organization.

1. On the **Configuration** > **Please read the license terms** page, review the Microsoft Software License Terms. Select **I have read, understood and agree with the license terms**, and then select **Next**.

1. When the **Configuration** > **Configure the operational database** page opens, fill in the **Server name and instance name** box. Enter the name of the server and the name of the SQL Server instance for the database server that will host the operational database. Keep these points in mind:

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server AG, replace `computer\<instance>` with the AG listener. For **SQL Server port**, enter the port number of the AG listener.

   As you enter the values for the server and instance names, a red circle with a white **X** appears to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values aren't validated yet. The black text indicates that you didn't enter any illegal characters. If you enter illegal characters, the text itself turns red.

   The white **X** appears under the following circumstances:

   - You entered a SQL Server instance or a SQL Server port value that isn't valid or that doesn't exist.
   - The SQL Server instance that you specified doesn't have the required configuration or features.
   - You entered a value that's out of range (for example, port 999999).
   - You entered an illegal character for that box (for example, **server\instance%**).

   You can hover over the **Server name and instance name** box to view more information about the error.

1. After you enter the correct value for the SQL Server database server name, select the **SQL Server port** box. Setup attempts to validate the values that you entered for the server name and for the port number.

1. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Select **Next**.

    These paths don't change if you connect to a different SQL Server instance.

    > [!IMPORTANT]  
    > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the `<path>` placeholder with the location of the SQL Server instance.
    >
    > For SQL Server 2022 and later versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\160\Shared\sqlmgmprovider.mof`
    >
    > For SQL Server 2019 and earlier versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\150\Shared\sqlmgmproviderxpsp2up.mof`

    The SQL Server `model` database size must not be greater than 100 MB. If it is, you might encounter an error in Setup regarding the inability to create a database on SQL Server due to user permissions. To resolve the problem, you must reduce the size of the `model` database.

1. When the **Configuration** > **Configure the data warehouse database** page opens, fill in the **Server name and instance name** box. Enter the name of the server and the name of the SQL Server instance for the database server that will host the data warehouse database. Keep these points in mind:

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server AG, replace `computer\<instance>` with the AG listener. For **SQL Server port**, enter the port number of the AG listener.

1. Because this is the first management server installation, accept the default value of **Create a new data warehouse database**.

1. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Select **Next**.

   > [!IMPORTANT]  
   > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server WMI provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the `<path>` placeholder with the location of the SQL Server instance.
    >
    > For SQL Server 2022 and later versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\160\Shared\sqlmgmprovider.mof`
    >
    > For SQL Server 2019 and earlier versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\150\Shared\sqlmgmproviderxpsp2up.mof`

   These paths don't change if you connect to a different SQL Server instance.

1. On the **Configuration** > **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for **Management server action account**, the **System Center Configuration service and System Center Data Access service** account, **Data Reader account**, and **Data Writer account**. None of them should have domain administrator credentials. Select **Next**.

1. On the **Configuration** > **Diagnostic and Usage Data** page, review the information and select **Next**.

1. If Windows Update isn't enabled on the computer, the **Configuration** > **Microsoft Update** page appears. Select your options, and then select **Next**.

1. Review the options on the **Configuration** > **Installation Summary** page, and then select **Install**.

1. When Setup finishes, the **Setup is complete** page appears. Select **Close**.

1. Open the operations console.

1. On the left pane, select the **Administration** button, and then expand **Device Management**.

1. In **Device Management**, select **Management Servers**. On the results pane, the management server that you installed should appear with a green check mark in the **Health State** column.

## Install additional management servers in the management group

1. Sign in to the server by using an account that has local administrative credentials.

1. On the Operations Manager installation media, run **Setup.exe**, and then select **Install**.

1. On the **Getting Started** > **Select features to install** page, select the **Management server** feature.

   You can also select any of the additional features listed. For example, to install the operations console, select **Operations console**. To read more about each feature and its requirements, select **Expand all** (or expand the button next to each feature). Then select **Next**.

1. On the **Getting Started** > **Select installation location** page, accept the default value. Or you can enter a new location or browse to one. Then select **Next**.

1. On the **Configuration** > **Specify an installation option** page, select **Add a Management server to an existing management group**. Then select **Next**.

1. On the **Configuration** > **Please read the license terms** page, review the Microsoft Software License Terms. Select **I have read, understood and agree with the license terms**, and then select **Next**.

1. When the **Configuration** > **Configure the operational database** page opens, fill in the **Server name and instance name** box. Enter the name of the server and the name of the SQL Server instance for the database server that will host the operational database. Keep these points in mind:

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server AG, replace `computer\<instance>` with the AG listener. For **SQL Server port**, enter the port number of the AG listener.

   As you enter the values for the server and instance names, a red circle with a white **X** appears to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values aren't validated yet. The black text indicates that you didn't enter any illegal characters. If you enter illegal characters, the text itself turns red.

   The white **X** appears under the following circumstances:

   - You entered a SQL Server instance or a SQL Server port value that isn't valid or that doesn't exist.
   - The SQL Server instance that you specified doesn't have the required configuration or features.
   - You entered a value that's out of range (for example, port 999999).
   - You entered an illegal character for that box (for example, **server\instance%**).

   You can hover over the **Server name and instance name** box to view more information about the error.

1. After you enter the correct value for the SQL Server database server name, select the **SQL Server port** box. Setup attempts to validate the values that you entered for the server name and for the port number.

1. Select the database name from the **Database name** dropdown list, and then select **Next**.

1. On the **Configuration** > **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for **Management server action account** and the **System Center Configuration service and System Center Data Access service** account. Neither of them should have domain administrator credentials. Select **Next**.

   > [!IMPORTANT]  
   > For these accounts, you must provide the same credentials that you provided when you created the first management server in your management group.

1. On the **Configuration** > **Diagnostic and Usage Data** page, review the information and select **Next**.

1. If Windows Update isn't enabled on the computer, the **Configuration** > **Microsoft Update** page appears. Select your options, and then select **Next**.

1. Review the options on the **Configuration** > **Installation Summary** page, and then select **Install**.

1. When Setup finishes, the **Setup is complete** page appears. Select **Close**.

1. On a computer where the operations console is installed, sign in with an account that's a member of the Operations Manager Administrators group. Then open the operations console.

1. On the left pane, select the **Administration** button, and then expand **Device Management**.

1. In **Device Management**, select **Management Servers**. On the results pane, the management server that you installed should appear with a green check mark in the **Health State** column.

## Install the first management server in the management group from the command prompt

1. Sign in to the server by using an account that has local administrative credentials.

1. Open the Command Prompt window by using the **Run as Administrator** option.

   **Setup.exe** requires administrator privileges because the setup process requires access to system processes that only a local administrator can use.

1. Change the path to where the Operations Manager **Setup.exe** file is located, and run the following command.

   > [!IMPORTANT]  
   > The following command assumes that you specified the local system for the management server action account (`/UseLocalSystemActionAccount`) and the Data Access service account (`/UseLocalSystemDASAccount`). To specify a domain and user name for these accounts, you must provide these parameters instead:
   >
   > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
   >
   > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

   ```console
   setup.exe /silent /install /components:OMServer
   /ManagementGroupName: "<ManagementGroupName>"
   /SqlServerInstance: <server\instance or AG listener>
   /SqlInstancePort: <SQL instance port number>
   /DatabaseName: <OperationalDatabaseName>
   /DWSqlServerInstance: <server\instance or AG listener>
   /DWSqlInstancePort: <SQL instance port number>
   /DWDatabaseName: <DWDatabaseName>
   /UseLocalSystemActionAccount /UseLocalSystemDASAccount
   /DatareaderUser: <domain\username>
   /DatareaderPassword: <password>
   /DataWriterUser: <domain\username>
   /DataWriterPassword: <password>
   /EnableErrorReporting: [Never|Queued|Always]
   /SendCEIPReports: [0|1]
   /UseMicrosoftUpdate: [0|1]
   /AcceptEndUserLicenseAgreement: [0|1]
   ```

## Install additional management servers in the management group from the command prompt

1. Sign in to the server by using an account that has local administrative credentials.

1. Open the Command Prompt window by using the **Run as Administrator** option.

   **Setup.exe** requires administrator privileges because the setup process requires access to system processes that only a local administrator can use.

1. Change the path to where the Operations Manager **Setup.exe** file is located, and run the following command.

   > [!IMPORTANT]  
   > The following command assumes that you specified the local system for the management server action account (`/UseLocalSystemActionAccount`) and the Data Access service account (`/UseLocalSystemDASAccount`). To specify a domain and user name for these accounts, you must provide these parameters instead:
   >
   > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
   >
   > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

   ```console
   setup.exe /silent /install /components:OMServer
   /SqlServerInstance: <server\instance or AG listener>
   /SqlInstancePort: <SQL instance port number>
   /DatabaseName: <OperationalDatabaseName>
   /UseLocalSystemActionAccount /UseLocalSystemDASAccount
   /DataReaderUser: <domain\username>
   /DataReaderPassword: <password>
   /DataWriterUser: <domain\username>
   /DataWriterPassword: <password>
   /EnableErrorReporting: [Never|Queued|Always]
   /SendCEIPReports: [0|1]
   /UseMicrosoftUpdate: [0|1]
   ```

## Related content

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed deployment of Operations Manager](deploy-distributed-deployment.md).
