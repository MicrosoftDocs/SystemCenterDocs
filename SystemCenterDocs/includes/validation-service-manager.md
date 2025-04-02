---
title: Include file
description: Include file for Validation section in Install docs.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  03/19/2025
ms.topic:  include
ms.service: system-center
ms.subservice: service-manager
---

## Installer validation (recommended) 

After you download the installation media (zip), we recommend verifying that the file isn't corrupted. Following is the checksum for the file:

::: moniker range="sc-sm-2025"

```
3001D0F19CFC8E1881B8D77E3251B81FB21E7A59C027CB4EB7663435068D41B1
```

::: moniker-end

::: moniker range="sc-sm-2022"

```
667802FC1FA8545065AFBC06A28BAE4015B54528B6A9E5A80201C908E082D198
```

::: moniker-end

::: moniker range="sc-sm-2019"

```
223870FB43CA8B584040401BBE7FEDE9D90A066A391ABD39F3D7948BBD0FE4A1
```

::: moniker-end

To verify its authenticity, perform checksum validation on your computer by running the following PowerShell snippet:

```powershell
$expectedChecksum = "ENTER_EXPECTED_HASH_HERE"
$zipFilePath = "ENTER_ZIP_Path\<product>_<version>.zip"
$expectedChecksum -eq (Get-FileHash -Path $zipFilePath -Algorithm SHA256).Hash
```

When validation passes, you see **True** printed. If you see **False** printed, the downloaded file isn't valid and you need to download it again.
