---
title: Include file
description: Include file for Validation section in Install docs.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  03/19/2025
ms.topic:  include
ms.service: system-center
ms.subservice: operations-manager
---

## Installer validation (recommended) 

After you download the installation media (zip), we recommend verifying that the file isn't corrupted. Following is the checksum for the file:

::: moniker range="sc-om-2025"
```
EAB2EB4A877857E44420759512682A153AFBBD80A169752CCD9B0DB8A9C0D1C2
```
::: moniker-end

::: moniker range="sc-om-2022"
```
77E84740E2D7BD893227627616CC048B5BC1EF939F734D326EB654CADE8E5C0C
```
::: moniker-end

::: moniker range="sc-om-2019"
```
5562D148315D8208F15CACE00F33C6A9820AF1EA3CAAA9CD2144973B4548B8C9
```
::: moniker-end

To verify its authenticity, perform checksum validation on your computer by running the following PowerShell snippet:

```powershell
$expectedChecksum = "ENTER_EXPECTED_HASH_HERE"
$zipFilePath = "ENTER_ZIP_Path\<product>_<version>.zip"
$expectedChecksum -eq (Get-FileHash -Path $zipFilePath -Algorithm SHA256).Hash
```

When validation passes, you see **True** printed. If you see **False** printed, the downloaded file isn't valid and you need to download it again.