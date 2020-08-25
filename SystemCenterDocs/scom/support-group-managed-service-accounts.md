---
ms.assetid: a13cf51e-e6f0-4446-b00c-bf7516426d4f  
title: Support for group managed service accounts in System Center Operations Manager
description: This article details the group managed service accounts feature, supported in System Center Operations Manager 2019  UR1 and later..
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 08/25/2020
ms.prod: system-center
monikerRange: 'sc-om-2019'
ms.technology: operations-manager
ms.topic: article
---


# Support for group managed service accounts
Operations Manager 2019 UR1 and later supports group managed service accounts (gMSA). This article details the accounts used for gMSA, and the procedures involved with gMSA support.

>[!NOTE]
> This article is applicable for Operations Manager 2019 UR1 and later.
>The article provides information on how to use gMSA in operations manager, does not include information on how to create these. For information on how to create gMSA accounts, see [gMSA accounts](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

## Accounts used for gMSA
Currently, Operations Manager uses the following accounts and services :

  - Action Accounts
      - Default Action account-management server Action account
      - Agent Action account
      - GW Server Action account
      - Run as accounts
  - System Center Configuration Service and System Center Data Access Service (needs to be a part of local admin group)
  - Data Reader account (for SSRS)
  - Data Warehouse Write account (for DW)
  - Agent Installation account
      - MSAA by default, needs admin rights on the target computers.

To leverage gMSA, administrators need to do the following:

**Verify if managed service accounts can be used on the computer**

Run the following PowerShell command for each gMSA account. If it returns **True**, then gMSA is ready to be used on the management server you selected.

```
Test-ADServiceAccount \<gMSA\_name\>

```

## Next steps
To use gMSA, do the following:

[Provide security rights](provide-security-rights.md)

[Change databases](database-changes.md)

[Service level account changes](service-level-changes.md)

[Console level changes](console-level-changes.md)
