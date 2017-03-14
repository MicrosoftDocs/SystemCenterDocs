---
title: Process all dimensions in the data warehouse using cmdlets
description: Describes how you can process all dimensions in the Service Manager data warehouse using cmdlets.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: c235b610-c86e-443e-bb4d-337eead6febd
---

# Process all dimensions in the Service Manager data warehouse using cmdlets

>Applies To: System Center 2016 - Service Manager

You can process all the dimensions in the data warehouse in one operation using Windows PowerShell cmdlets, instead of processing each dimension individually. On the server that hosts SQL Server Analysis Services (SSAS), use the following Windows PowerShell script. Be sure to specify the fully qualified server name. You can type each command separately, or you can save them all as a Windows PowerShell script (.ps1) file and then run the script.

Before you can use Service Manager cmdlets, you need to configure the Service Manager Shell. For information about configuring the Service Manager Shell, see [Configuring and Using the System Center 2016 - Service Manager Cmdlets for Windows PowerShell](admin-configuring-and-using-the-system-center-2016-service-manager-cmdlets-for-windows-powershell.md).

### To process all dimensions using cmdlets

- Copy and paste the following code snippets at the prompt in a Service Manager Shell:

    ```
    [System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices") > $NULL
    ```

    ```
    $Server = New-Object Microsoft.AnalysisServices.Server
    $Server.Connect("<FullyQualifiedServerName>")
    $Databases = $Server.Databases
    $DWASDB = $Databases["DWASDataBase"]
    $Dimensions = New-Object Microsoft.AnalysisServices.Dimension
    $Dimensions = $DWASDB.Dimensions
    ```

    ```
    foreach ($Dimension in $Dimensions){$Dimension.Process("ProcessFull")}
    ```
