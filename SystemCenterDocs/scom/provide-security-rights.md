---
ms.assetid: 9b7c1978-eae4-469b-bb11-06f5dc213bc0  
title: Provide security rights for gMSA in System Center Operations Manager
description: This article provides information on how to provide security rights to group manages service accounts (gMSA), a new feature in System Center 2019 UR1 - Operations Manager.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 02/04/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---


# Provide security rights

This article provides information on how to provide security rights to  group Managed Service Accounts (gMSA). For more information, see [accounts used for gMSA](support-group-managed-service-accounts.md).

>[!NOTE]
>This article is applicable for System Center 2019 UR1 - Operations Manager.

## Provide *Log on as a service* right

To provide *log on as a service* right to gMSA accounts, follow these steps:


1.	Open the *Local Security Policy* MMC snap-in.
2.	Go to **Local Policies**>**User Rights Assignment**
3.	Double-click **Log on as a service** job under **Policy**.
4.	Add the gMSAs to the list of accounts that are allowed to generate security audits.

    ![Log-on Service properties](media/gmsa/logon-service-properties.png)

## Provide *Log on as a batch* right
To grant *log on as a batch right* to Data Writer and Data Reader gMSAs, follow these steps:

1.	Follow step 1 and 2 from above procedure.
2.	Select **Log on as a batch** under **Policy**.  
3.  Add the gMSAs to the list of accounts that are allowed to generate security audits.

    ![log on as a batch](media/gmsa/batch-job-properties.png)

## Generate security audits
Provide permissions to the gMSA SDK account if you wish to generate auditing events. Follow these steps:

1.	Open the *Local Security Policy* MMC snap-in.
2.	Go to **Local Policies**>**User Rights Assignment**
3.	Double-click **Generate security audits** under **Policy**.
4.	Add the gMSAs to the list of accounts that are allowed to generate security audits.

    ![Generate Security Audits](media/gmsa/generate-security-audit-properties.png)

## Next steps
After you have provided the required access rights, [change the databases](database-changes.md).
