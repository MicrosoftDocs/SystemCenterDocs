---
title: PGP Encrypt File
description: This article describes the PGP Encrypt File activity.
ms.date: 11/05/2025
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 1866b4f2-8755-43d0-89a3-dbeaa948a508
caps.latest.revision: 20
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
---
# PGP Encrypt File

The PGP Encrypt File activity encrypts a file or an entire folder tree using a PGP key file that you've created. When encrypting an entire folder, the folder tree is preserved from the root folder down. For example, if you encrypt C:\Documents and Settings\Administrator\My Documents\\\*.\* and all subfolders, all files in My Documents are encrypted and also all the files in folders under My Documents. All the files that are in subfolders will be in the same subfolder in the Output folder. Use the PGP Encrypt File activity to encrypt files before backing them up.  

 To use this activity, you must install the gpg executable.

> [!IMPORTANT]
> This activity supports DSS and RSA4 keys.  
> RSA keys are not supported by this activity.  

## Install GnuPG

GnuPG is an open-source program used by the standard activities PGP Encrypt file and PGP Decrypt file to encrypt and decrypt files. The following procedures describe how to install this executable program and associated file on a runbook server or computer that is running the Runbook Designer.

### Install GnuPG version 1.x and 2.0.x

Use the following steps:

1. Download gpg.exe and iconv.dll, version 1.4.10 or later, from [GnuPG](https://www.gnupg.org/download/index.html).
2. Save gpg.exe and iconv.dll to the \<System drive\>:\Program Files (x86)\Common Files\Microsoft System Center \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that is running the Runbook Designer.

For example, 

Go to [GnuPG](https://www.gnupg.org/download/index.html), under **GNUPG BINARY RELEASES**, download Gpg4win, and installer for GnuPG.

If you download and install gnupg-w32-2.4.8_20250514.exe, *gpg.exe, gpg-agent.exe, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll* are found in `<System drive>:\Program Files\GnuPG\bin` and *iconv.dll* in Gpg4win installer file `<System drive>:\Program Files\Gpg4win\bin`.

### Install GnuPG version 2.x

Use the following steps:

1. Download gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll version 2.x or later from [GnuPG](https://www.gnupg.org/).

2. Save gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll to the \<System drive\>:\Program Files(x86)\Common Files\<Microsoft System Center Orchestrator \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that is running the Runbook Designer.

For example, 

Go to [GnuPG](https://www.gnupg.org/download/index.html), under **GNUPG BINARY RELEASES**, download Gpg4win, and installer for GnuPG.

If you download and install gnupg-w32-2.4.8_20250514.exe, *gpg.exe, gpg-agent.exe, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll* are found in `<System drive>:\Program Files\GnuPG\bin` and *iconv.dll* in Gpg4win installer file `<System drive>:\Program Files\Gpg4win\bin`.

### Install GnuPG on new Outlook

To install GnuPG on new Outlook, download Gpg4win and select **GpgOL** checkbox.

:::image type="content" source="./media/pgp-encrypt-file/install.png" alt-text="Screenshot of Install screen.":::

:::image type="content" source="./media/pgp-encrypt-file/setup.png" alt-text="Screenshot of Gpg4win-setup page.":::

## Configure the PGP Encrypt File Activity

 Before you configure the PGP Encrypt File activity, you need to determine the following:  

- The path of the files that you want to encrypt.  

- The output folder where the encrypted files will be stored.  

Use the following information to configure the PGP Encrypt File activity.  

### Details  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Path**|Enter the path of the files that you want to encrypt. You must use the full path name. You can use wildcards ? and * to specify the files that you want to encrypt. This field only accepts characters from the current system locale.|  
|**Include sub-directories**|Select this option to find all the files that match the filename that you specified in all the subfolders of the folder that you specified in the path.|  
|**Output folder**|Enter the path of the folder where you want the encrypted files to be stored.|  
|**Skip**|Select this option to skip encrypting a file when a file with the same name is found in the Output folder.|  
|**Overwrite**|Select this option to overwrite any files with the same name as the resulting encrypted file.|  
|**Create unique name**|Select this option to give the encrypted file a unique name if a file with the same name already exists.|  
|**File extension**|Enter the file name extension that you want to append to the file name when it's encrypted. The default extension is gpg.|  

### Advanced  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Key file**|Enter the location of the PGP key file that you'll use to encrypt the files. If you leave this field blank, the PGP Encrypt File activity uses the file that you specify in the **Keyring folder** field. Files can have any file name extension, but *.asc is the standard.|  
|**Keyring folder**|Enter the location of the folder that contains the keyring that you'll use to encrypt the files. The public keyring file (\*.pkr) may be renamed with a \*.gpg file name extension. **Important:** The PGP Encrypt File activity creates files in the keyring folder. The Orchestrator Runbook Service account, or the user account used to run the runbook, requires read and write permissions on the keyring folder.|  
|**User**|Enter the user name that was specified when the encryption key was created. This is a required field.|  
|**Comment**|Enter the comment that was specified when the encryption key was created. If this field was completed when the encryption key was created, you must provide this information when using this activity.|  
|**Email**|Enter the email address that was specified when the encryption key was created. This is a required field.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Key file|The path of the key file used to encrypt the files.|  
|Keyring folder|The path of keyring folder that contains the key used to encrypt the files.|  
|User|The name of the user that was used to encrypt the files.|  
|Comment|The comment that was used to encrypt the files.|  
|Email|The email address that was used to encrypt the files.|  
|Output folder|The path of the folder where the encrypted files were saved.|  
|Files to encrypt|The number of files that Orchestrator attempted to encrypt.|  
|Files encrypted|The number of files that successfully encrypted.|  
|Encrypted filename|The path of the resulting encrypted file.|
