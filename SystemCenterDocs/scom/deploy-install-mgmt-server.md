---
title: Install an Operations Manager management server
description: This article describes how to install an Operations Manager management server.
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: randolphwest
ms.date: 03/19/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
ms.custom: engagement-fy23, engagement-fy24
---

# Install an Operations Manager management server

In System Center Operations Manager, the first feature you install is the management server. The setup procedure creates the operational database and data warehouse database. The procedure described in this article assumes that you've already installed a supported version of Microsoft SQL Server. If you're hosting the Operations Manager operational and data warehouse database on a SQL Server Always On availability group (AG), be sure to use the node planned for the initial Primary replica for initial installation of these databases.

You must ensure that your server meets the minimum system requirements for System Center Operations Manager. For more information, see [System Requirements for System Center - Operations Manager](./system-requirements.md).

Once you've installed the first management server and created the management group, you can follow the steps for installing an additional management server if you're planning to include additional management servers to provide high availability and increased capacity for your monitoring workloads.

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range="sc-om-2016"

> [!NOTE]  
> If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 management server role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.

::: moniker-end

::: moniker range=">=sc-om-2022"

> [!NOTE]  
> You can set up and upgrade Operations Manager databases with an existing SQL Always-On setup without any need for post configuration changes.

::: moniker-end

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

### Install the first management server in the management group

1. Sign in to the server by using an account that has local administrative credentials.

1. On the Operations Manager installation media, run **Setup.exe**, and then select **Install**.

1. On the **Getting Started**, **Select features to install** page, select the **Management server** feature. You can also select any of the additional features listed. For example, to also install the Operations console, select **Operations console**. To read more about each feature and its requirements, select **Expand all**, or expand the buttons next to each feature, and select **Next**.

1. On the **Getting Started**, **Select installation location** page, accept the default value, enter a new location or browse to one, and select **Next**.

1. On the **Prerequisites** page, review and resolve any warnings or errors, and select **Verify Prerequisites Again** to recheck the system.

   > [!IMPORTANT]  
   > You might receive a message that indicates that ASP.NET 4 isn't registered with Internet Information Services (IIS). To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command:
   >
   > `%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r`

1. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

1. On the **Configuration**, **Specify an installation option** page, select **Create the first Management server in a new management group**, type a name for your management group, and then select **Next**.

   > [!NOTE]  
   > After the management group name is set, it can't be changed. The Management Group name cannot contain the following characters: ( ) ^ ~ : ; . ! ? " , ' ` @ # % \ / * + = $ | & [ ] < > { }, and it can't have a leading or trailing space. It's recommended that the Management Group name be unique within your organization if you plan to connect several management groups together.

1. On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and select **Next**.

1. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, enter the name of the server and the name of the SQL Server instance for the database server that will host the operational database.

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server AG, replace `computer\<instance>` with the AG listener, and for **SQL Server port**, enter the port number of the AG listener.

     As you enter the values for the SQL Server and instance names, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values haven't yet been validated, and the black text indicates that you haven't entered any illegal characters. If you enter illegal characters, the text itself turns red.

     The white **X** appears under the following circumstances:

     - You entered an instance of SQL Server or a SQL Server port value that isn't valid or that doesn't exist.

     - The instance of SQL Server that you specified doesn't have the required configuration or features.

     - You entered a value that is out-of-range (for example, port 999999).

     - You entered an illegal character for that box (for example, server\instance%)

     You can hover the cursor over the **Server name and instance name** text box to view additional information about the error.

1. After you enter the correct value for the SQL Server database server name, select the **SQL Server port** box so that Setup will attempt to validate the values you entered for the SQL Server name and for the port number.

1. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Select **Next**.

    > [!NOTE]  
    > These paths don't change if you connect to a different instance of SQL Server.

    > [!IMPORTANT]  
    > You might receive a message about having the wrong version of the SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the `<path>` placeholder with the location of the SQL Server.
    >
    > For SQL Server 2022 and later versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\160\Shared\sqlmgmprovider.mof`
    >
    > For SQL Server 2019 and earlier versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\150\Shared\sqlmgmproviderxpsp2up.mof`

    > [!NOTE]  
    > The SQL Server `model` database size must not be greater than 100 MB. If it is, you might encounter an error in Setup regarding the inability to create a database on SQL due to user permissions. To resolve the issue, you must reduce the size of the `model` database.

1. When the **Configuration**, **Configure the data warehouse database** page opens, in the **Server name and instance name** box, enter the server name and the name of the instance of the SQL Server for the database server that will host the data warehouse database.

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server availability group (AG), replace `computer\<instance>` with the AG listener and for **SQL Server port**, enter the port number of the AG listener.

1. Because this is the first management server installation, accept the default value of **Create a new data warehouse database**.

1. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Select **Next**.

   > [!IMPORTANT]  
   > You might receive a message about having the wrong version of the SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the `<path>` placeholder with the location of SQL Server.
    >
    > For SQL Server 2022 and later versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\160\Shared\sqlmgmprovider.mof`
    >
    > For SQL Server 2019 and earlier versions:
    >
    > `mofcomp.exe \<path>\Microsoft SQL Server\150\Shared\sqlmgmproviderxpsp2up.mof`

   > [!NOTE]  
   > These paths don't change if you connect to a different instance of the SQL Server.

1. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for the **Management server action account**, the **System Center Configuration service and System Center Data Access service** account, the **Data Reader account**, and the **Data Writer account**. None of them should have domain administrator credentials. Select **Next**.

1. On the **Configuration**, **Diagnostic and Usage Data** page, review the information and select **Next**.

1. If Windows Update isn't enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and select **Next**.

1. Review the options on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

1. When Setup is finished, the **Setup is complete** page appears. Select **Close**.

1. Open the Operations console.

1. In the Operations console, in the navigation pane, select the **Administration** button, and then expand **Device Management**.

1. In **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you installed with a green check mark in the **Health State** column.

### Install additional management servers in the management group

Perform the following steps to add additional management servers in your management group.

1. Sign in to the server by using an account that has local administrative credentials.

1. On the Operations Manager installation media, run **Setup.exe**, and select **Install**.

1. On the **Getting Started**, **Select features to install** page, select the **Management server** feature. You can also select any of the additional features listed. For example, to also install the Operations console, select **Operations console**. To read more about each feature and its requirements, select **Expand all**, or expand the buttons next to each feature, and select **Next**.

1. On the **Getting Started**, **Select installation location** page, accept the default value, enter a new location or browse to one, and select **Next**.

1. On the **Configuration, Specify an installation option** page, select **Add a Management server to an existing management group**, and select **Next**.

1. On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and select **Next**.

1. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, enter the name of the server and the name of the SQL Server instance for the database server that will host the operational database.

   - If you installed SQL Server by using the default instance, you only have to enter the server name.
   - If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.
   - If you're hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.
   - If the database is part of a SQL Server AG, replace `computer\<instance>` with the AG listener and for **SQL Server port**, enter the port number of the AG listener.

     As you enter the values for the SQL Server and instance names, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values haven't yet been validated, and the black text indicates that you haven't entered any illegal characters. If you enter illegal characters, the text itself turns red.

     The white **X** appears under the following circumstances:

     - You entered an instance of SQL Server or a SQL Server port value that isn't valid or that doesn't exist.

     - The instance of SQL Server that you specified doesn't have the required configuration or features.

     - You entered a value that is out-of-range (for example, port 999999).

     - You entered an illegal character for that box (for example, server\instance%)

     You can hover the cursor over the **Server name and instance name** text box to view additional information about the error.

1. After you enter the correct value for the SQL Server database server name, select the **SQL Server port** box so that Setup will attempt to validate the values you entered for the SQL Server name and for the port number.

1. Select the database name from the **Database name** dropdown list, and select **Next**.

1. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for the **Management server action account** and the **System Center Configuration service and System Center Data Access service** account. None of them should have domain administrator credentials. Select **Next**.

   > [!IMPORTANT]  
   > You must provide the same credentials for the Management server action account, and the System Center Configuration Service and System Center Data Access service that you provided when you created the first management server in your management group.

1. On the **Configuration**, **Diagnostic and Usage Data** page, review the information and select **Next**.

1. If Windows Update isn't enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and select **Next**.

1. Review the options on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

1. When Setup is finished, the **Setup is complete** page appears. Select **Close**.

1. On a computer with the Operations console installed, sign in with an account that's a member of the Operations Manager Administrators group and launch the Operations console.

1. In the Operations console, in the navigation pane, select the **Administration** button, and then expand **Device Management**.

1. In **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you installed with a green check mark in the **Health State** column.

## Install the first management server in the management group from the command prompt

1. Sign in to the server by using an account that has local administrative credentials.

1. Open the Command Prompt window by using the **Run as Administrator** option.

   > [!NOTE]  
   > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

1. Change the path to where the Operations Manager setup.exe file is located, and run the following command.

   > [!IMPORTANT]  
   > The following command assumes that you specified the Local System for the Management server action account (`/UseLocalSystemActionAccount`) and Data Access service (`/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead.
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

   > [!NOTE]  
   > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

1. Change the path to where the Operations Manager setup.exe file is located, and run the following command.

   > [!IMPORTANT]  
   > The following command assumes that you specified the Local System for the Management server action account (`/UseLocalSystemActionAccount`) and Data Access service (`/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead.
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

## Next steps

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
