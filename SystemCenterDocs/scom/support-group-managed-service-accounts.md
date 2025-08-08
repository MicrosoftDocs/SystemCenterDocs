---
ms.assetid: a13cf51e-e6f0-4446-b00c-bf7516426d4f  
title: Support for group managed service accounts in System Center Operations Manager
description: This article details the group managed service accounts feature, supported in System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.service: system-center
monikerRange: '>=sc-om-2019'
ms.subservice: operations-manager
ms.topic: concept-article
ms.custom: UpdateFrequency3, engagement-fy24
---

# Support for group managed service accounts

::: moniker range="sc-om-2019"

Operations Manager 2019 UR1 and later supports group managed service accounts (gMSA). This article details the accounts used for gMSA and the procedures involved with gMSA support.

>[!NOTE]
> This article is applicable for Operations Manager 2019 UR1 and later.
> The article provides information on how to use gMSA in operations manager, and doesn't include information on how to create these. For information on how to create gMSA accounts, see [gMSA accounts](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

::: moniker-end

::: moniker range=">=sc-om-2022"

Operations Manager supports group managed service accounts (gMSA). This article details the accounts used for gMSA and the procedures involved with gMSA support.

>[!NOTE]
>The article provides information on how to use gMSA in operations manager, and doesn't include information on how to create these. For information on how to create gMSA accounts, see [gMSA accounts](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

::: moniker-end

## Accounts used for gMSA

Currently, the Operations Manager uses the following accounts and services:

  - Action Accounts
      - Default Action account-management server Action account
      - Agent Action account
      - GW Server Action account
      - Run as accounts
  - System Center Configuration Service and System Center Data Access Service (needs to be a part of local administrators group).
  - Data Reader account (for SSRS) must be a member of Operations Manager Report Security Administrators group.
  - Data Warehouse Write account (for DW) must be a member of Operations Manager Report Security Administrators group.
  - Agent Installation account
      - MSAA, by default, needs admin rights on the target computers.

>[!Note]
>[Group Managed Service Accounts (gMSAs)](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) are not supported as a SQL report server service account for Data reader account.

To use gMSA, administrators must do the following:

**Verify if managed service accounts can be used on the computer**

Run the following PowerShell command for each gMSA account. If it returns **True**, then gMSA is ready to be used on the management server you selected.

```powershell
Test-ADServiceAccount <gMSA_name>
```

## Next steps

To use gMSA, do the following:

- [Provide security rights](provide-security-rights.md)

- [Change databases](database-changes.md)

- [Service level account changes](service-level-changes.md)

- [Console level changes](console-level-changes.md)
