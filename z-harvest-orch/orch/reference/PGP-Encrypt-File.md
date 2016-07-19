---
title: PGP Encrypt File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1866b4f2-8755-43d0-89a3-dbeaa948a508
author:bwren
manager:cfreemanwa
---
# PGP Encrypt File
The PGP Encrypt File activity encrypts a file or an entire folder tree using a PGP key file that you have created. When encrypting an entire folder, the folder tree is preserved from the root folder down. For example, if you encrypt C:\\Documents and Settings\\Administrator\\My Documents\\\*.\* and all subfolders, all files in My Documents are encrypted as well as all files in folders under My Documents. All files that are in subfolders will be in the same subfolder in the Output folder. Use the PGP Encrypt File activity to encrypt files before backing them up.  
  
To use this activity you must install the Gpg executable. To install the Gpg executable, see [Install GnuPG](http://go.microsoft.com/fwlink/p/?LinkId=219849).  
  
> [!IMPORTANT]  
> This activity supports DSS and RSA4 keys.  
>   
> RSA keys are not supported by this activity.  
  
## Configuring the PGP Encrypt File Activity  
Before you configure the PGP Encrypt File activity, you need to determine the following:  
  
-   The path of the files that you want to encrypt.  
  
-   The output folder where the encrypted files will be stored.  
  
Use the following information to configure the PGP Encrypt File activity.  
  
### Details  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Path**|Type the path of the files that you want to encrypt. You must use the full path name. You can use wildcards ? and \* to specify the files that you want to encrypt. This field only accepts characters from the current system locale.|  
|**Include sub\-directories**|Select this option to find all the files that match the filename that you specified in all the subfolders of the folder that you specified in the path.|  
|**Output folder**|Type the path of the folder where you want the encrypted files to be stored.|  
|**Skip**|Select this option to skip encrypting a file when a file with the same name is found in the Output folder.|  
|**Overwrite**|Select this option to overwrite any files with same name as the resulting encrypted file.|  
|**Create unique name**|Select this option to give the encrypted file a unique name if a file with the same name already exists.|  
|**File extension**|Type the file name extension that you want to appended to the file name when it is encrypted. The default extension is gpg.|  
  
### Advanced  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Key file**|Type the location of the PGP key file that you will use to encrypt the files. If you leave this field blank, the PGP Encrypt File activity uses the file that you specify in the **Keyring folder** field. Files can have any file name extension, but \*.asc is the standard.|  
|**Keyring folder**|Type the location of the folder that contains the keyring that you will use to encrypt the files. The public keyring file \(\*.pkr\) may be renamed with a \*.gpg file name extension. **Important:** The PGP Encrypt File activity creates files in the keyring folder. The Orchestrator Runbook Service account, or the user account used to run the runbook, requires read and write permissions on the keyring folder.|  
|**User**|Type the user name that was specified when the encryption key was created. This is a required field.|  
|**Comment**|Type the comment that was specified when the encryption key was created. If this field was completed when the encryption key was created, you must provide this information when using this activity.|  
|**Email**|Type the email address that was specified when the encryption key was created. This is a required field.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Key file|The path of the key file used to encrypt the files.|  
|Keyring folder|The path of keyring folder that contains the key used to encrypt the files.|  
|User|The name of the user that was used to encrypt the files.|  
|Comment|The comment that was used to encrypt the files.|  
|Email|The email address that was used to encrypt the files.|  
|Output folder|The path of the folder where the encrypted files were saved.|  
|Files to encrypt|The number of files that Orchestrator attempted to encrypt.|  
|Files encrypted|The number of files that successfully encrypted.|  
|Encrypted filename|The path of the resulting encrypted file.|  
  
