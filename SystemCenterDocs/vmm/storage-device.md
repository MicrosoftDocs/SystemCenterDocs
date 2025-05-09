---
ms.assetid: 41d863fe-2888-466c-891c-43e2e57ae0c6
title: Add storage devices to the VMM fabric
description: This article describes how to discover storage devices in the VMM fabric
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 05/09/2025
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Add storage devices to the VMM fabric


To manage storage in System Center Virtual Machine Manager (VMM), you discover and add it to the VMM storage fabric.

## Before you start

Ensure that the storage device is supported before you add it.

## Add a storage device

1. Select **Fabric** > **Storage** > **Add Resources** >**Storage Devices**.
2. In **Add Storage Devices Wizard** > **Select Provider Type**, select to add a storage device with SMI-S or SMP according to the device you're using.
3. In **Specify Discovery Scope**:
    - If you're using SMI-S, specify whether the provider uses **SMI-S CIMXML** or **SMI-S WMI WMI**, add the IP address/FQDN and add the port used to connect to the provider on the remote server. You can enable SSL if you're using CIMXML. Specify an account for connecting to the provider.
    - If you're using SMP, select the provider from the list. If it isn't in the list, select **Import** to refresh it.

::: moniker range="<=sc-vmm-2019"

   >[!Important]
   >For enhanced security, we recommend you to
     >- use a Secure Sockets Layer (SSL) connection for adding storage devices in the VMM fabric. If you have added storage devices without using SSL connection, you can remove and re-add them. 
     >- keep the `EnableHTTPListenerClientCertificateCheck` enabled on the VMM server machine.
     
::: moniker-end

::: moniker range=">=sc-vmm-2022"

   >[!Important]
   >For enhanced security, we recommend you to
     >- use a Secure Sockets Layer (SSL) connection for adding storage devices in the VMM fabric. If you have added storage devices without using SSL connection, you can remove and re-add them. 
     >- keep the `EnableHTTPListenerClientCertificateCheck` key enabled in the registry under **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows/CurrentVersion/Storage Management/** on the VMM server machine.

::: moniker-end


4. In **Gather Information**, VMM automatically tries to discover and import the storage device information. To retry, select **Scan Provider**.

::: moniker range="<=sc-vmm-2019"

5. If you selected the option to use an SSL connection for an SMI-S provider, you observe that:
    - During discovery, the **Import Certificate** dialog appears. Check settings and select **Import**. By default, the certificate common name (CN) will be verified. This might cause storage discovery to fail if there's no CN or if it doesn't match.
    - If discovery fails because of the CN, disable CN verification in the registry on the VMM server. In the registry, go to **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Storage Management/** and create a new DWORD value - **DisableHttpsCommonNameCheck**. Set the value to 1.

::: moniker-end

::: moniker range=">=sc-vmm-2022"

5. If you selected the option to use an SSL connection for an SMI-S provider, you observe that:
    - During discovery, the **Import Certificate** dialog appears. Check settings and select **Import**. By default, the certificate common name (CN) will be verified. This might cause storage discovery to fail if there's no CN or if it doesn't match.
    - If discovery fails because of the CN, disable CN verification in the registry on the VMM server. In the registry, go to **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows/CurrentVersion/Storage Management/** and create a new DWORD value - **DisableHttpsCommonNameCheck**. Set the value to 1.

::: moniker-end

6. If the discovery process succeeds, the discovered storage arrays, storage pools, manufacturer, model, and capacity are listed on the page. When the process finishes, select **Next**.
7. In **Select Storage Devices**, you can specify a classification for each storage pool. Storage classifications group storage pools with similar characteristics together so that you can assign a classification as storage for a host or cluster rather than a specific storage device. [Learn more](storage-classification.md) about setting up classifications.
8. On the **Summary** page, confirm the settings, and then select **Finish**. The **Jobs** dialog appears. When the status is **Completed**, you can verify the storage in **Fabric** > **Storage**.

## Next steps

[Allocate storage to host groups](storage-host-group.md).
