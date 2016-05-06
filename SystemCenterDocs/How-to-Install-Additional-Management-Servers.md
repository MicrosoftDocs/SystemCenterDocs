---
title: How to Install Additional Management Servers
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 399ecf87-5a24-42d5-9925-4a82cb4e3d5b
---
# How to Install Additional Management Servers
After you have installed [!INCLUDE[om12long](./Token/om12long_md.md)], you can add additional management servers and join them to your existing management group.

> [!IMPORTANT]
> If you install a stand\-alone web console on a server, you will not be able to add the management server feature to this server. If you want to install the management server and web console on the same server, you must either install both features simultaneously, or install the management server before you install the web console.

You must ensure that your server meets the minimum system requirements for [!INCLUDE[om12long](./Token/om12long_md.md)]. For more information, see [System Requirements for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650).

> [!IMPORTANT]
> Before you follow these procedures, read the [Before You Begin](assetId:///d81818d2-534e-475c-98e1-65496357d5a5#BKMK_BeforeYouBegin) section of [Deploying System Center 2012 \- Operations Manager](assetId:///d81818d2-534e-475c-98e1-65496357d5a5).

### To install additional management servers

1.  Log on to the server with an account that has local administrative credentials.

2.  On the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select **Management server**.

    You can also additional features, such as the Operations console. Select **Operations console**. To read more about each feature and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default location of **C:\\Program Files\\System Center 2012\\Operations Manager**, or type in a new location or browse to one, and then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Specify an installation option** page, select **Add a Management server to an existing management group**, and then click **Next**.

8.  When the **Configuration**, **Configure the operational database** page opens, type the name of the SQL Server database server and instance for the database server that hosts the operational database in the **Server name and instance name** box. If you installed SQL Server by using the default instance, you only have to enter the server name. If you changed the default SQL Server port, you must type in the new port number in the **SQL Server port** box.

    As you type the values for SQL Server and instance name, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values have not yet been validated. The black text indicates that you have not entered any illegal characters. If you enter illegal characters, the text itself turns red.

9. After you have typed the correct values for the name of the SQL Server database server, click the **SQL Server port** box. Setup attempts to validate the values that you have typed for the SQL Server name and the port number.

10. Select the database name from the **Database name** drop\-down list, and then click **Next**.

11. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for the **Management server action account** and the **System Center Configuration service and System Center Data Access service** account. Neither of them should have domain administrator credentials. Click **Next**.

    > [!IMPORTANT]
    > You must provide the same credentials for the Management server action account and the System Center Configuration Service and System Center Data Access service that you provided when you created the first management server in your management group.

12. If Windows Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

13. Review the options on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

14. When setup is finished, the **Setup is complete** page appears. Click **Close**.

15. Open the Operations console.

16. In the Operations console, select the **Administration** workspace, and then expand **Device Management**.

17. In **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you just installed with a green check mark in the **Health State** column.

### To install additional management servers by using the Command Prompt window

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the [!INCLUDE[om12short](./Token/om12short_md.md)] setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account \(`/UseLocalSystemActionAccount`\) and Data Access service \(`/UseLocalSystemDASAccount`\). To specify a domain\\user name for these accounts, you must provide the following parameters instead.
    > 
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    > 
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    setup.exe /silent /install /components:OMServer
    /SqlServerInstance: <server\instance>
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

## See Also
[Distributed Deployment of Operations Manager for System Center 2012](assetId:///e9b6f067-8f3e-465e-9a0f-f3ae46859bd6)


