---
ms.assetid: 41d863fe-2888-466c-891c-43e2e57ae0c6
title: Add storage devices to the VMM fabric
description: This article describes how to discover storage devices in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Add storage devices to the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

To manage storage in System Center 2016 - Virtual Machine Manager (VMM), you discover and add it to the VMM storage fabric.

## Before you start

Make sure that the storage device is supported before you add it.

## Add a storage device

1.  Click **Fabric** > **Storage** > **Add Resources** >**Storage Devices**.
2.  In  **Add Storage Devices Wizard** > **Select Provider Type**, select to add a storage device with SMI-S or SMP, according to the device you're using.
3.  In **Specify Discovery Scope**:

	- If you're using SMI-S, specify whether the provider uses **SMI-S CIMXML** or **SMI-S WMI WMI**, add the IP address/FQDN, and add the port used to connect to the provider on the remote server. You can enable SSL if you're using CIMXML. Then specify an account for connecting to the provider.
	- If you're using SMP, select the provider from the list. If it isn't in the list click **Import** to refresh it.

4.  In **Gather Information**, VMM automatically tries to discover and import the storage device information. To retry click **Scan Provider**.
5.  If you selected the option to use an SSL connection for an SMI-S provider, note that:

	- During discovery, the **Import Certificate** dialog box appears. Check settings and click **Import**. By default the certificate common name (CN) will be verified. This might cause storage discovery to fail if there's no CN, or it doesn't match.
	- If discovery fails because of the CN, disable CN verification in the registry on the VMM server. In the registry go to **HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Storage Management/** and create a new DWORD value - **DisableHttpsCommonNameCheck**. Set the value to 1.

6.  If the discovery process succeeds, the discovered storage arrays, storage pools, manufacturer, model, and capacity are listed on the page. When the process finishes, click **Next**.
7.  In **Select Storage Devices**, you can specify a classification for each storage pool. Storage classifications group storage pools with similar characteristics together so that you can assign a classification as storage for a host or cluster, rather than a specific storage device. Learn more about setting up classifications.
8.  On the **Summary** page, confirm the settings, and then click **Finish**. The **Jobs** dialog box appears. When status is **Completed** you can verify the storage in **Fabric** > **Storage**.

## Next steps

[Allocate storage to host groups](storage-host-group.md)
