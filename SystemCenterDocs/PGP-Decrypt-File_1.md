---
title: PGP Decrypt File_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cdaf123-27e0-4da0-bfea-98cb54189ab0
---
# PGP Decrypt File_1
The PGP Decrypt File activity decrypts a file or entire folder tree using a PGP key file and passphrase that you have created. When decrypting an entire folder, the folder tree is preserved from the root folder down. For example, if you decrypt C:\\Documents and Settings\\Administrator\\My Documents\\\*.\* and all subfolders, all files in My Documents are decrypted as well as all the files in the folders under My Documents. All files in subfolders will be in the same subfolder in the Output folder.

You can use the PGP Decrypt File activity to decrypt files that were encrypted as part of a backup operation. To use this activity you must install the Gpg executable. To install the Gpg executable, see [Install GnuPG](http://go.microsoft.com/fwlink/?LinkId=219849) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=219849\).

## Configuring the PGP Decrypt Activity
Use the following information to configure the PGP Decrypt File activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Path**|Type the path of the files that you want to decrypt. You can use wildcards ? and \* to specify the files that you are decrypting. This field will only accept characters from the current system locale. If you use other characters, the activity will fail.|
|**Include sub\-directories**|Select this option to find all files that match the file name that you specified in all sub\-directories under the folder that you specified in the path.|
|**Output folder**|Type the path of the folder where you want the decrypted files to be stored.|
|**Skip**|Select this option to skip decrypting a file when a file with the same name is found in the **Output folder**.|
|**Overwrite**|Select this option to overwrite any files with the same name as a resulting decrypted file.|
|**Create unique name**|Select this option to give the decrypted file a unique name if a file with the same name already exists.|

### Advanced Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Keyring folder**|Type the location of the keyring folder that contains the secret keyring file that you will use to decrypt the files. The secret keyring file \(\*.skr\) may be renamed with a \*.gpg extension.|
|**Passphrase**|Type the passphrase that is associated with the keyring file.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Keyring folder|The path of Keyring folder that contains the key used to decrypt the files.|
|Output folder|The path of the folder where the decrypted files were saved.|
|Files to decrypt|The number of files that Orchestrator attempted to decrypt.|
|Files decrypted|The number of files that were successfully decrypted.|
|Decrypted filename|The path and filename of the resulting decrypted file.|


