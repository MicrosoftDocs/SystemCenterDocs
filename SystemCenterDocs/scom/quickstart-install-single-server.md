---
title: Install Operations Manager on a Single Server
description: This article describes how to install all Operations Manager roles in a simple single-server deployment.
ms.custom: engagement-fy23, UpdateFrequency.5
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/19/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 1ddc69fb-fb40-4631-8b49-fb8288806004
---

# Install Operations Manager on a Single Server

This walkthrough guides you through an installation of System Center - Operations Manager on a single server. The features installed include the following:

- Management server

- Operations console

- Web console

- Reporting server

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

## Prerequisites

You must ensure that your server meets the minimum supported configurations for System Center Operations Manager. For more information, see [System Requirements for System Center  Operations Manager](./system-requirements.md).

**Required SQL Server Components**

- Database Engine Services - Full-Text and Semantic Extractions for Search (as called in SQL Server 2012 and later)

- Reporting Services - Native

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

### Install the single server management group configuration

Follow these steps to install the single server management group configuration:

1. Sign in to the server by using an account that has local administrative credentials.

2. On the System Center Operations Manager installation media, run **Setup.exe**, and then select **Install**.

3. On the **Getting Started**, **Select features to install** page, select the **Management server**, **Operations console**, **Web console**, and **Reporting server** features. To read more about each feature and its requirements, select **Expand all**, or expand the buttons next to each feature. Then select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

::: moniker range="sc-om-2025"

   > [!NOTE]
   > For System Center 2025 - Operations Manager, the default path is:
   > ```
   > C:\Program Files\Microsoft System Center\Operations Manager
   > ```

::: moniker-end

::: moniker range="sc-om-2022"

   > [!NOTE]
   > For System Center 2022 - Operations Manager, the default path is:
   > ```
   > C:\Program Files\Microsoft System Center\Operations Manager
   > ```

::: moniker-end

::: moniker range="sc-om-2019"

   > [!NOTE]
   > For System Center 2019 - Operations Manager, the default path is:
   > ```
   > C:\Program Files\Microsoft System Center\Operations Manager
   > ```

::: moniker-end


::: moniker range="sc-om-2016"

   > [!NOTE]
   > For System Center 2016 - Operations Manager, the default path is:
   > ```
   > C:\Program Files\Microsoft System Center 2016\Operations Manager
   > ```

::: moniker-end

