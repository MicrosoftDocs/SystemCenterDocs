---
ms.assetid: 8b9770b0-4700-4871-82df-158f1d8c9869
title: How to Upgrade from the Evaluation Version of Operations Manager 
description: This article describes how to upgrade from an evaluation version of Operations Manager.
author: jyothi
ms.author: magoedte
manager: carmonm
ms.date: 01/11/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# How to upgrade from the evaluation version of Operations Manager

The System Center Operations Manager evaluation version expires 180 days after you install it. 

To upgrade from an evaluation version of Operations Manager to a licensed version, you must obtain a valid product key from Microsoft. For information about Operations Manager licensing, see [System Center Licensing](https://www.microsoft.com/cloud-platform/system-center-pricing). 

> [!NOTE] 
> To check whether Operations Manager is licensed, in the Operations console, click **Help**, and then click **About**. In the **Product version** field, it will show the version **(Retail)** after the version information.  If it shows **(Eval)**, then your installation is an evaluation version.  

::: moniker range="sc-om-1801"

## To upgrade from the evaluation version of System Center Operations Manager 1801

Before proceeding, you need to be a member of the Operations Manager administrators role.

1. In the Operations console, click **Help** and then click **About**.  
2. Click **Activate** and on the **Enter Product Key** window in the **Product key** box, enter a valid product key including the dashes. Press **Continue**  to save your changes.
3. On the **Please read this license agreement**, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and then click **Accept**.

After the change is applied, the Operations console title bar will no longer show how many days are remaining for evaluation period as well as in the **About** window.  

### Upgrade after the evaluation period

If you did not activate your license for the management group before the evaluation period expires, which is 180 days, after the evaluation period has expired you will receive a notification when you open the Operations console or launch the Operations Manager command shell.  

You perform the following steps to upgrade from the evaluation period using PowerShell directly on a management server or from a remote computer that has the Operations Manager Command Shell installed.  

Before proceeding, you need to be a member of the Operations Manager administrators role to ensure this completes successfully.  

1. Open the Operations Manager Command Shell.
2. Run the `Set-SCOMLicense -ManagementServer <Server name or IP address> -ProductId <your licensekey> -Credential <PSCredential>` command.  If you do not include the `-Credential` parameter, after you enter the command, an authentication dialog box appears prompting you to enter credentials.  
3. The cmdlet asks for confirmation.  Enter `Y` to allow it to complete the action.  If the command is successful, it returns a message indicating it was licensed successfully.
4. Restart the System Center Data Access Service service on all management servers in the management group in order for the setting to take effect.  

::: moniker-end

## To upgrade from the evaluation version of System Center 2016 - Operations Manager

Before proceeding, you need to be a member of the Operations Manager administrators role, member of the computer's local Administrators group on the management server, and granted temporary membership of the sysadmin fixed server role on the SQL Server instance hosting the Operations Manager operational database to ensure this completes successfully.  

> [!NOTE]
> Note To use the Set-SCOMLicense cmdlet, you must use elevated permissions (Run as Administrator).  

1. Open PowerShell as an administrator.
2. Load the **OperationsManager** module (import-module operationsmanager).
3. Connect to your management group (New-SCOMManagementGroupConnection).
4. Run the `Set-SCOMLicense -ProductId <yourlicensekey>` command.
5. Restart the System Center Data Access Service service on all management servers in the management group in order for the setting to take effect.  
6. To check whether the changes were made, run the following command: 
`Get-SCOMManagementGroup | ft skuforlicense, version, timeofexpiration –a`

For more information about [Set-SCOMLicense](https://docs.microsoft.com/powershell/module/operationsmanager/set-scomlicense?view=systemcenter-ps-2016), type the following in the Operations Manager Command Shell:

`get-help Set-SCOMLicense`

For current information about your license, you can use the [Get-SCOMLicense](https://docs.microsoft.com/powershell/module/operationsmanager/get-scomlicense?view=systemcenter-ps-2016) cmdlet. For more information, type the following in the Operations Manager Command Shell:

`get-help Get-SCOMLicense`


