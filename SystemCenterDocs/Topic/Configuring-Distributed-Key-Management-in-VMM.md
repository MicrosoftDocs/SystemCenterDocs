---
title: Configuring Distributed Key Management in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1238b5b8-98fc-4c2b-bdb5-253e4e1b3baa
---
# Configuring Distributed Key Management in VMM
During the installation of a [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] management server, you must decide whether to store the keys to encrypted data on the local computer or configure distributed key management. On the **Configure service account and distributed key management** page of Setup, you can select to use distributed key management to store encryption keys in Active Directory Domain Services \(AD DS\) instead of storing the encryption keys on the computer on which the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server is installed.

By default, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] encrypts some data in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database by using the Data Protection Application Programming Interface \(DPAPI\). For example, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] encrypts Run As account credentials and passwords in guest operating system profiles. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] also encrypts product key information in virtual hard disk properties for virtual machine role scenarios and configuration. The encryption of this data is tied to the specific computer on which [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] is installed and the service account that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] uses. Therefore, if you move your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] installation to another computer, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will not retain the encrypted data. In that case, you must enter this data manually to fix the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] objects.

Distributed key management, however, stores the encryption keys in AD DS. Therefore, if you must move your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] installation to another computer, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] will retain the encrypted data because the other computer will have access to the encryption keys in AD DS.

> [!IMPORTANT]
> For virtual machine roles, if the encrypted data is not retained, you will not be able to enter it manually, so you will not be able to manage the roles.

If you choose to enable distributed key management, coordinate with your AD DS administrator about creating the appropriate container in AD DS for storing the cryptographic keys.

The following are requirements and considerations for using distributed key management in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]:

-   You must create a container in AD DS before you install [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. You can create the container by using [Active Directory Service Interfaces Editor](http://technet.microsoft.com/library/cc773354.aspx#BKMK_UsingADSIEdit) \(ADSI Edit\). To install **ADSI Edit**, in **Server Manager** add the feature **AD DS Tools** under **Remote Server Administration Tools**. After installation, **ADSI Edit** is listed on the **Tools** menu in **Server Manager**.

-   You must create the container in the same domain as the user account with which you are installing [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. Also, if you specify a domain account that the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] service will use, that account must also be in the same domain.

    For example, if the installation account and the service account are both in the corp.contoso.com domain, you must create the container in that domain. So, if you want to create a container that is named **VMMDKM**, you specify the container location as `CN=VMMDKM,DC=corp,DC=contoso,DC=com`.

-   After the AD DS administrator has created the container, the account with which you are installing [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] must have Full Control permissions to the container in AD DS. Also, the permissions must apply to this object and all descendant objects of the container.

-   If you are installing a highly available [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, you must use distributed key management to store encryption keys in AD DS.

    Distributed key management is required in this scenario because when the Virtual Machine Manager service fails over to another node in the cluster, the Virtual Machine Manager service still needs access to the encryption keys in order to access data in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] database. This access is possible only if the encryption keys are stored in a central location like AD DS.

-   For future upgrades that involve virtual machine roles, we recommend that you use distributed key management during setup. This will help ensure that virtual machine roles are properly upgraded, and that you can manage them after the upgrade.

-   On the **Configure service account and distributed key management** page, you must type the location of the container in AD DS, for example:

    **CN\=VMMDKM,DC\=corp,DC\=contoso,DC\=com**

