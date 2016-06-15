---
title: Walkthrough: Installing Operations Manager on a Single Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 76eb99bf-9aca-49d1-b5e7-63909fd21b13
---
# Walkthrough: Installing Operations Manager on a Single Server
This walkthrough guides you through an installation of [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)] on a single server. The features installed include the following:

-   Management server

-   Operations console

-   Web console

-   Reporting server

## Prerequisites
You must ensure that your server meets the minimum supported configurations for [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)]. For more information, see [System Requirements for System Center Technical Preview](../../system-requirements/System-Requirements-for-System-Center-Technical-Preview.md).

**Required SQL Server Components**

-   Database Engine Services \- Full\-Text and Semantic Extractions for Search \(as called in SQL Server 2012\)

-   Reporting Services \- Native

### To install the single server management group configuration

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)] installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page select the **Management server**, **Operations console**, **Web console**, and **Reporting server** features. To read more about each feature and its requirements, click **Expand all**, or expand the buttons next to each feature. Then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default value of **C:\\Program Files\\System Center 2016\\Operations Manager** or type in a new location or browse to one. Then click **Next**.

5.  On the **Prerequisites** page, review and resolve any warnings or errors, and then click **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    > Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double\-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

    > [!IMPORTANT]
    > You must install IIS before installing .NET Framework 4. If you installed IIS after installing .NET Framework 4, you must register ASP.NET 4.0 with IIS. Open a Command prompt window by using the **Run As Administrator** option and then run the following command:
    > 
    > **%WINDIR%\\Microsoft.NET\\Framework64\\v4.0.30319\\aspnet\_regiis.exe \-r**

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Specify an installation option** page, select **Create the first Management server in a new management group**, type in a name for your management group and then click **Next**.

    > [!NOTE]
    > After the management group name is set, it cannot be changed. The Management Group name cannot contain the following characters:, \( \) ^ ~ : ; . \! ? " , ' \` @ \# % \\ \/ \* \+ \= $ | & \[ \] <>{}, and it cannot have a leading or trailing space. It is recommended that the Management Group name be unique within your organization if you plan to connect several management groups together.

8.  On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and then click **Next**.

9. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, type the name of the server and the name of the SQL Server instance for the database server that will host the operational database. If you installed SQL Server by using the default instance, you only have to enter the server name. If you changed the default SQL Server port, you must type in the new port number in the **SQL Server port** box.

    If you type an invalid SQL Server and instance name, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port**.

    The white **X** appears under the following circumstances:

    -   You entered an instance of SQL Server or a SQL Server port value that is not valid or that does not exist.

    -   The instance of SQL Server that you specified does not have the required configuration or features.

    -   You entered a value that is out\-of\-range \(for example, port 999999\).

    -   You entered an illegal character for that box \(for example, server\\instance%\)

    You can hover the cursor over the **Server name and instance** text box to view additional information about the error.

10. After you type the correct value for the SQL Server database server name, click the **SQL Server port** box so that Setup will attempt to validate the values you typed for the SQL Server name and for the port number.

11. In the **Database name**, **Database size \(MB\)Data file folder**, and **Log file folder** box, we recommend that you accept the default values. Click **Next**

    > [!NOTE]
    > These paths do not change if you connect to a different instance of SQL Server.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation \(WMI\) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the *\<path\>*  placeholder with the location of SQL Server:
    > 
    > **mofcomp.exe “\<path>\\Microsoft SQL Server\\100\\Shared\\sqlmgmproviderxpsp2up.mof”**

    > [!NOTE]
    > The SQL Server model database size must not be greater than 100 MB. If it is, you might encounter an error in Setup regarding the inability to create a database on SQL due to user permissions. To resolve the issue, you must reduce the size of the model database.

12. When the **Configuration**, **Configure the data warehouse database** page opens, in the **Server name and instance name** box, type the server name and the name of the instance of SQL Server for the database server that will host the data warehouse database.

13. Because this is a single\-server installation, accept the default value of **Create a new data warehouse database**.

14. In the **Database name**, **Database size \(MB\)Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Click **Next**.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation \(WMI\) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the *\<path\>* placeholder with the location of SQL Server:
    > 
    > **mofcomp.exe “\<path>\\Microsoft SQL Server\\100\\Shared\\sqlmgmproviderxpsp2up.mof”.**

    > [!NOTE]
    > These paths do not change if you connect to a different instance of SQL Server.

15. On the **Configuration**, **SQL Server instance for reporting services** page, select the SQL Server database instance from the drop\-down list. This drop\-down list contains the SQL Server database instance name that was created when you installed SQL Server 2012 or 2012 SP1, SQL Server 2014 or 2014 SP1, or SQL Server 2016 RC1 and should be the name of the server on which you are installing [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)]. Click **Next**.

16. On the **Configuration**, **Specify a web site for use with the Web console** page, select **Default Web Site** or the name of an existing website. Select the option **Enable SSL** only if the website has been configured to use SSL, and then click **Next**.

17. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and then click **Next**.

18. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use **Domain Account** option for the **Management Server Action Account**, **System Center Configuration service and System Center Data Access service**, the **Data Reader account**, and the **Data Writer account**.

    Enter the credentials for a domain account in each field. The error icon will disappear after account validation. Click **Next**.

19. On the **Configuration**, **Help improve System Center 2016 \- Operations Manager** page, select your options and click **Next**.

20. If Windows Update is not activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

21. Review the options on the **Configuration**, **Installation Summary** page, and click **Install**. Setup continues.

22. When Setup is finished, the **Setup is complete** page appears. Click **Close** and the Operations console will open.

### To install the System Center 2016 \- Operations Manager single server management group configuration by using the Command Prompt window

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

    > [!NOTE]
    > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

3.  Change the path to where the [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)] setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer \(SSL\) activated.
    > 
    > For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account \(`/UseLocalSystemActionAccount`\) and Data Access service \(`/UseLocalSystemDASAccount`\). To specify a domain\\user name for these accounts, you must provide the following parameters instead.
    > 
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    > 
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    setup.exe /silent /install
    /components:OMServer,OMConsole,OMWebConsole,OMReporting
    /ManagementGroupName: "<ManagementGroupName>"
    /SqlServerInstance: <server\instance>
    /DatabaseName: <OperationalDatabaseName>
    /DWSqlServerInstance: <server\instance>
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

## Verifying the Installation

#### To confirm the health of the Management server

1.  In the Operations console, select the **Administration** workspace.

2.  In **Device Management** select **Management Servers**. In the results pane, you should see the Management server that you just installed with a green check mark in the **Health State** column.

#### To confirm the health of Operations Manager reports

1.  In the Operations console, in the navigation pane, click the **Reporting** button.

    > [!NOTE]
    > After initial deployment, it can take up to 30 minutes for reports to appear.

2.  Click **Microsoft ODR Report Library**, and then double\-click any of the reports listed. The selected report is generated and displays in a new window.

    By default, you should see the following reports:

    -   **Alerts Per Day**

    -   **Instance Space**

    -   **Management Group**

    -   **Management Packs**

    -   **Most Common Alerts**

    > [!NOTE]
    > Selecting the Management Packs report is particularly useful at this point because it provides you with a full inventory of the management packs that have been installed on your server.

3.  Close the report window.

## Next Steps
Now that you have installed [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)], you can deploy agents and start monitoring your applications, servers, and network devices. For more information, see [Managing Discovery and Agents](http://go.microsoft.com/fwlink/p/?LinkID=207756) and [Operations Manager 2016 Monitoring Scenarios](http://go.microsoft.com/fwlink/p/?LinkID=218372).


