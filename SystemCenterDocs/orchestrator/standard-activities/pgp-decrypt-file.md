---
title: PGP Decrypt File
description: This article describes the functionality of PGP Decrypt File activity.
ms.date: 10/09/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
ms.assetid: cf1b4f0c-2694-405b-9940-1fdb88c9228b
caps.latest.revision: 16
author: jyothisuri
ms.author: jsuri
---
# PGP Decrypt File

The PGP Decrypt File activity decrypts a file or entire folder tree using a PGP key file and passphrase that you've created. When decrypting an entire folder, the folder tree is preserved from the root folder down. For example, if you decrypt C:\Documents and Settings\Administrator\My Documents\\\*.\* and all subfolders, all files in My Documents are decrypted and also all the files in the folders under My Documents. All the files in subfolders will be in the same subfolder in the Output folder.  

You can use the PGP Decrypt File activity to decrypt files that were encrypted as part of a backup operation. To use this activity, you must install the gpg executable.

## Install GnuPG

GnuPG is an open-source program used by the standard activities PGP Encrypt file and PGP Decrypt file to encrypt and decrypt files. The following procedures describe how to install this executable program and associated file on a runbook server or computer that is running the Runbook Designer.

### Install GnuPG version 1.x and 2.0.x

Use the following steps:

1. Download gpg.exe and iconv.dll, version 1.4.10 or later, from [GnuPG](https://www.gnupg.org/).
2. Save gpg.exe and iconv.dll to the \<System drive\>:\Program Files (x86)\Common Files\Microsoft System Center \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that's running the Runbook Designer.

### Install GnuPG version 2.x

Use the following steps:

1. Download gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll version 2.x or later from [GnuPG](https://www.gnupg.org/).

2. Save gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll to the \<System drive\>:\Program Files(x86)\Common Files\<Microsoft System Center Orchestrator \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that is running the Runbook Designer.

### Encrypt and decrypt

To encrypt and decrypt, run the following command:
 
```PowerShell
gpg.exe -r <Public Key ID> -o <Output File Path> --encrypt <Source File Path>
gpg --list-keys
gpg --full-generate-key
gpg.exe --decrypt <Encrypted File Path>
```

## Configure the PGP Decrypt Activity

 Use the following information to configure the PGP Decrypt File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Path**|Enter the path of the files that you want to decrypt. You can use wildcards, **?** and * to specify the files that you're decrypting. This field will only accept characters from the current system locale. If you use other characters, the activity fails.|  
|**Include sub-directories**|Select this option to find all files that match the file name that you specified in all subdirectories under the folder that you specified in the path.|  
|**Output folder**|Enter the path of the folder where you want the decrypted files to be stored.|  
|**Skip**|Select this option to skip decrypting a file when a file with the same name is found in the **Output folder**.|  
|**Overwrite**|Select this option to overwrite any files with the same name as the resulting decrypted file.|  
|**Create unique name**|Select this option to give the decrypted file a unique name if a file with the same name already exists.|  

### Advanced Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Keyring folder**|Enter the location of the keyring folder that contains the secret keyring file that you use to decrypt the files. The secret keyring file (*.skr) may be renamed with a \*.gpg extension.|  
|**Passphrase**|Enter the passphrase that's associated with the keyring file.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Keyring folder|The path of Keyring folder that contains the key used to decrypt the files.|  
|Output folder|The path of the folder where the decrypted files were saved.|  
|Files to decrypt|The number of files that Orchestrator attempted to decrypt.|  
|Files decrypted|The number of files that were successfully decrypted.|  
|Decrypted filename|The path and filename of the resulting decrypted file.|
