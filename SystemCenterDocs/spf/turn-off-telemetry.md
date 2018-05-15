---
ms.assetid: f08056ae-d899-464c-9746-052833dfe2dd
title: Turn off telemetry settings in Service Provider Foundation
description: This article provides information about how to turn off the telemetry settings in System Center Service Provider Foundation
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  05/09/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: service-provider-foundation
---

# Turn off telemetry settings in Service Provider Foundation

This article provides information about how to turn off the telemetry settings in System Center - Service Provider Foundation (SPF).

By default, SPF sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time.


> [!NOTE]

> Microsoft does not collect any personal data from the customers. We only listen to events that would help diagnostics in SMA. [Learn more](#telemetry-data-collected).


## Turn off telemetry in SPF

Use the following procedure:

1. On the SPF server, Set the value of the "DiagnosticAndUsageDataEnabled" registry subkey under *HKEY_LOCAL_MACHINE\Software\Microsoft\Service Provider Foundation* to 0. If the registry key is not present, then create the key with the name *DiagnosticAndUsageDataEnabled* and set the value to 0.

  - To create a new Registry Key, under HKEY_LOCAL_MACHINE\Software\Microsoft\Service Provider Foundation,  right-click and select **New** > **DWORD (32-bit) Value** as shown below:

  ![spf telemetry new key ](./media/telemetry/spf-telemetry-newkey.png)

  - Enter the name of the key as *DiagnosticAndUsageDataEnabled*.

  - Once the key appears in the list of keys double-click on the key and enter 0 in the *Value data* field as shown below:

  ![spf telemetry key value](./media/telemetry/spf-telemetry-keyvaluedata.png)

2. Use the *Set-SCSpfTelemetry* command and set the telemetry option as shown in the following image:

  ![spf telemetry](./media/telemetry/spf-telemetrydisabled.png)  

## Next steps
