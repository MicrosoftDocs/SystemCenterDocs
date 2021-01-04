---
title: "PGP Decrypt File | Microsoft Docs"
ms.custom: ""
ms.date: 05/07/2019
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf1b4f0c-2694-405b-9940-1fdb88c9228b
caps.latest.revision: 16
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# PGP Decrypt File

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The PGP Decrypt File activity decrypts a file or entire folder tree using a PGP key file and passphrase that you have created. When decrypting an entire folder, the folder tree is preserved from the root folder down. For example, if you decrypt C:\Documents and Settings\Administrator\My Documents\\\*.\* and all subfolders, all files in My Documents are decrypted as well as all the files in the folders under My Documents. All files in subfolders will be in the same subfolder in the Output folder.  

You can use the PGP Decrypt File activity to decrypt files that were encrypted as part of a backup operation. To use this activity, you must install the gpg executable.


## Install GnuPG

GnuPG is an open-source program used by the standard activities PGP Encrypt file and PGP Decrypt file to encrypt and decrypt files. The following procedures describe how to install this executable program and associated file on a runbook server or computer that is running the Runbook Designer.

### Install GnuPG version 1.x and 2.0.x

Use the following steps:

1.	Download gpg.exe and iconv.dll, version 1.4.10 or later, from [GnuPG](https://www.gnupg.org/).
2.	Save gpg.exe and iconv.dll to the <System drive>:\Program Files (x86)\Common Files\Microsoft System Center \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that is running the Runbook Designer.

### Install GnuPG version 2.x

Use the following steps:

1.	Download gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll, and zlib1.dll version 2.x or later from [GnuPG](https://www.gnupg.org/).

2.	Save gpg.exe, gpg-agent.exe, iconv.dll, libassuan-0.dll, libgcrypt-20.dll, libgpg-error-0.dll, libnpth-0.dll, libsqlite3-0.dll and zlib1.dll to the <System drive>:\Program Files(x86)\Common Files\<Microsoft System Center Orchestrator \<version\>\Orchestrator\Extensions\Support\Encryption folder on each runbook server and computer that is running the Runbook Designer.


## Configuring the PGP Decrypt Activity  
 Use the following information to configure the PGP Decrypt File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Path**|Type the path of the files that you want to decrypt. You can use wildcards, **?** and * to specify the files that you are decrypting. This field will only accept characters from the current system locale. If you use other characters, the activity will fail.|  
|**Include sub-directories**|Select this option to find all files that match the file name that you specified in all subdirectories under the folder that you specified in the path.|  
|**Output folder**|Type the path of the folder where you want the decrypted files to be stored.|  
|**Skip**|Select this option to skip decrypting a file when a file with the same name is found in the **Output folder**.|  
|**Overwrite**|Select this option to overwrite any files with the same name as a resulting decrypted file.|  
|**Create unique name**|Select this option to give the decrypted file a unique name if a file with the same name already exists.|  

### Advanced Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Keyring folder**|Type the location of the keyring folder that contains the secret keyring file that you will use to decrypt the files. The secret keyring file (*.skr) may be renamed with a \*.gpg extension.|  
|**Passphrase**|Type the passphrase that is associated with the keyring file.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Keyring folder|The path of Keyring folder that contains the key used to decrypt the files.|  
|Output folder|The path of the folder where the decrypted files were saved.|  
|Files to decrypt|The number of files that Orchestrator attempted to decrypt.|  
|Files decrypted|The number of files that were successfully decrypted.|  
|Decrypted filename|The path and filename of the resulting decrypted file.|
