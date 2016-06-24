---
title: How to Process All Dimensions in the Data Warehouse Using Windows PowerShell Cmdlets
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c235b610-c86e-443e-bb4d-337eead6febd
---
# How to Process All Dimensions in the Data Warehouse Using Windows PowerShell Cmdlets
You can process all the dimensions in the data warehouse in one operation using Windows PowerShell cmdlets, instead of processing each dimension individually. On the server that hosts SQL Server Analysis Services (SSAS), use the following Windows PowerShell script. Be sure to specify the fully qualified server name. You can type each command separately, or you can save them all as a Windows PowerShell script (.ps1) file and then run the script.

Before you can use Service Manager cmdlets, you need to configure the Service Manager Shell. For information about configuring the Service Manager Shell, see [Configuring and Using the System Center 2016 - Service Manager Cmdlets for Windows PowerShell](Configuring-and-Using-the-System-Center-2016---Service-Manager-Cmdlets-for-Windows-PowerShell.md).

### To process all dimensions using cmdlets

1.  Copy and paste the following code snippets at the prompt in a Service Manager Shell:

    1.  ```
        [System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices") > $NULL
        ```

    2.  ```
        $Server = New-Object Microsoft.AnalysisServices.Server
        $Server.Connect("<FullyQualifiedServerName>")
        $Databases = $Server.Databases
        $DWASDB = $Databases["DWASDataBase"]
        $Dimensions = New-Object Microsoft.AnalysisServices.Dimension
        $Dimensions = $DWASDB.Dimensions

        ```

    3.  ```
        foreach ($Dimension in $Dimensions){$Dimension.Process("ProcessFull")}

        ```


