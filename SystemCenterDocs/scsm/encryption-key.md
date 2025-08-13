---
title: Complete Service Manager Deployment by Backing Up the Encryption Key
description: After you deploy Service Manager, you should back up the encryption key to help prepare for disaster recovery.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 04/11/2025
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: dbb276a9-7df5-4cd9-ae75-9099aabcaa93
---

# Complete Service Manager deployment by backing up the encryption key



When you deployed your System Center - Service Manager management server and database, an encryption key was created so that data between the Service Manager and data warehouse management servers and their associated databases could be encrypted. When you deployed the Self-Service Portal, an encryption key was created so that data between the Self-Service Portal and the Service Manager database could be encrypted.  

Your disaster recovery strategy depends on you backing up the encryption keys as soon as you complete the Service Manager installation. After you back up the encryption keys and store them in a safe location, you can recover from software or hardware failures on the Service Manager management servers, data warehouse management servers, and Self-Service Portal.  

Use the Encryption Key Backup or Restore Wizard and the following procedures to back up and restore encryption keys on the Service Manager management servers and Self-Service Portal. This wizard is located on the Service Manager installation media in the *Tools\\SecureStorageBackup* folder.  

## Back up the encryption key  

To back up the encryption key, follow these steps:

1. Sign in to the computer that hosts the Service Manager management server, data warehouse management server, or Self-Service Portal by using an account that is a member of the Administrators group.  

2. In Windows Explorer, open the *Tools\\SecureStorageBackup* folder on the installation media.  

3. Right\-click **SecureStorageBackup.exe**, and select **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  

4. On the **Introduction** page, select **Next**.  

5. On the **Backup or Restore?** page, select **Backup the Encryption Key**, and select **Next**.  

6. On the **Provide a Location** page, enter the path and file name for the encryption key. 
     For example, if you want to specify the file name `SMBackupkey.bin` as the encryption key and save the key on the server MyServer in the Backup folder, enter **\\\\MyServer\\Backup\\SMBackupkey.bin**, and select **Next**.  

7. On the **Provide a Password** page, enter a password that contains at least eight characters in the **Password** box. In the **Confirm Password** box, re-enter the same password, and select **Next**.  

    > [!NOTE]  
    > Recovery of the password isn't possible if it's lost or forgotten.  

8. After you receive the message **Secure Storage Backup Complete**, select **Finish**.  

## Restore the encryption key  

To restore the encryption key, follow these steps:

1. Sign in to the computer that hosts the Service Manager management server, data warehouse management server, or Self-Service Portal by using an account that is a member of the Administrators group.  

2. In Windows Explorer, open the *Tools\\SecureStorageBackup* folder on the installation media.  

3. Right-click **SecureStorageBackup.exe**, and select **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  

4. On the **Introduction** page, select **Next**.  

5. On the **Backup or Restore?** page, select **Restore the Encryption Key**, and select **Next**.

6. On the **Provide a Location** page, enter the path and file name for the encryption key. 
     For example, if you want to specify the file name SMBackupkey.bin for the encryption key and save the key on the server MyServer in the Backup folder share, enter **\\\\MyServer\\Backup\\SMBackupkey.bin**, and select **Next**.  

7. On the **Provide a Password** page, enter the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, re-enter the same password, and select **Next**.  

8. After you receive the message, **Secure Storage Key Restore Complete**, select **Finish**.

## Next steps

To resolve an indexing issue in an environment where you create, or plan to create, knowledge articles in any language other than English, review [Index non-English knowledge articles](non-eng-articles.md).
