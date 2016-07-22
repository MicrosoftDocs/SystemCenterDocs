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


















---
# How to Restore the Service Manager Encryption Key
You can use the following procedure to restore the encryption keys before you run Setup.exe to restore a part of System Center 2012 - Service Manager.  
  
### To restore the encryption key  
  
1.  Log on to the computer that will host the Service Manager part that you are attempting to recover by using an account that is a member of the Administrators group. For example, log on to the computer that will host the Service Manager or data warehouse management servers.  
  
2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  
  
3.  Right\-click **SecureStorageBackup.exe** then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  
  
    > [!NOTE]  
    >  In this release, the wizard contains references to "Operations Manager." This issue will be resolved in a future release.  
  
4.  On the **Introduction** page, click **Next**.  
  
5.  On the **Backup or Restore?** page, select **Restore the Encryption Key**, and then click **Next**.  
  
6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the server MyServer in the Backup shared folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  
  
7.  On the **Provide a Password** page, type the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, reenter the same password, and then click **Next**.  
  
8.  After you receive the message, "Secure Storage Key Restore Complete," click **Finish**.
