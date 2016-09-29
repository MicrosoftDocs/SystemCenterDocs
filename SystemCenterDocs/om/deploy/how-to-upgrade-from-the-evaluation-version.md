---
title:  How to Upgrade from the Evaluation Version of Operations Manager 
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Upgrade from the Evaluation Version of Operations Manager

>Applies To: System Center 2016 - Operations Manager

The System Center 2016 – Operations Manager evaluation version expires 180 days after you install it. 

To upgrade from an evaluation version of Operations Manager to a licensed version, you must obtain a valid product key from Microsoft. For information about Operations Manager licensing, see [System Center 2016 Licensing](https://www.microsoft.com/cloud-platform/system-center-2016). 

> [!NOTE] 
> To check whether Operations Manager is licensed, in Operations console, click Help, and then click About. In the **Product version** field, it will show the version **(Retail)** after the version information.  If it shows **(Eval)**, then your installation is an evaluation version.  

## To upgrade from the evaluation version of Operations Manager to a licensed version

> [!NOTE]
> Note To use the Set-SCOMLicense cmdlet, you must use elevated permissions (Run as Administrator).

1. Open PowerShell as an administrator.
2. Load the **OperationsManager** module (import-module operationsmanager).
3. Connect to your management group (New-SCOMManagementGroupConnection).
4. Run the `Set-SCOMLicense -ProductId <yourlicensekey>` command.
5. Restart the System Center Data Access Service service on all management servers in the management group in order for the setting to take effect.  
6. To check whether the changes were made, run the following command: 
`Get-SCOMManagementGroup | ft skuforlicense, version, timeofexpiration –a`

For more information about [Set-SCOMLicense](https://technet.microsoft.com/library/hh920237.aspx), type the following in the Operations Manager Command Shell:

`get-help Set-SCOMLicense`

For current information about your license, you can use the [Get-SCOMLicense](https://technet.microsoft.com/library/hh920216.aspx) cmdlet. For more information, type the following in the Operations Manager Command Shell:

`get-help Get-SCOMLicense`