---
title: Include file
description: Include file for Validation section in Install docs.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  03/19/2025
ms.topic:  include
ms.service: system-center
ms.subservice: data-protection-manager
---

## Installer Validation (optional) 

After you download the installation media (zip), we recommend verifying that the file isn't corrupted. Following is the checksum for the file:

::: moniker range="sc-dpm-2025"

```
149737D812D674D655A879E8A59481F665504448146B78ED8FD2C9B36A17B9F4
```

::: moniker-end

::: moniker range="sc-dpm-2022"

```
2C47B45CD3A9F21379FED7A8AE5CF0BE5CAB4A39B219129F6AE0A5EDB25BFB78
```

::: moniker-end

::: moniker range="sc-dpm-2019"

```
5D6045D14645DB56282CF33F99F753AF591ED846E2E37B7BC54F76ABA73A885A
```

::: moniker-end

To verify its authenticity, perform checksum validation on your computer by running the following PowerShell snippet:

```powershell
$expectedChecksum = "ENTER_EXPECTED_HASH_HERE"
$zipFilePath = "ENTER_ZIP_Path\<product>_<version>.zip"
$expectedChecksum -eq (Get-FileHash -Path $zipFilePath -Algorithm SHA256).Hash
```

When validation passes, you see **True** printed. If you see **False** printed, the downloaded file isn't valid and you need to download it again.
