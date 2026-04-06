---
ms.assetid: 9b7c1978-eae4-469b-bb11-06f5dc213bc0  
title: Provide security rights for gMSA in System Center Operations Manager
description: This article provides information on how to provide security rights to group manages service accounts (gMSA), a new feature supported in System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 365-days
ms.date: 11/01/2024
ms.service: system-center
monikerRange: '>=sc-om-2019'
ms.subservice: operations-manager
ms.topic: how-to
ms.custom: UpdateFrequency2
---


# Provide security rights

This article provides information on how to provide security rights to group Managed Service Accounts (gMSA). For more information, see [accounts used for gMSA](support-group-managed-service-accounts.md).

::: moniker range="sc-om-2019"

>[!NOTE]
>This article is applicable for Operations Manager 2019 Update Rollup 1 (UR1) and later.

::: moniker-end

## Provide *Log on as a service* right

To provide *log on as a service* right to gMSA accounts, follow these steps:

1. Open the *Local Security Policy* MMC snap-in. Or you can open a run box and enter: `secpol.msc`
2. Go to **Local Policies**>**User Rights Assignment**
3. Double-click **Log on as a service** job under **Policy**.
4. Add the gMSAs to the list of accounts that are allowed to log on as a service.

    Here are the account details:

    - **SMX\momActGMSA$**: Management Server Action account

    - **SMX\momDASGMSA$**: Data Access Service account (SDK)

    - **SMX\momDWGMSA$**: Data Warehouse Write account

    - **SMX\momRepGMSA$**: Data Warehouse Read account

        ![Screenshot of Log-on Service properties.](media/gmsa/logon-service-properties.png)

## Provide *Log on as a batch* right

To grant *log on as a batch right* to Data Writer and Data Reader gMSAs, follow these steps:

1. Open the *Local Security Policy* MMC snap-in. Or you can open a run box and enter: `secpol.msc`
2. Go to **Local Policies**>**User Rights Assignment**
3. Select **Log on as a batch** under **Policy**.  
4. Add the gMSAs to the list of accounts that are allowed to log on as a batch.

    ![Screenshot of log on as a batch.](media/gmsa/batch-job-properties.png)

## Generate security audits

Provide permissions to the gMSA SDK account if you wish to generate auditing events. Follow these steps:

1. Open the *Local Security Policy* MMC snap-in. Or you can open a run box and enter: `secpol.msc`
2. Go to **Local Policies**>**User Rights Assignment**
3. Double-click **Generate security audits** under **Policy**.
4. Add the gMSAs to the list of accounts that are allowed to generate security audits.

    ![Screenshot of Generate Security Audits.](media/gmsa/generate-security-audit-properties.png)

## Next step

After you've provided the required access rights, [change the databases](database-changes.md).
