---
title: Disaster Recovery in System Center 2012 - Operations Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ef1b1b2-e6e8-4750-817a-fc6b8519077f
---
# Disaster Recovery in System Center 2012 - Operations Manager
Various [!INCLUDE[om12long](Token/om12long_md.md)] servers and features can potentially fail, impacting [!INCLUDE[om12short](Token/om12short_md.md)] functionality. The amount of data and functionality lost during a failure is different in each failure scenario. It depends on the role of the failing feature, the length of time it takes to restore the failing feature, and on the availability of backups.

You should always keep a backup of your operational database and data warehouse database. For information about scheduling regular backups of the [!INCLUDE[om12short](Token/om12short_md.md)] databases, see [How to Schedule Backups of Operations Manager Databases](assetId:///301b7af3-3695-41b5-b91c-e1a672bce591).

The amount of data and functionality lost during a failure is different in each failure scenario. The impact of failure is minimized if the [!INCLUDE[om12short](Token/om12short_md.md)] deployment includes multiple management servers. The impact is greater if only one management server is implemented. This is because you do not have a second management server which can take on the load if one fails, and you will lose all monitoring capabilities. The impact of failure of a management server in a distributed environment is minimized, but it increases the workload on additional management servers in the management group until the failed management server is restored.

## Recovering Operations Manager Features
If your [!INCLUDE[om12short](Token/om12short_md.md)] databases have failed, you can restore them from back up. For more information, see [How to Restore Operations Manager Databases](assetId:///369e3f08-c1a3-4d2d-ad69-0f6e4d3c663e).

If your Operations console, web console, or Reporting server have failed, you must reinstall them. For information on installing these features, see

-   [How to Install the Operations Manager Web Console](assetId:///9fbc3f03-a8e4-4ef8-b154-822936849630)

-   [How to Install the Operations Console](assetId:///a23f0a8f-e685-439e-9cd8-48bc90ab7c2f)

-   [How to Install the Operations Manager Reporting Server](assetId:///15404d1e-ad4b-4734-997c-c4992aba31ad)

If one or more management servers have failed, you can recover them by using the **setup.exe** command with a **\/recover** switch in Command Prompt window. There are two scenarios for recovery. The first scenario is when you have to recover a management server when all management servers in the management group have failed. In this case, you must recover all of the failed management servers, and then reconfigure the RunAs accounts. The second scenario is when you have a failed management server, but one or more management servers are still online. In this case, you just recover all of the failed management servers. You should not reconfigure the RunAs accounts.

#### To Recover a Management Server

1.  Build a new server, ensuring that it meets the minimum supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)], and use the same name that was given to the failed management server.

2.  Restore the operational database and data warehouse database, if required. For more information, see [How to Restore Operations Manager Databases](assetId:///369e3f08-c1a3-4d2d-ad69-0f6e4d3c663e).

3.  On the new server, open a Command Prompt window by using the Run as Administrator option, and run the following command:

    > [!NOTE]
    > This process only recovers the management server. If consoles or Reporting were also installed on the failed management server, you must reinstall them after recovery is complete.

    > [!IMPORTANT]
    > You must use the same parameter values for account credentials, management group, and database names as the failed server you are trying to recover.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account \(`/UseLocalSystemActionAccount`\) and Data Access service \(`/UseLocalSystemDASAccount`\). To specify a domain\\user name for these accounts, you must provide the following parameters instead.
    > 
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    > 
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    Setup.exe /silent /AcceptEndUserLicenseAgreement 
    /recover 
    /EnableErrorReporting:[Never|Queued|Always]
    /SendCEIPReports:[0|1]
    /UseMicrosoftUpdate:[0|1]
    /DatabaseName:<OperationalDatabaseName> 
    /SqlServerInstance:<server\instance> 
    /DWDatabaseName:<DWDatabaseName>
    /DWSqlServerInstance:<server\instance>
    /UseLocalSystemDASAccount 
    /DatareaderUser:<domain\username> 
    /DatareaderPassword:<password> 
    /DataWriterUser:<domain\username> 
    /DataWriterPassword:<password>
    /ActionAccountUser:<domain\username>
    /ActionAccountPassword:<password>
    ```

    Setup detects that the server was a prior management server in the management group, and recovers the management server. You must follow these procedures for each failed management server in your management group.

For information about the command\-line parameters, see [Disaster Recovery Command\-line Parameters](assetId:///44e73962-2711-41ec-aabb-2a4baf7e0a3e).

If you have to recover a management server when all management servers in the management group have failed, then you must also reconfigure the RunAs Accounts.

> [!IMPORTANT]
> If you have management servers that have not failed, you should not reconfigure the RunAs Accounts.

#### To Reconfigure the RunAs Accounts

1.  In the Operations console, click the **Administration** button.

2.  In the **Administration** pane, under **Run As Configuration**, click **Accounts**.

3.  In the **Accounts** pane, right\-click a Run As account, and then click **Properties**.

4.  In the **Run As Account Properties** dialog box, click the **Credentials** tab.

5.  Re\-enter your credentials for the Run As account and click OK.

6.  Repeat these steps for all Run As accounts.

    > [!NOTE]
    > If you are not using SQL Server authentication, you can remove any associations to the **Data Warehouse SQL Server Authentication Account** and **Reporting SDK SQL Server Authentication Account** and then delete these accounts.

If you are not using SQL Server authentication, you can remove the SQL Server Authentication accounts.

#### To Remove the SQL Server Authentication Accounts

1.  In the Operations console, click the **Administration** button.

2.  In the **Administration** pane, under **Run As Configuration**, click **Profiles**.

3.  In the **Profiles** pane, right\-click **Data Warehouse SQL Server Authentication Account**, and then click **Properties**.

4.  Click **Run As Accounts** in the right pane, click **Data Warehouse SQL Server Authentication Account**, and then click **Remove**.

5.  Click **Save**, and then click **Close**.

6.  In the **Profiles** pane, right\-click **Reporting SDK SQL Server Authentication Account**, and then click Properties.

7.  Click **Run As Accounts** in the right pane, click **Reporting SDK SQL Server Authentication Account**, and then click **Remove**.

8.  Click **Save**, and then click **Close**.

9. In the **Administration** pane, under **Run As Configuration**, click **Accounts**.

10. In the **Profiles** pane, right\-click **Data Warehouse SQL Server Authentication Account**, and then click **Delete**.

11. In the **Profiles** pane, right\-click **Reporting SDK SQL Server Authentication Account**, and then click **Delete**.

## See Also
[Backup and Disaster Recovery in Operations Manager](assetId:///4348e46d-1119-40ff-baed-b1075c1190ca)
[Disaster Recovery Command\-line Parameters](assetId:///44e73962-2711-41ec-aabb-2a4baf7e0a3e)


