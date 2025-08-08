---
ms.assetid: b6aec30b-3bd1-4e4e-a664-23faee39953a
title: Enabling debugging in Management Pack for SQL Server
description: This article explains how to enable debugging in Management Pack for SQL Server
manager: evansma
author: epomortseva
ms.author: v-fkornilov
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Debugging in SQL Server Management Pack 

In Management Pack for SQL Server, you can enable debugging in the Windows Event log in cases where you want to investigate potential issues that may occur during monitoring or see the detailed data sets used in the management pack workflows.

## Enabling Debugging

To enable debugging, do the following:

1. Open the Windows registry.

2. Create the following key:
`HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\SQL Server MP`

3. Create a Multi-String with the name `<MG Name>` that corresponds to the management group name for which you want to collect logs. Leave **Value data** empty to enable Debug logging for all SQL MP modules in the Operations Manager Event Log.

Or use the following PowerShell script to enable debugging in automated mode:

```PowerShell
$SCOMRoot = 'HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\'
$MPDebugKey = Join-Path -Path $SCOMRoot -ChildPath 'SQL Management Packs\EnableEvtLogDebugOutput\SQL Server MP'
$AgRoot = Join-Path -Path $SCOMRoot -ChildPath 'Agent Management Groups'
$SrvRoot = Join-Path -Path $SCOMRoot -ChildPath 'Server Management Groups'
$searchPath = if (Test-Path $AgRoot) { $AgRoot } else { $SrvRoot }

if (-not(Test-Path $SCOMRoot)) {
    Write-Error 'The Microsoft Operations Manager or Monitoring Agent is not installed.' -ErrorAction Stop
}

if (-not(Test-Path $MPDebugKey)) {
    New-Item -Path $MPDebugKey -Force | Out-Null
}

Get-ChildItem -Path $searchPath |
Out-GridView -OutputMode Multiple | # Remove this line if there is no need for GUI
ForEach-Object {
    New-ItemProperty -LiteralPath $MPDebugKey -Name $_.PSChildName -Value '1' -PropertyType 'MultiString' -Force | Out-Null
}
```

The same should be done for each Operations Manager or Monitoring Agent where extended logging must be enabled. You don't need to restart any service; changes are applied automatically.

## Disabling Debugging

To disable debugging, delete the keys added above or use the following PowerShell script to disable debugging in automated mode:

```PowerShell
$MPDebugKey = 'HKLM:\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\SQL Management Packs\EnableEvtLogDebugOutput\SQL Server MP'

if (-not(Test-Path $MPDebugKey)) {
    Write-Error 'The Microsoft Operations Manager or Monitoring Agent is not installed.' -ErrorAction Stop
}

(Get-Item -Path $MPDebugKey).property |
Out-GridView -OutputMode Multiple | # Remove this line if there is no need for GUI
ForEach-Object {
    Remove-ItemProperty -LiteralPath $MPDebugKey -Name $_ -Force | Out-Null
}
```

> [!NOTE]
> Currently, you can enable extended logging for all SQL MP modules only. Extended logging of separate modules isn't supported yet.
