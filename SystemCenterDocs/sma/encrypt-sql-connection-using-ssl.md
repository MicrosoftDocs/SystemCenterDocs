---
ms.assetid: ba58d433-17ea-4ddc-af8d-42748ad2d349
title: Encrypt SMA web service to SQL connection by using SSL
description: This article provides information about how to encrypt SMA web service to SQL connection by using SSL.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  12/23/2020
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: service-management-automation-(sma)
---

# Encrypt SMA network traffic

::: moniker range=">= sc-sma-1801 <= sc-sma-1807"

[!INCLUDE [eos-notes-service-management-automation.md](../includes/eos-notes-service-management-automation.md)]

::: moniker-end

This article provides information about how to encrypt SMA Web Service to SQL connection by using Secure Socket Layer (SSL) and encrypt the network traffic between runbook worker and SQL database.

## Encrypt SMA web service connection using SSL

Use the following procedure:

1.	Open an elevated PowerShell console.
2.	Navigate to your .NET Framework home directory (for example, C:\Windows\Microsoft.NET\Framework64\v4.0.30319).
3.	Decrypt the config file section using the following command:

    ```powershell
    .\aspnet_regiis.exe -pdf "connectionStrings" 'C:\inetpub\Service Management Automation'
    ```
    ![Decrypt config file](./media/encrypt-sma-web-service/decrypt-config-file.png)

4.	Open the web.config file in Notepad from the path **C:\inet\Service Management Automation** and append the Connection String with **“;encrypt=true;trustServerCertificate=true”** as shown below:

    ![Append connection](./media/encrypt-sma-web-service/append-connection.png)

5.	Encrypt the Config file section by running the following command:

    ```powershell
    .\aspnet_regiis.exe -pef "connectionStrings" 'C:\inetpub\Service Management Automation'
    ```
    ![Encrypt config file](./media/encrypt-sma-web-service/encrypt-config-file.png)

6.	Restart the SMA App Pool from **Computer Management**> **Service and Applications** > **Internet Information Service(IIS) Manager**.

## Encrypt the network traffic from runbooks

Secure the connection between Runbook worker and SQL server to avoid clear text display of network traffic from runbook server.


1. Navigate to the installation path of SMA and locate the `Orchestrator.Settings.config` file.

2. Add the following under the (root) `configuration` key:

  ```xml
    <configuration>
    ...
      <connectionStrings>  
        <add name="OrchestratorStoreConnectionString"
             providerName="System.Data.SqlClient"
             connectionString="<explained-below>" />
      </connectionStrings>
    ...
    </configuration>
```

3. The `connectionString` depends on your authentication settings:
   - If using Integrated Windows Authentication (without an SQL user/pass):

     `Data Source=<database-server-hostname>;Database=<SMA-database-name>;Integrated Security=True;MultipleActiveResultSets=False;Encrypt=True;`

   - If using SQL user/pass:

     `Data Source=<database-server-hostname>;Database=<SMA-database-name>;User ID=<username>;Password=<password>;MultipleActiveResultSets=False;Encrypt=True;`

     For more information, see [SqlClient Connection Strings](https://docs.microsoft.com/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).

4. Append `TrustServerCertificate=true;` to `connectionString` in case the SSL certificate is not installed on the worker computer.


### Next steps
[Manage runbooks](manage-runbooks.md)
