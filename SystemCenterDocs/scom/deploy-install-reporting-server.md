---
ms.assetid: bc3c9818-6019-4af3-bcaa-990229650c0c
title: How to Install the Operations Manager Reporting Server
description: This article describes how to install the Operations Manager Reporting server role.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to install the Operations Manager Reporting server

In this procedure, the Reporting server is installed on a stand-alone server that is hosting the SQL Server database and SQL Server Reporting Services.

> [!WARNING]
> Although SQL Server Reporting Services is installed on the stand-alone server, Operations Manager reports are not accessed on this server; instead, they are accessed in the **Reporting** workspace in the Operations console. If you want to access published reports via the web console, you must install the Operations Manager web console on the same computer as Operations Manager Reporting server.

You must ensure that your server meets the minimum system requirement for Operations Manager. For more information, see [System Requirements for System Center 2016 - Operations Manager](/system-center/orchestrator/system-requirements).

## Installing Operations Manager reporting

No other applications that are using SQL Server Reporting Services can be installed on this instance of SQL Server.

Ensure that SQL Server Reporting Services has been correctly installed and configured. For more information about how to install and configure SQL Server Reporting Services, see [SQL Server Installation (SQL Server 2012)](https://go.microsoft.com/fwlink/p/?LinkId=146943).

> [!NOTE]
> Before you continue with this procedure, ensure that the account you plan to use for the Data Warehouse Write account has SQL Server logon rights and is an Administrator on the computers hosting both the operational database and the Reporting data warehouse database. Otherwise, Setup fails, and all changes are rolled back, which might leave SQL Server Reporting Services in an inoperable state.

#### To verify that Reporting Services is configured correctly

1.  Verify that the **ReportServer** and **ReportServerTempDB** databases in SQL Server Management Studio are located on the stand-alone server. Open **SQL Server Management Studio**, and then connect to the default database instance. Open the **Databases** node and verify that the two Reporting Services databases exist under this node.

2.  Verify the correct configuration of SQL Server Reporting Services. Click **Start**, point to **Programs**, point to the appropriate offering of Microsoft SQL Server, point to **Configuration Tools**, and then click **Reporting Services Configuration Manager**. Connect to the instance on which you installed Reporting Services.

3.  In the navigation pane, select the `<servername>\SQLinstance`. This displays the Report Server status in the results pane. Ensure that the **Report Server Status** is **Started**.

4.  In the navigation pane, select **Scale-out Deployment**, and then ensure that the **Status** column has the value of **Joined**.

5.  If **Report Server** is not started and the **Scale out Deployment** is not joined, check the configuration of **Service Account**, **Web Service URL**, and **Database**.

6.  Confirm that the SQL Server Reporting Services service is running. On the taskbar, click **Start**, point to **Administrative Tools**, and then click **Services**.

7.  In the **Name** column, find the **SQL Server Reporting Services** instance service and verify that its status reads **Started** and that the **Startup Type** is **Automatic**.

8.  In the **Name** column, find the **SQL Server Agent** service and verify that its status reads **Started** and that its **Startup Type** is **Automatic**.

9. Verify that the Report Server website is functioning and available by browsing to `http://\<servername>/reportserver/_<$instance>`. You should see a page with the `<servername>/ReportServer/_<$instance>` and the text, **Microsoft SQL Server Reporting Services Version** ##.#.####.## where the # is the version number of your SQL Server installation.

10. Verify that the Report Manager website is configured correctly by opening **Internet Explorer** and browsing to `http://<servername>/reports/_<$instance>`.

11. In the Report Manager website, click **New Folder** to create a new folder. Enter a name and description, and then click **OK**. Ensure that the new, created folder is visible on the Report Manager website.

#### To install Operations Manager reporting

1.  Log on to the computer with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select the **Reporting server** feature. To read more about each feature and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default value of **C:\Program Files\System Center 2016\Operations Manager** or type a new location or browse to one, and then click **Next**.

5.  On the **Prerequisites** page, review and resolve any warnings or errors, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, continue to the **Prerequisites**, **Proceed with Setup** page. Click **Next**.

7.  On the **Configuration**, **Specify a Management server** page, enter the name of a management server that is used by the Reporting features only. Then click **Next**.

8.  On the **Configuration**, **SQL Server instance for reporting services** page, select the instance of SQL Server that hosts SQL Server Reporting Services, and then click **Next**.

9. On the **Configuration**, **Configure Operations Manager accounts** page, enter the credentials for the **Data Reader account**, and then click **Next**.

10. On the **Configuration**, **Help improve System Center - Operations Manager** page, select your options, and then click **Next**.

11. If Windows Update is not activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

12. Review the options on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

13. When Setup is finished, the **Setup is complete** page appears. Click **Close**.

#### To install Operations Manager reporting from the Command Prompt

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!NOTE]
    > The /ManagementServer parameter is only required when you are installing reporting on a server that is not a management server.

    ```
    setup.exe /silent /install /components:OMReporting 
    /ManagementServer: "<ManagementServerName>"
    /SRSInstance: <server\instance>
    /DataReaderUser: <domain\username>
    /DataReaderPassword: <password>
    /SendODRReports: [0|1]
    /UseMicrosoftUpdate: [0|1]
    ```

#### To confirm the health of Operations Manager reports

1.  Open the Operations console, and select the **Reporting** workspace.

    > [!NOTE]
    > After initial deployment, reports can require up to 30 minutes to appear.

2.  Click **Microsoft ODR Report Library**, and then double-click any of the reports listed. The selected report is then generated and displayed in a new window.

    By default, you should see the following reports:

    -   **Alerts Per Day**

    -   **Instance Space**

    -   **Management Group**

    -   **Management Packs**

    -   **Most Common Alerts**

3.  Close the report window.

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  



