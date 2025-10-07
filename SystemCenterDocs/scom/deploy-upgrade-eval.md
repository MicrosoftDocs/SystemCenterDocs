---
ms.assetid: 8b9770b0-4700-4871-82df-158f1d8c9869
title: Upgrade from an evaluation version of Operations Manager
description: This article describes how to upgrade from an evaluation version of Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade from the evaluation version of Operations Manager

The System Center Operations Manager evaluation version expires 180 days after you install it.

To upgrade from an evaluation version of Operations Manager to a licensed version, you must obtain a valid product key from Microsoft. For information about Operations Manager licensing, see [System Center Licensing](https://www.microsoft.com/cloud-platform/system-center-pricing).

> [!NOTE]
> To check whether Operations Manager is licensed, in the Operations console, select **Help**, and then select **About**. In the **Product version** field, it'll show the version **(Retail)** after the version information.  If it shows **(Eval)**, then your installation is an evaluation version.  

## Upgrade from the evaluation version of System Center - Operations Manager

Before proceeding, you need to be a member of the Operations Manager administrators role, member of the computer's local Administrators group on the management server, and granted temporary membership of the sysadmin fixed server role on the SQL Server instance hosting the Operations Manager operational database to ensure this completes successfully.  

> [!NOTE]
> To use the Set-SCOMLicense cmdlet, you must use elevated permissions (Run as Administrator).  

1. Open PowerShell as an administrator.
2. Load the **OperationsManager** module (import-module operationsmanager).
3. Connect to your management group (New-SCOMManagementGroupConnection).
4. Run the `Set-SCOMLicense -ProductId <yourlicensekey>` command.
5. Restart the System Center Data Access Service service on all management servers in the management group for the setting to take effect.  
6. To check whether the changes were made, run the following command:
`Get-SCOMManagementGroup | ft skuforlicense, version, timeofexpiration –a`

For more information about [Set-SCOMLicense](/powershell/module/operationsmanager/set-scomlicense), enter following in the Operations Manager Command Shell:

`get-help Set-SCOMLicense`

For current information about your license, you can use the [Get-SCOMLicense](/powershell/module/operationsmanager/get-scomlicense) cmdlet. For more information, enter the following in the Operations Manager Command Shell:

`get-help Get-SCOMLicense`

## Next steps

To understand the post-upgrade tasks to be performed once you've completed the upgrade process, see [Post-upgrade tasks when upgrading Operations Manager](deploy-upgrade-post-tasks.md).
