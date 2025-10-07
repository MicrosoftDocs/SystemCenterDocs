---
title: Modify the Orchestrator database
description: Describes how to change the database location in a System Center - Orchestrator environment.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom:
  - UpdateFrequency2
  - engagement-fy23
  - sfi-ropc-nochange
---

# Modify the Orchestrator database

You might have to change the location of the Orchestrator database after installation, because you might want to separate the management server and database server, move the database to a larger server or a cluster, or just reconfigure the orchestration database based on required changes in your environment. You can use standard Microsoft SQL Server methods to move the existing database to another server, but then you must configure the Orchestrator features to connect to the new server. You must perform this configuration for the management server, the web service supporting the Orchestration console, and each runbook server as described in the following procedures.  

## Management server and runbook servers  

You can use the Database Configuration utility to change the connection settings that the management server and runbook servers installed in your environment. The settings for these servers are stored in an encrypted file called **Settings.dat**. If you change your orchestration database settings, such as the port, user account access, or computer name, you must manually uninstall and reinstall all runbook servers, and then re-run the Database Configuration utility on the management server and all runbook servers.  

### Change the database settings for the management server and runbook servers  

Follow these steps to change the database settings for the management server and runbook servers:

1. On the management server, select **Start**, point to **All Programs**, select **Microsoft System Center \<version\>**, select **Orchestrator**, and then select **Data Store Configuration**.  
2. In the **Server** box, enter the name of the server that is hosting the database by using the format **\<server\>\\<instance\>,\<port\>**. You can select the ellipsis button **(...)** to select the computer. You don't have to include the instance if the Orchestrator database is installed on the default instance. You don't have to include the port if the SQL Server is usually installed on the default port 1433.  

   If the Orchestrator database is installed on an instance called MyInstance on a computer named MySQLServer that is configured on port 12345, enter **MySQLServer\\MyInstance,12345**.  

   If the Orchestrator database is installed on an instance called MyInstance on a computer named MySQLServer that is configured on port 1433, enter **MySQLServer\\MyInstance**.  

   If the orchestration database is installed on the default instance on a computer named MySQLServer that is configured on port 1433, enter **MySQLServer**.  
3. Select the authentication method to use to connect to the SQL Server:  

   - **Windows Authentication** Connect to the SQL Server by using Windows Authentication.  

   - **SQL Server Authentication** Connect to the SQL Server by using a SQL Server user account. Enter the **User Name** and **Password** of the SQL Server user account. This account must have the rights to create, write, and own a database and create, update, and delete rows in the database.  
4. Select **Next**.  
5. In the **Data Store** pane, select **Use an existing database**.  
6. In the **Name** list, select the database.  
7. Select **Finish**.  

## Web Service  

The web service supporting the Orchestration console doesn't use the **Settings.dat** file. To change the database settings for the web service, you must modify the `web.config` file on the Internet Information Services (IIS) server.

::: moniker range="<=sc-orch-2019"
You can use **IIS Manager** to modify the file, but you must first decrypt it by running the aspnet\_regiis.exe executable file.
::: moniker-end  

### Change the database settings for the Orchestrator web service  

Follow these steps to change the database settings for the Orchestrator web service:

::: moniker range="<=sc-orch-2019"
1. Sign in with administrative credentials to the computer with the Orchestration console installed.  
2. Open a Command Prompt window with administrator credentials.  
3. Run the following command to decrypt the Web.config file:  

    ```powershell
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet\_regiis.exe -pdf "connectionStrings" "C:\Program Files (x86)\Microsoft System Center\Orchestrator\Web Service\Orchestrator"
    ```

4. To start the IIS Manager, select **Start**, point to **Administrative Tools**, and then select **Internet Information Services \(IIS\) Manager**.  
5. Expand the **Sites** node, and then select **Microsoft System Center \<version\> Orchestrator Web Service**.  
6. In the **Features View**, double-click **Connection Strings**.  
7. In the **Connections String** pane, double-click **OrchestratorContext**.  
8. In the **Custom** box, scroll down to the portion of the string that includes the server name (Data Source) and database name (Initial Catalog). Modify these values as required.  
9. Select **OK** to close the dialog.  
10. Close **IIS Manager**.  
11. Run the following command to encrypt the Web.config file:  

    ```powershell
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet\_regiis.exe -pef "connectionStrings" "C:\Program Files (x86)\Microsoft System Center\Orchestrator\Web Service\Orchestrator"
    ```
::: moniker-end

::: moniker range=">=sc-orch-2022"
Edit the `environmentVariable` element in `system.webServer` \> `aspNetCore` \> `environmentVariables` in the `web.config` using a text editor. Particularly, you'd want to change the values of the `DATABASE__*` variables.

The full list of Database connection settings is available in [Connection String syntax][db-conn-string]. First determine the keys you need to specify for your scenario; for example, the `Trusted_Connection` (or its alias `Integrated Security`) may require other keys like `User ID`.

```xml
<!-- system.webServer > aspNetCore -->
<environmentVariables>
  <environmentVariable name="Database__Database" value="Orchestrator" />
  <environmentVariable name="Database__Trusted_Connection" value="true" />
  <environmentVariable name="Database__Address" value="localhost\mssqlserver" />
</environmentVariables>
```

To set a value for a key called `property`, set an environment variable named `Database__<property>`.

> [!NOTE]
> You must use **two** underscores to separate the `Database` prefix.

[db-conn-string]: /dotnet/api/system.data.sqlclient.sqlconnection.connectionstring#remarks
::: moniker-end

## Next steps

- Read more about best practices for [database sizing and performance](database-sizing-and-performance.md).
- Get an overview of [Orchestrator architecture](learn-about-orchestrator.md).  
