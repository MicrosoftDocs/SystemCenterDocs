---
title: Include file
description: Include file for Validation section in Install docs.
author: jyothisuri
ms.author: jsuri
ms.date:  03/19/2025
ms.topic:  include
ms.service: system-center
ms.subservice: virtual-machine-manager
---

## Installer validation (recommended) 

After you download the installation media (zip), we recommend verifying that the file isn't corrupted. Following is the checksum for the file:

::: moniker range="sc-vmm-2025"
```
223CE90811799223DA635EC66F81302ECBB3AB4842C37002AC29B23D556F5AAF
```
::: moniker-end

::: moniker range="sc-vmm-2022"
```
DA06F77E74F5D21A1824EA846F6A0C34EC0E7FC2826FF3ABB97E0874A602EB8D
```
::: moniker-end

::: moniker range="sc-vmm-2019"
```
92ED26AA920D260AF7C7EFF0E974B8B8062263728F0D62A507896B92B96EE31A
```
::: moniker-end

To verify its authenticity, perform checksum validation on your computer by running the following PowerShell snippet:

```powershell
$expectedChecksum = "ENTER_EXPECTED_HASH_HERE"
$zipFilePath = "ENTER_ZIP_Path\<product>_<version>.zip"
$expectedChecksum -eq (Get-FileHash -Path $zipFilePath -Algorithm SHA256).Hash
```

When validation passes, you see **True** printed. If you see **False** printed, the downloaded file isn't valid and you need to download it again.