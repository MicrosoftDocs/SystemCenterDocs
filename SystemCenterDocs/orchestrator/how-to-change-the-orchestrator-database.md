---
title: How to Change the Orchestrator Database
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acf45816-d68e-4ad5-ac9c-f29eb8254d5b
author: cfreemanwa
ms.author: cfreeman
ms.date: 10/12/2016
manager: cfreeman
---
# How to Change the Orchestrator Database

> Applies To: System Center 2016 - Orchestrator

You might have to change the location of the Orchestrator database after installation, because you might want to separate the management server and database server, move the database to a larger server or a cluster, or just reconfigure the orchestration database based on required changes in your environment. You can use standard Microsoft SQL Server methods to move the existing database to another server, but then you must configure the Orchestrator features to connect to the new server. You must perform this configuration for the management server, the web service supporting the Orchestration console, and each runbook server as described in the following procedures.  

## Management server and runbook servers  
You can use the Database Configuration utility to change the connection settings that the management server and runbook servers installed in your environment. The settings for these servers are stored in an encrypted file called **Settings.dat**. If you change your orchestration database settings, such as the port, user account access, or computer name, you must manually uninstall and reinstall all runbook servers, and then re\-run the Database Configuration utility on the management server and all runbook servers.  

#### To change the database settings for the management server and runbook servers  

1.  On the management server, click **Start**, point to **All Programs**, click **Microsoft System Center 2016**, click **Orchestrator**, and then click **Data Store Configuration**.  

2.  In the **Server** box, enter the name of the server that is hosting the database by using the format **<server>\\<instance>,<port>**. You can click the ellipsis **\(...\)** button to select the computer. You do not have to include the instance if the Orchestrator database is installed on the default instance. You do not have to include the port if SQL Server is usually installed on the default port 1433.  

    If the Orchestrator database is installed on an instance called MyInstance on a computer named MySQLServer that is configured on port 12345, enter **MySQLServer\\MyInstance,12345**.  

    If the Orchestrator database is installed on an instance called MyInstance on a computer named MySQLServer that is configured on port 1433, enter **MySQLServer\\MyInstance**.  

    If the orchestration database is installed on the default instance on a computer named MySQLServer that is configured on port 1433, enter **MySQLServer**.  

3.  Select the authentication method to use to connect to the SQL Server:  

    -   **Windows Authentication** Connect to the SQL Server by using Windows Authentication.  

    -   **SQL Server Authentication** Connect to the SQL Server by using a SQL Server user account. Type the **User Name** and **Password** of the SQL Server user account. This account must have rights to create, write, and own a database and create, update, and delete rows in the database.  

4.  Click **Next**.  

5.  In the **Data Store** pane, click **Use an existing database**.  

6.  In the **Name** list, select the database.  

7.  Click **Finish**.  

## Web Service  
The web service supporting the Orchestration console does not use the **Settings.dat** file. To change the database settings for the web service, you must modify the Web.config file on the Internet Information Services \(IIS\) server. You can use **IIS Manager** to modify the file, but you must first decrypt it by running the aspnet\_regiis.exe executable file.  

#### To change the database settings for the Orchestrator web service  

1.  Log on with administrative credentials to the computer with the Orchestration console installed.  

2.  Open a Command Prompt window with administrator credentials.  

3.  Run the following command to decrypt the Web.config file:  

    **C:\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\aspnet\_regiis.exe \-pdf "connectionStrings" "C:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Web Service\\Orchestrator2016"**  

4.  To start the IIS Manager, click **Start**, point to **Administrative Tools**, and then click **Internet Information Services \(IIS\) Manager**.  

5.  Expand the **Sites** node, and then click **Microsoft System Center 2016 Orchestrator Web Service**.  

6.  In the **Features View**, double\-click **Connection Strings**.  

7.  In the **Connections String** pane, double\-click **OrchestratorContext**.  

8.  In the **Custom** box, scroll down to the portion of the string that includes the server name \(Data Source\) and database name \(Initial Catalog\). Modify these values as required.  

9. Click **OK** to close the dialog box.  

10. Close **IIS Manager**.  

11. Run the following command to encrypt the Web.config file:  

    **C:\\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\aspnet\_regiis.exe \-pef "connectionStrings" "C:\\Program Files \(x86\)\\Microsoft System Center 2016\\Orchestrator\\Web Service\\Orchestrator2016"**  

## See Also  
[Administering System Center 2016 - Orchestrator](../orch/manage/administering-orchestrator.md)  
