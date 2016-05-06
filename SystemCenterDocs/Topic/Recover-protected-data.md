---
title: Recover protected data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 951d9dcf-9b98-4b59-98b5-9b6b89bbd59a
---
# Recover protected data
Loss of data is an unwanted event for any organization. [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] helps mitigate such losses by providing you with the ability to recover backed up data. To enable data recovery, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] creates recovery points \(previous versions\) of your protected data in accordance with settings you specify in the policy for a protection group. A recovery point, also referred to as a snapshot, is a point\-in\-time copy of a replica stored on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server. A replica is a complete point\-in\-time copy of the protected shares, folders, and files for a single volume on a protected computer. When you start protecting data, an initial full replica of the data is copied to the allocated replica volume.

You can browse through the recovery points to find, select, and recover previous versions of your protected data. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] provides search and browse features that help you find the data that you need to recover. After you find the data, you can recover the version you find, or you can display a list of all available versions so that you can select a specific version to recover. Recovered data can be from any workloads you protect using [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] — client computer or server data, files, applications, or workloads such as SQL Server, SharePoint, Hyper\-V, or Exchange.

It takes only a few minutes to find data, select a version, and start a recovery job or recovery collection \(multiple jobs\). Depending on the size of data being recovered, the job can take less than a minute or it could take hours. You can check the status of recovery jobs in the **Monitoring** task area.

## In this section
[Work with recovery points](../Topic/Work-with-recovery-points.md)

[Find recoverable data](../Topic/Find-recoverable-data.md)

[Recover client computer data \[TO DELETE\]](assetId:///ba1d7ab2-41f9-4c2e-b2dd-5e5cfb4af9ab)

[Recover system state or BMR](../Topic/Recover-system-state-or-BMR.md)

[Recover virtual machine data \[TO DELETE\]](assetId:///f4b0b4c4-ac5f-44f8-b66e-575a9b3d38fc)

[Recover backed up data \[DPM2012\_Web\]](assetId:///d755b1e4-ac20-4ee3-92d5-5c0cf028f87d)

[Recover SharePoint data \[TO DELETE\]](assetId:///6ee4cb68-5e6d-4d85-9f18-f1a1cd434221)

[Recover Exchange data](assetId:///68cf7c59-b7da-4e69-999a-99689c08d8eb)

[Recover SQL Server data \[TO DELETE\]](assetId:///8df7bffc-b96d-4906-8664-4d539d01cd9f)

[Recover Hyper\-V data \[TO DELETE\]](assetId:///673b31ee-24a2-41cc-90af-dcbba319f89b)

