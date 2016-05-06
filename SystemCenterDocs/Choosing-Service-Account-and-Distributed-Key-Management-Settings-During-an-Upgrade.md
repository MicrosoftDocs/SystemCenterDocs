---
title: Choosing Service Account and Distributed Key Management Settings During an Upgrade
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8bfa1bd-b745-4bd1-ba3f-f0abe1165441
---
# Choosing Service Account and Distributed Key Management Settings During an Upgrade
This topic provides information to help you choose your service account and distributed key management settings during an upgrade of [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] from [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] to [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)].

During the upgrade, on the **Configure service account and distributed key management** page, you need to specify which account to use for the System Center Virtual Machine Manager service, and whether to use distributed key management to store encryption keys in Active Directory Domain Services \(AD DS\). You need to choose your service account and distributed key management settings carefully. In some circumstances, depending on what you choose, encrypted data, such as passwords in templates and profiles, will not be available after the upgrade, and you will have to manually enter them. Information that is not retained about Virtual Machine Roles will not be available for you to enter after the upgrade.

For the service account, you can choose to use the Local System account or a domain account. In some cases, such as installing a high availability VMM management server, you must use a domain account. For more information, see [Specifying a Service Account for VMM](Specifying-a-Service-Account-for-VMM.md).

Distributed key management enables you to store encryption keys in AD DS instead of storing the encryption keys on the computer on which the VMM management server is installed. We recommend that you use distributed key management, and in some cases \(such as installing a high availability VMM management server\), you must use distributed key management. For more information, see [Configuring Distributed Key Management in VMM](Configuring-Distributed-Key-Management-in-VMM.md).

Whether encrypted data is available after the upgrade depends on the following factors:

-   The account you use to sign in when you perform the upgrade.

-   The account that the Virtual Machine Manager service is using in the current installation of VMM.

-   The account that the System Center Virtual Machine Manager service will use in the [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] installation.

The following table provides information about accounts that are used during the upgrade.

|Account used when upgrading|VMM service account in   [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)]|VMM service account in  [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)]|Not using distributed key management|Using distributed key management|
|-------------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|----------------------------------------|------------------------------------|
|Any valid administrator account|Local system|Local system|Encrypted data is preserved|Encrypted data is preserved|
|Any valid administrator account|Local system|Domain account|Encrypted data is not preserved|Encrypted data is preserved|
|Any valid administrator account|Domain account|Local system|N\/A|N\/A|
|Same domain account as the VMM service account in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)]|Domain account|Domain account|Encrypted data is preserved|Encrypted data is preserved|
|Different domain account from the VMM service account in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)]|Domain account|Domain account|Encrypted data is not preserved|Encrypted data is not preserved|

> [!NOTE]
> If the Virtual Machine Manager service in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)] is configured to use a domain account, when you upgrade to a high availability management server in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)], you must use the same domain account for the Virtual Machine Manager service. During the upgrade process, you will be required to enter the password for that domain account.
> 
> If your upgrade involves installing VMM on a different computer and using your current VMM database, encrypted data is not preserved during the upgrade unless you configured distributed key management. The benefit of using distributed key management is that the encryption keys are stored in AD DS instead of on the computer that was running [!INCLUDE[vmm12short](Token/vmm12short_md.md)] in [!INCLUDE[sc2012r2_1](Token/sc2012r2_1_md.md)]. Therefore, if you reinstall [!INCLUDE[vmm12short](Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](Token/sc_threshold_1_md.md)] on a different computer, you can access the encrypted data.


