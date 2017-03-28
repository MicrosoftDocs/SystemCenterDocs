---
title: Complete Service Manager deployment by backing up the encryption key
description: After you deploy Service Manager, you should back up the encryption key to help prepare for disaster recovery.
manager:  carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dbb276a9-7df5-4cd9-ae75-9099aabcaa93
---

# Complete Service Manager deployment by backing up the encryption key

>Applies To: System Center 2016 - Service Manager

When you deployed your System Center - Service Manager management server and database, an encryption key was created so that data between the Service Manager and data warehouse management servers and their associated databases could be encrypted. When you deployed the Self-Service Portal, an encryption key was created so that data between the Self-Service Portal and the Service Manager database could be encrypted.  

Your disaster recovery strategy depends on you backing up the encryption keys as soon as you complete the Service Manager installation. After you back up the encryption keys and store them in a safe location, you can recover from software or hardware failures on the Service Manager management servers, data warehouse management servers, and Self-Service Portal.  

Use the Encryption Key Backup or Restore Wizard and the following procedures to back up and restore encryption keys on the Service Manager management servers and Self-Service Portal. This wizard is located on the Service Manager installation media in the Tools\\SecureStorageBackup folder.  

### To back up the encryption key  

1.  Log on to the computer that hosts the Service Manager management server, data warehouse management server, or Self-Service Portal by using an account that is a member of the Administrators group.  

2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  

3.  Right\-click **SecureStorageBackup.exe**, and then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  

4.  On the **Introduction** page, click **Next**.  

5.  On the **Backup or Restore?** page, select **Backup the Encryption Key**, and then click **Next**.  

6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin as the encryption key and save the key on the server MyServer in the Backup folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  

7.  On the **Provide a Password** page, type a password that contains at least eight characters in the **Password** box. In the **Confirm Password** box, re\-enter the same password, and then click **Next**.  

    > [!NOTE]  
    >  Recovery of the password is not possible if it is lost or forgotten.  

8.  After you receive the message "Secure Storage Backup Complete," click **Finish**.  

### To restore the encryption key  

1.  Log on to the computer that hosts the Service Manager management server, data warehouse management server, or Self-Service Portal by using an account that is a member of the Administrators group.  

2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  

3.  Right\-click **SecureStorageBackup.exe**, and then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  

4.  On the **Introduction** page, click **Next**.  

5.  On the **Backup or Restore?** page, select **Restore the Encryption Key**, and then click **Next**.  

6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key and save the key on the server MyServer in the Backup folder share, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  

7.  On the **Provide a Password** page, type the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, re\-enter the same password, and then click **Next**.  

8.  After you receive the message, **Secure Storage Key Restore Complete**, click **Finish**.

## Next steps

- Review [Index non-English knowledge articles](deploy-indexing-non-english-knowledge-articles.md) to resolve an indexing issue in an environment where you create, or plan to create, knowledge articles in any language other than English.
