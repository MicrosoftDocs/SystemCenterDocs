---
title: How to Recover Web Components
description: Describes how to recover web components after restoring a System Center 2016 - Orchestrator environment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edc3c49a-93e9-4ec4-81e3-c454b54ae976
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# How to recover web components

> Applies To: System Center 2016 - Orchestrator

When you use the Database Configuration utility to modify the Orchestrator database, the tool will not modify the Web Service database reference \(only the installer performs this task\). You will need to manually modify it after updating with the database configuration utility.  

To do this, you will need to complete the following actions:  

### To modify the Web Service database reference  

1.  Open a Command Prompt using **Run as administrator**.  
2.  Execute the following command \(assuming the default installation path\):  

    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pdf "connectionStrings" "C:\Program Files (x86)\Microsoft System Center 2016\Orchestrator\Web Service\Orchestrator2016"  
    ```  
3.  Open IIS Manager and navigate to the Orchestrator2016 virtual application.  
4.  Open up Connection Strings and then modify OrchestratorContext. Locate the segment that starts with "provider\=System.Data.SqlClient;provider connection string" and then modify the Data Source and Initial Catalog attributes according to your new SQL Server and Database Catalog name respectively, then click OK.  
5.  If you want to re\-encrypt the connection strings, you can execute the following command at the command prompt:  

    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe -pef "connectionStrings" "C:\Program Files (x86)\Microsoft System Center 2016\Orchestrator\Web Service\Orchestrator2016"  
    ```  

## Next steps
To learn more about the Orchestrator Web components read [Orchestrator Overview](learn-about-orchestrator.md)  