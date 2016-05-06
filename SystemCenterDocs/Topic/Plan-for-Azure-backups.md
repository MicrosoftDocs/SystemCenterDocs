---
title: Plan for Azure backups
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6dbbc896-8517-4853-85d4-bc1ce9125624
---
# Plan for Azure backups
You can back up protected DPM data to Azure using Azure Backup. When you set up a protection group in DPM you select disk for short\-term storage and then you can select to backup data online. To plan for online Azure Backup note the following

-   Only some workloads and file types can be backed up to Azure. For details see [Prerequisites for DPM backup to Azure](http://go.microsoft.com/fwlink/?LinkId=524065).

-   Make sure you have all the Azure and DPM deployment requirements in place. See [Prerequisites for DPM backup to Azure](http://go.microsoft.com/fwlink/?LinkId=524065).

-   You’ll need to have Azure Backup set up before you can select to back up protection group data online. This includes creating a Backup vault under an Azure subscription, installing the Azure Recovery Services Agent on the DPM server, and registering the DPM server in the vault. For instructions, see [Configure a Backup vault and register the DPM server](http://go.microsoft.com/fwlink/?LinkId=524066).

-   When you back up a protection group to Azure you can retain data for up to 3360 days. In Azure Backup each backup is stored as a recovery point. The maximum amount of recovery points is 120 for daily synchronization, but you can create a less granular backup policy.

    |Synchronize every x weeks|Maximum retention algorithm|Maximum retention \(days\)|
    |-----------------------------|-------------------------------|------------------------------|
    |1|120 x7 x 1|840|
    |2|120 x 7 x 2|1680|
    |3|120 x 7 x 3|2520|
    |4|120 x 7 x 4|3360|

