---
title: How to Back Up the Encryption Key in Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d10d5c2c-7930-47ba-afa2-f1256bacc442
---
# How to Back Up the Encryption Key in Service Manager
Your disaster recovery strategy for [!INCLUDE[smlong12](Token/smlong12_md.md)] depends on backing up the encryption keys as soon as you complete the [!INCLUDE[smshort](Token/smshort_md.md)] installation. After you back up the encryption keys and store them in a safe location, you can recover from software or hardware failures on the [!INCLUDE[smshort](Token/smshort_md.md)] and data warehouse management servers.

You use the Encryption Key Backup or Restore Wizard to back up encryption keys on the management servers and [!INCLUDE[smssp](Token/smssp_md.md)]. This wizard is located on the [!INCLUDE[smshort](Token/smshort_md.md)] installation media in the Tools\\SecureStorageBackup folder.

### To back up the encryption key

1.  Log on to the computer that hosts the [!INCLUDE[smshort](Token/smshort_md.md)] management server of data warehouse management server by using an account that is a member of the Administrators group.

2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.

3.  Right\-click **SecureStorageBackup.exe** then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.

4.  On the **Introduction** page, click **Next**.

5.  On the **Backup or Restore?** page, select **Backup the Encryption Key**, and then click **Next**.

6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the MyServer server in the Backup shared folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.

7.  On the **Provide a Password** page, in the **Password** box type a password that contains at least eight characters. In the **Confirm Password** box, retype the same password, and then click **Next**.

    > [!IMPORTANT]
    > Recovery of the password is not possible if the password is lost or forgotten.

8.  After you see the message “Secure Storage Backup Complete,” click **Finish**.


