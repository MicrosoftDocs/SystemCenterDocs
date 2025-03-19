---
title: include file
description: include file for Validation section in Install docs.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  03/19/2025
ms.topic:  include
ms.service: system-center
ms.subservice: orchestrator
---

## Installer Validation (recommended) 

After you download the installation media (zip), it is recommended to verify that the file is not corrupted. Following is the checksum for the file:

::: moniker range="sc-orch-2025"
```
52F79F65908851AB5E2EDE18DD002273C3846811BC7560795EDSFB121A1EEFB3
```
::: moniker-end

::: moniker range="sc-orch-2022"
```
8767920692157DA537284D38F8E1E9A1C8EDE94047452176AF6EA7C23AFFFC91
```
::: moniker-end

::: moniker range="sc-orch-2019"
```
7BD107535B6AB329D1D90B841C2629D2BE4014D1FB82DF030C1164A021BE9062
```
::: moniker-end

To verify its authenticity, perform checksum validation on your computer by running the following PowerShell snippet:

```powershell
$expectedChecksum = "ENTER_EXPECTED_HASH_HERE"
$zipFilePath = "ENTER_ZIP_Path\<product>_<version>.zip"
$expectedChecksum -eq (Get-FileHash -Path $zipFilePath -Algorithm SHA256).Hash
```

When validation passes, you see **True** printed. If you see **False** printed, the downloaded file is not valid and you need to download it again.