5. On the **Prerequisites** page, review and resolve any warnings or errors, and then select **Verify Prerequisites Again** to recheck the system.

   > [!NOTE]
   > Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and select **Allow**.

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration**, **Specify an installation option** page, select **Create the first Management server in a new management group**, enter a name for your management group and then select **Next**.

   > [!NOTE]
   > After the management group name is set, it can't be changed. The Management Group name can't contain the following characters:
   > ```
   > ( ) ^ ~ : ; . ! ? " , ' ` @ # % \ / * + = $ | & [ ] < > { }
   > ```
   > Also, the Management Group name can't have a leading or trailing space. It's recommended that the Management Group name be unique within your organization if you plan to connect several management groups together.

8. On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and select **Next**.

9. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, enter the name of the server and the name of the SQL Server instance for the database server that will host the operational database. If you installed the SQL Server by using the default instance, you only have to enter the server name. If you changed the default SQL Server port, you must enter the new port number in the **SQL Server port** box.

    If you enter an invalid SQL Server and instance name, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port**.

    The white **X** appears under the following circumstances:

   - You entered an instance of SQL Server or a SQL Server port value that isn't valid or that doesn't exist.

   - The instance of SQL Server that you specified doesn't have the required configuration or features.

   - You entered a value that is out-of-range (for example, port 999999).

   - You entered an illegal character for that box (for example, server\instance%).

     You can hover the cursor over the **Server name and instance** text box to view additional information about the error.

10. After you enter the correct value for the SQL Server database server name, select the **SQL Server port** box so that Setup will attempt to validate the values you entered for the SQL Server name and for the port number.

11. In the **Database name**, **Database size (MB)Data file folder**, and **Log file folder** box, we recommend that you accept the default values. Select **Next**

    > [!NOTE]
    > These paths don't change if you connect to a different instance of the SQL Server.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of the SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the *<path\>* placeholder with the location of the SQL Server:
    >
    > ```
    > mofcomp.exe "<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof"
    > ```

    > [!NOTE]
    > The SQL Server model database size must not be greater than 100 MB. If it is, you might encounter an error in Setup regarding the inability to create a database on SQL due to user permissions. To resolve the issue, you must reduce the size of the model database.

12. When the **Configuration**, **Configure the data warehouse database** page opens, in the **Server name and instance name** box, enter the server name and the name of the instance of SQL Server for the database server that will host the data warehouse database.

13. Because this is a single-server installation, accept the default value of **Create a new data warehouse database**.

14. In the **Database name**, **Database size (MB)Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Select **Next**.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of the SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the *<path\>* placeholder with the location of SQL Server:
    >
    > ```
    > mofcomp.exe "<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof"
    > ```

    > [!NOTE]
    > These paths don't change if you connect to a different instance of the SQL Server.

15. On the **Configuration**, **SQL Server instance for reporting services** page, select the SQL Server database instance from the dropdown list. This dropdown list contains the SQL Server database instance name that was created when you installed the SQL Server. Select **Next**.

16. On the **Configuration**, **Specify a web site for use with the Web console** page, select **Default Web Site** or the name of an existing website. Select the option **Enable SSL** only if the website has been configured to use SSL, and select **Next**.

17. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and select **Next**.

18. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use **Domain Account** option for the **Management Server Action Account**, **System Center Configuration service and System Center Data Access service**, the **Data Reader account**, and the **Data Writer account**.

    Enter the credentials for a domain account in each field. The error icon will disappear after account validation. Select **Next**.

19. On the **Configuration**, **Diagnostic and Usage Data** page, review the information and select **Next**.

20. If Windows Update isn't activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and select **Next**.

21. Review the options on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

22. When Setup is finished, the **Setup is complete** page appears. Select **Close** and the Operations console will open.

### Install the Operations Manager single server management group configuration from the command prompt

Follow these steps to install the Operations Manager single server management group configuration from the command prompt:

1. Sign in to the server by using an account that has local administrative credentials.

2. Open the command prompt by using the **Run as Administrator** option.

    > [!NOTE]
    > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

3. Change the path to where the System Center Operations Manager setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated.
    >
    > For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account (`/UseLocalSystemActionAccount`) and Data Access service (`/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead.
    >
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    >
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    setup.exe /silent /install
    /components:OMServer,OMConsole,OMWebConsole,OMReporting
    /ManagementGroupName: "<ManagementGroupName>"
    /SqlServerInstance: <server\instance>
    /SqlInstancePort: <SQL instance port number>
    /DatabaseName: <OperationalDatabaseName>
    /DWSqlServerInstance: <server\instance>
    /DWSqlInstancePort: <SQL instance port number>
    /DWDatabaseName: <DWDatabaseName>
    /UseLocalSystemActionAccount /UseLocalSystemDASAccount
    /DatareaderUser: <domain\username>
    /DatareaderPassword: <password>
    /DataWriterUser: <domain\username>
    /DataWriterPassword: <password>
    /AcceptEndUserLicenseAgreement: [0|1]
    /WebSiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    /SRSInstance: <server\instance>
    /SendODRReports: [0|1]
    /EnableErrorReporting: [Never|Queued|Always]
    /SendCEIPReports: [0|1]
    /UseMicrosoftUpdate: [0|1]
    ```

::: moniker range=">=sc-om-2022"

## Removed dependency on LocalSystem account

Operations Manager provides the following changes:

- LocalSystem is no longer used internally instead of the Default Action Account.
This was used earlier for APM configuration, Privileged Monitoring Account, RunAs Profile fallback. There was an association created for the Validate Subscription Account RunAs Profile.  
- LocalSystem account is still being added to Operations Manager Administrators Group by Setup, but it's now visible in the console and can be removed and added later as required.  

::: moniker-end

## Verify the installation

### Confirm the health of the management server

Follow these steps to confirm the health of the management server:

1. In the Operations console, select the **Administration** workspace.

2. In **Device Management**, select **Management Servers**. In the results pane, you should see the Management server that you installed with a green check mark in the **Health State** column.

### Confirm the health of Operations Manager reports

Follow these steps to confirm the health of Operations Manager reports:

1. In the Operations console, in the navigation pane, select the **Reporting** button.

    > [!NOTE]
    > After the initial deployment, it can take up to 30 minutes for the reports to appear.

2. Select **Microsoft ODR Report Library**, and then double-click any of the reports listed. The selected report is generated and displays in a new window.

    By default, you should see the following reports:

    - **Alerts Per Day**

    - **Instance Space**

    - **Management Group**

    - **Management Packs**

    - **Most Common Alerts**

    > [!NOTE]
    > Selecting the Management Packs report is particularly useful at this point because it provides you with a full inventory of the management packs that have been installed on your server.

3. Close the report window.

## Next steps

Now that you've installed System Center Operations Manager, you can deploy agents and start monitoring your applications, servers, and network devices. For more information, see [Agent deployment planning](plan-planning-agent-deployment.md) and [Operations Manager Monitoring Scenarios](manage-monitoring-scenarios.md).
