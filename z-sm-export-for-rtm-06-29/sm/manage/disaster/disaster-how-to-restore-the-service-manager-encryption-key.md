---
title: How to Restore the Service Manager Encryption Key
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a117356d-ba50-49ec-b41b-d7771bccc973
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Restore the Service Manager Encryption Key
You can use the following procedure to restore the encryption keys before you run Setup.exe to restore a part of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
### To restore the encryption key  
  
1.  Log on to the computer that will host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] part that you are attempting to recover by using an account that is a member of the Administrators group. For example, log on to the computer that will host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse management servers.  
  
2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  
  
3.  Right\-click **SecureStorageBackup.exe** then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  
  
    > [!NOTE]  
    >  In this release, the wizard contains references to “Operations Manager.” This issue will be resolved in a future release.  
  
4.  On the **Introduction** page, click **Next**.  
  
5.  On the **Backup or Restore?** page, select **Restore the Encryption Key**, and then click **Next**.  
  
6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the server MyServer in the Backup shared folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  
  
7.  On the **Provide a Password** page, type the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, reenter the same password, and then click **Next**.  
  
8.  After you receive the message, “Secure Storage Key Restore Complete,” click **Finish**.