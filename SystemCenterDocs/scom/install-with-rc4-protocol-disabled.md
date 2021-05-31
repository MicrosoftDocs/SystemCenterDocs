---
ms.assetid: 0497e546-7da7-4342-a427-4a9488ae6c7a
title: Install Operations Manager with RC4 protocol disabled
description: This article describes Operations Manager installation with RC4 protocol disabled
author: v-anesh
manager: evansma
ms.author: v-anesh
ms.date: 05/27/2021
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to disable RC4 while installing Operations Manager?

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

This article describes Operations Manager installation with disabled RC4 protocol and is in line with Microsoft's Security Advisory to disable RC4. For more information on the security advisory, see [MSRC Blog](https://msrc-blog.microsoft.com/2013/11/12/security-advisory-2868725-recommendation-to-disable-rc4/).

When you install Operations Manager in a security hardened environment, the set up tends to fail at the account configuration step if the appropriate permissions are not configured properly.

## Important information

In a disabled RC4 environment, when you try to install Operations Manager 2016 or 2019, you cannot pass the Account Validation stage if the steps in the Before you Begin section are not implemented, and you will see the following error in the Operations Manager set up.

![Error in operations manager set up](./media/protocol-disabled/operations-manager-setup.png)


Operations Manager internally uses a Windows Security API as part of its credential validation process and the requested encryption type is not supported by the KDC. The client and service should support same type of encryption for communication.

When a service ticket is requested, the domain controller selects the ticket encryption type based on the **msDS-SupportedEncryptionTypes** attribute of the account associated with the requested SPN.

By default, user accounts do not have a value set, unless you have manually enabled AES on them, tickets for service accounts are encrypted with RC4. For more information, see [Decrypting the Selection of Supported Kerberos Encryption Types - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/decrypting-the-selection-of-supported-kerberos-encryption-types/ba-p/1628797).

## Before you begin

Before you begin, implement the steps in the section below.

### Configure the encryption types allowed for Kerberos

For information about how to configure the encryption types allowed for Kerberos, see [Network security Configure encryption types allowed for Kerberos - Windows security | Microsoft Docs](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-configure-encryption-types-allowed-for-kerberos).

In an environment which has RC4 disabled, ensure the following steps are implemented:

1. The user account used to install Operations Manager has **AES Attributes** enabled on the **Domain Controller**.

   ![AES Attributes enabled on the Domain Controller](./media/protocol-disabled/domain-controller.png)


AES Encryption type is allowed for Kerberos on the computer where Management Server needs to be installed.

   ![AES encryption type](./media/protocol-disabled/aes-encryption-type.png)


> [!NOTE]
> If the Agent and Management Server are in different domains from the same forest (Child/Parent domain). Follow [Method 3: Configure the trust to support AES128 and AES 256 encryption instead of RC4 encryption](https://docs.microsoft.com/troubleshoot/windows-server/windows-security/unsupported-etype-error-accessing-trusted-domain).


## Disable RC4 in Operations Manager

To disable RC4 in an Operations Manager Management Server, follow these steps:

1. On the Management Server, go to **Local Group Policy Editor** > **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **Security Options** > **Network security: Configure encryption types allowed for Kerberos** > **Disable RC4**.

   ![Disable RC4](./media/protocol-disabled/disable-rc4.png)

2. Run a `gpupdate /force` command in an elevated command prompt to ensure that the changes are done.

## Install Operation manager

Install operations manager using the following information:

- [Install Operations Manager on a Single Server](quickstart-install-single-server.md)

- [Install Operations Manager from the Command Prompt](install-using-cmdline.md)
