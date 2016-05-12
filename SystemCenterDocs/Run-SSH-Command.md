---
title: Run SSH Command
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f04d8a08-3621-4d03-b231-20994b0d5c93
---
# Run SSH Command
The Run SSH Command activity opens an SSH connection to a remote server and runs shell commands on that server. Use the Run SSH Command activity to run backup applications or a batch script that runs a set of complex commands on a non\-Windows computer. The Run SSH Command activity can run any command in a Secure Shell.

Run SSH Command activity is based on PuTTY beta .61.  The implementation of SSH in "Run SSH Command" has certain limitations:

-   The Run SSH Command activity does not work against all SSH\-1 and SSH\-2 servers.  In general, this activity functions with most SSH servers, but it does not work for all SSH server implementations.

-   You must download and use the PuTTy key generation tool to create keys for the Run SSH Command activity.  The key generation tool is available at [Download PuTTY \- a free SSH and telnet client for Windows](http://go.microsoft.com/fwlink/p/?LinkID=230517).

-   The Run SSH Command activity supports SSH\-1.  Microsoft does not recommend the use of SSH\-1. If you want to prevent The Run SSH Command activity from using SSH\-1, you should use a key file that contains keys that do not support SSH\-1.  Do not use a username and password pair use a key file.

-   The property **Accept Host Key Change** is not a recommended setting.  This property should only be used to establish the initial connection to a computer when the key is stored on the runbook server.  Runbooks that contain the Run SSH Command activity should be configured with **Accept Host Key Change** disabled.  When you use this property it disables the validation of the identity of the SSH server and represents a security risk.

-   You should review the list if cryptographic ciphers supported by PuTTY, which is found at [Encryption algorithm selection](http://go.microsoft.com/fwlink/p/?LinkId=235054).

-   PuTTY beta .61 uses a pseudorandom number generator suitable for most cryptographic purposes. It is not recommended for the generation of long\-term cryptographic keys.

For more information about PuTTY, go to [Download PuTTY \- a free SSH and telnet client for Windows](http://go.microsoft.com/fwlink/p/?LinkID=230517).

## Configuring the Run SSH Command Activity
Before you configure the Run SSH Command activity, you need to determine the following:

-   Connection information for the computer that hosts the SSH server that you want to connect to.

-   Commands that you want to run.

-   Whether you require a key file to log into the server before you are able to run commands; this depends on your SSH server.

Use the following information to configure the Run SSH Command activity.

### Details

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Computer**|Type the name of the computer or IP address where the SSH server is running. You can also use the ellipsis **\(...\)** button to browse for the computer.|
|**Port**|Type the port number that you need to use to connect to the SSH server.|
|**Run Command**|Select this option and type the command that you want to run on the SSH server after the connection has been established.|
|**Command Set File**|Select this option and specify a file that contains a set of commands that will be run on the SSH server when the connection has been established. The command set file must use the scripting language of the native shell on the SSH server.|
|**Accept Host Key Change**|Select this option to accept host key changes when they occur. **Security Note:** It is recommended that you do not use this setting because it can cause a runbook to accept any change in a server, including any that are for  malicious purposes.  By selecting this option, you are instructing the activity to connect to any server, regardless of the host key.  Only use this option for testing purposes.|
|**Connection Timeout**|Specify the amount of time, in seconds, that the Run SSH Command activity will wait for the SSH command to complete. Configure a value of **0** \(zero\), or leave the box blank, to wait indefinitely.<br /><br />After the timeout period has elapsed, the Run SSH Command activity times out and returns a warning. The command that you ran may continue running, regardless of whether the Run SSH Command activity times out.|

### Advanced

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Username**|Type the username that you need to log into the SSH server.|
|**Password**|Select this option and type the password that is associated with the Username that you specified.|
|**Key File**|Select this option to specify a key file to use. You must use the PuTTY key file generator to create a key file. You can download this tool from [Download PuTTY \- a free SSH and telnet client for Windows](http://go.microsoft.com/fwlink/p/?LinkID=230517).|
|**Passphrase**|Type the passphrase that is associated with the key file that you specified.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Command|The command that ran on the SSH server. This data is not available when the **Command Set File** option is selected.|
|Command Set file|The command set file that was used to run commands on the SSH server. This option is not available when the **Run Command** option is selected.|
|Computer name|The name or IP address of the SSH server.|
|Execution Result|The text that was published as output from the commands that were run on the SSH server.|
|Exit Code|The exit code published by the command. When using a command set file, this will be the exit code of the last command in the file.|
|Key file path|The path of the key file that was used to authenticate with the SSH server.|
|Port|The port used to connect to the SSH server.|
|Username|The username used to log into the SSH server.|


