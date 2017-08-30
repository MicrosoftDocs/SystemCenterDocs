---
ms.assetid: dbd26196-14f8-4593-9e4b-5c54ac4edb45
title:  How to Install an Operations Manager Management Server
description: This article describes how to install an Operations Manager management server. 
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 08/30/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to install an Operations Manager management server

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, the first feature you install is the management server. The setup procedure creates the operational database and data warehouse database. The procedure described in this topic assumes that you have already installed a supported version of Microsoft SQL Server.  If you are hosting the Operations Manager operational and data warehouse database on a SQL Always On Availability Group, be sure to use the node planned for the initial Primary replica for initial installation of these databases.  

You must ensure that your server meets the minimum system requirements for System Center 2016 - Operations Manager. For more information, see [System Requirements for System Center 2016 - Operations Manager](plan-system-requirements.md).

Once you have installed the first management server and created the management group, you can follow the steps for installing an additional management server if you are planning to include additional management servers to provide high availability and increased capacity for your monitoring workloads.  

### To install the first management server in the management group

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select the **Management server** feature. You can also select any of the additional features listed. For example, to also install the Operations console, select **Operations console**. To read more about each feature and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default value of **C:\Program Files\System Center 2016\Operations Manager**. Or, type a new location or browse to one, and then click **Next**.

5.  On the **Prerequisites** page, review and resolve any warnings or errors, and then click **Verify Prerequisites Again** to recheck the system.

    > [!IMPORTANT]
    > You might receive a message that indicates that ASP.NET 4 is not registered with Internet Information Services (IIS). To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command:
    >
    > **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r**

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Specify an installation option** page, select **Create the first Management server in a new management group**, type a name for your management group, and then click **Next**.

    > [!NOTE]
    > After the management group name is set, it cannot be changed. The Management Group name cannot contain the following characters:, ( ) ^ ~ : ; . ! ? " , ' ` @ # % \ / * + = $ | & [ ] <>{}, and it cannot have a leading or trailing space. It is recommended that the Management Group name be unique within your organization if you plan to connect several management groups together.

8.  On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and then click **Next**.

9. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, type the name of the server and the name of the SQL Server instance for the database server that will host the operational database. 

  * If you installed SQL Server by using the default instance, you only have to type the server name. 
  * If you changed the default SQL Server port, you must type the new port number in the **SQL Server port** box.  
  * If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  
  * If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener and for **SQL Server port**, type the port number of the availability group listener.    

    As you type the values for the SQL Server and instance names, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values have not yet been validated, and the black text indicates that you have not entered any illegal characters. If you enter illegal characters, the text itself turns red.

    The white **X** appears under the following circumstances:

    -   You entered an instance of SQL Server or a SQL Server port value that is not valid or that does not exist.

    -   The instance of SQL Server that you specified does not have the required configuration or features.

    -   You entered a value that is out-of-range (for example, port 999999).

    -   You entered an illegal character for that box (for example, server\instance%)

    You can hover the cursor over the **Server name and instance name** text box to view additional information about the error.

10. After you type the correct value for the SQL Server database server name, click the **SQL Server port** box so that Setup will attempt to validate the values you typed for the SQL Server name and for the port number.

11. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Click **Next**.

    > [!NOTE]
    > These paths do not change if you connect to a different instance of SQL Server.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the <path\> placeholder with the location of SQL Server.
    >
    > **mofcomp.exe \<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof**

    > [!NOTE]
    > The SQL Server model database size must not be greater than 100 MB. If it is, you might encounter an error in Setup regarding the inability to create a database on SQL due to user permissions. To resolve the issue, you must reduce the size of the model database.

12. When the **Configuration**, **Configure the data warehouse database** page opens, in the **Server name and instance name** box, type the server name and the name of the instance of SQL Server for the database server that will host the data warehouse database.   

  * If you installed SQL Server by using the default instance, you only have to type the server name. 
  * If you changed the default SQL Server port, you must type the new port number in the **SQL Server port** box.  
  * If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  
  * If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener and for **SQL Server port**, type the port number of the availability group listener.    

13. Because this is the first management server installation, accept the default value of **Create a new data warehouse database**.

14. In the **Database name**, **Database size (MB)**, **Data file folder**, and **Log file folder** boxes, we recommend that you accept the default values. Click **Next**.

    > [!IMPORTANT]
    > You might receive a message about having the wrong version of SQL Server, or you might encounter a problem with the SQL Server Windows Management Instrumentation (WMI) provider. To resolve this problem, open a Command Prompt window, select **Run as administrator**, and then run the following command. In the command, replace the <path\> placeholder with the location of SQL Server.
    >
    > **mofcomp.exe \<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof**

    > [!NOTE]
    > These paths do not change if you connect to a different instance of SQL Server.

15. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for the **Management server action account**, the **System Center Configuration service and System Center Data Access service** account, the **Data Reader account**, and the **Data Writer account**. None of them should have domain administrator credentials. Click **Next**.

16. On the **Configuration**, **Diagnostic and Usage Data** page, review the information and then click **Next**. 

17. If Windows Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

18. Review the options on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

19. When Setup is finished, the **Setup is complete** page appears. Click **Close**.

20. Open the Operations console.

21. In the Operations console, in the navigation pane, click the **Administration** button, and then expand **Device Management**.

22. In **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you just installed with a green check mark in the **Health State** column.

### To install additional management servers in the management group

Perform the following steps to add additional management servers in your management group.

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select the **Management server** feature. You can also select any of the additional features listed. For example, to also install the Operations console, select **Operations console**. To read more about each feature and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default value of **C:\Program Files\System Center 2016\Operations Manager**. Or, type a new location or browse to one, and then click **Next**.

5. On the **Configuration, Specify an installation option** page, select **Add a Management server to an existing management group**, and then click **Next**.

6.  On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and then click **Next**.

7. When the **Configuration**, **Configure the operational database** page opens, in the **Server name and instance name** box, type the name of the server and the name of the SQL Server instance for the database server that will host the operational database. 

  * If you installed SQL Server by using the default instance, you only have to type the server name. 
  * If you changed the default SQL Server port, you must type the new port number in the **SQL Server port** box.  
  * If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  
  * If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener and for **SQL Server port**, type the port number of the availability group listener.    

    As you type the values for the SQL Server and instance names, you see a red circle with a white **X** in it appear to the left of the **Server name and instance name** and **SQL Server port** boxes. The white **X** indicates that the values have not yet been validated, and the black text indicates that you have not entered any illegal characters. If you enter illegal characters, the text itself turns red.

    The white **X** appears under the following circumstances:

    -   You entered an instance of SQL Server or a SQL Server port value that is not valid or that does not exist.

    -   The instance of SQL Server that you specified does not have the required configuration or features.

    -   You entered a value that is out-of-range (for example, port 999999).

    -   You entered an illegal character for that box (for example, server\instance%)

    You can hover the cursor over the **Server name and instance name** text box to view additional information about the error.

8. After you type the correct value for the SQL Server database server name, click the **SQL Server port** box so that Setup will attempt to validate the values you typed for the SQL Server name and for the port number.

9. Select the database name from the **Database name** drop-down list, and then click **Next**.  

10. On the **Configuration**, **Configure Operations Manager accounts** page, we recommend that you use the **Domain Account** option for the **Management server action account** and the **System Center Configuration service and System Center Data Access service** account. None of them should have domain administrator credentials. Click **Next**.

    > [!IMPORTANT]
    > You must provide the same credentials for the Management server action account and the System Center Configuration Service and System Center Data Access service that you provided when you created the first management server in your management group.
    >

11. On the **Configuration**, **Diagnostic and Usage Data** page, review the information and then click **Next**. 

12. If Windows Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

13. Review the options on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

14. When Setup is finished, the **Setup is complete** page appears. Click **Close**.

15. On a computer with the Operations console installed, sign on with an account that is a member of the Operations Manager Administrators group and launch the Operations console.

16. In the Operations console, in the navigation pane, click the **Administration** button, and then expand **Device Management**.

17. In **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you just installed with a green check mark in the **Health State** column.  

## To install the first management server in the management group from the Command Prompt 

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

    > [!NOTE]
    > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account (`/UseLocalSystemActionAccount`) and Data Access service (`/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead.
    >
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    >
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    setup.exe /silent /install /components:OMServer
    /ManagementGroupName: "<ManagementGroupName>"
    /SqlServerInstance: <server\instance or Always On availability group listener>
    /SqlInstancePort: <SQL instance port number>
    /DatabaseName: <OperationalDatabaseName>
    /DWSqlServerInstance: <server\instance or Always On availability group listener>
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

## To install additional management servers in the management group from the Command Prompt

1.  Log on to the server by using an account that has local administrative credentials.

2.  Open the Command Prompt window by using the **Run as Administrator** option.

    > [!NOTE]
    > Setup.exe requires administrator privileges because the Setup process requires access to system processes that can only be used by a local administrator.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > The following command assumes that you specified the Local System for the Management server action account (`/UseLocalSystemActionAccount`) and Data Access service (`/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead.
    >
    > `/ActionAccountUser: <domain\username> /ActionAccountPassword: <password>`
    >
    > `/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

    ```
    setup.exe /silent /install /components:OMServer
    /SqlServerInstance: <server\instance or Always On availability group listener>
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

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
