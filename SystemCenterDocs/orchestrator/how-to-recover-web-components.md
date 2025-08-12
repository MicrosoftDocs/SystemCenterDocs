---
title: How to Recover Web Components
description: Describes how to recover web components after restoring a System Center - Orchestrator environment.
ms.custom: UpdateFrequency2, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: edc3c49a-93e9-4ec4-81e3-c454b54ae976
author: jyothisuri
ms.author: jsuri
---

# Recover web components

When you use the Database Configuration utility to modify the Orchestrator database, the tool won't modify the Web Service database reference (only the installer performs this task). You will need to manually modify it after updating with the database configuration utility.  

## Modify the Web Service database reference  

Follow these steps to modify the Web Service database reference:

::: moniker range="<=sc-orch-2019"
1. Open a Command Prompt using **Run as administrator**.  
2. Execute the following command \(assuming the default installation path\):  

    ```powershell
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pdf "connectionStrings" "C:\Program Files (x86)\Microsoft System Center 2016\Orchestrator\Web Service\Orchestrator2016"  
    ```  
3. Open IIS Manager and navigate to the Orchestrator2016 virtual application.  
4. Open up Connection Strings and then modify OrchestratorContext. Locate the segment that starts with `provider=System.Data.SqlClient;provider connection string` and then modify the Data Source and Initial Catalog attributes according to your new SQL Server and Database Catalog name respectively, and then select **OK**.  
5. If you want to re-encrypt the connection strings, you can execute the following command at the command prompt:  

    ```powershell
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pef "connectionStrings" "C:\Program Files (x86)\Microsoft System Center 2016\Orchestrator\Web Service\Orchestrator2016"  
    ```  
::: moniker-end

::: moniker range=">=sc-orch-2022"
1. Open the installation location of the WebAPI; typically it's `<OrchestratorInstallDir>\WebApi`.
    - You can use IIS Manager to navigate to the WebAPI folder as well.
2. Edit the `environmentVariable` element in `system.webServer` \> `aspNetCore` \> `environmentVariables` in the `web.config` using a text editor. Particularly, you'd want to change the values of the `DATABASE__*` variables. 

The full list of Database connection settings is available in [Connection String syntax][db-conn-string]. First determine the keys you need to specify for your scenario, for example the `Trusted_Connection` (or its alias `Integrated Security`) may require other keys like `User ID`.

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
> You must use two underscores to separate the `Database` prefix.

[db-conn-string]: /dotnet/api/system.data.sqlclient.sqlconnection.connectionstring#remarks

::: moniker-end

## Next steps

To learn more about the Orchestrator Web components, see [Orchestrator Overview](learn-about-orchestrator.md).
