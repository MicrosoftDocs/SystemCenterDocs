---
title: How to Configure sudo Elevation and SSH Keys
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-09-22
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Configure sudo Elevation and SSH Keys

With System Center 2016 - Operations Manager, you can provide credentials for an unprivileged account to be elevated on a UNIX or Linux computer by using the sudo program, which allows users to run programs that have the security privileges of another user account. You can also use Secure Shell \(SSH\) keys instead of a password for secure communication between Operations Manager and the targeted computer.  
  
This topic provides examples for creating an account for a low\-privileged user, implementing sudo, and creating an SSH key on a computer that is running Red Hat Enterprise Linux Server 6. These are examples only, and might not reflect your environment. The following examples provide a user with access to a full set of privileges.  
  
To obtain and configure the SSH key from the UNIX and Linux computer, you have to install the following software on your Windows\-based computer:  
  
-   A file transfer tool, such as WinSCP, to transfer files from the UNIX or Linux computer to the Windows\-based computer.  
  
-   The PuTTY program, or a similar program, to run commands on the UNIX or Linux computer.  
  
-   The PuTTYgen program to save the private SHH key in OpenSSH format on the Windows\-based computer.  
  
> [!NOTE]  
> The sudo program exists at different locations on UNIX and Linux operating systems. To provide uniform access to sudo, the UNIX and Linux agent installation script creates the symbolic link `/etc/opt/microsoft/scx/conf/sudodir` to point to the directory expected to contain the sudo program. The agent uses this symbolic link to invoke sudo. The installation script automatically creates the symbolic link, so you do not need to take any action on standard UNIX and Linux configurations; however, if you have sudo installed at a non\-standard location, you should change the symbolic link to point to the directory where sudo is installed. If you change the symbolic link, its value is preserved across uninstall, re\-install, and upgrade operations with the agent.  
  
## Configure a low\-privileged account for sudo elevation  

The following procedures create a low\-privileged account and sudo elevation by using `opsuser` for a user name.  
  
#### To create a low\-privileged user  
  
1.  Log on to the UNIX or Linux computer as `root`.  
  
2.  Add the user:  
  
    `useradd opsuser`  
  
3.  Add a password and confirm the password:  
  
    `passwd opsuser`  
  
You can now configure sudo elevation and create an SSH key for `opsuser`, as described in the following procedures.  
  
#### To configure sudo elevation for the low\-privileged user  
  
1.  Log on to the UNIX or Linux computer as `root`.  
  
2.  Use the visudo program to edit the sudo configuration in a vi text editor. Run the following command:  
  
    `visudo`  
  
3.  Find the following line:  
  
    `root ALL=(ALL)  ALL`  
  
4.  Insert the following line after it:  
  
    `opsuser ALL=(ALL) NOPASSWD: ALL`  
  
5.  TTY allocation is not supported. Ensure the following line is commented out:  
  
    `# Defaults requiretty`  
  
    > [!IMPORTANT]  
    > This step is required for sudo to work.  
  
6.  Save the file and exit visudo:  
  
    Press ESC \+ : \(colon\) followed by `wq!`, and then press Enter.  
  
7.  Test the configuration by entering in the following two commands. The result should be a listing of the directory without being prompted for a password:  
  
    `su - opsuser`  
  
    `sudo ls /etc`  
  
You can use the `opsuser` account by using the password and sudo elevation for specifying credentials in Operations Manager wizards and for configuring Run As accounts.  
  
## Create an SSH key for authentication  

The following procedures create an SSH key for the `opsuser` account that was created in the previous examples.  
  
#### To generate the SSH key  
  
1.  Log on as `opsuser`.  
  
2.  Generate the key by using the Digital Signature Algorithm \(DSA\) algorithm:  
  
    `ssh-keygen -t dsa`  
  
    Note the optional passphrase if you provided it.  
  
The **ssh\-keygen** creates the `/home/opsuser/.ssh` directory with the private key file \(`id_dsa`\) and the public key file \(`id_dsa.pub`\). You can now configure the key to be supported by `opsuser` as described in the next procedure.  
  
#### To configure a user account to support the SSH key  
  
1.  At the command prompt, type the following commands. To navigate to the user account directory:  
  
    `cd /home/opsuser`  
  
2.  Specify exclusive owner access to the directory:  
  
    `chmod 700 .ssh`  
  
3.  Navigate to the .ssh directory:  
  
    `cd .ssh`  
  
4.  Create an authorized keys file with the public key:  
  
    `cat id_dsa.pub >> authorized_keys`  
  
5.  Give the user read and write permissions to the authorized keys file:  
  
    `chmod 600 authorized_keys`  
  
You can now copy the private SSH key to the Windows\-based computer, as described in the next procedure.  
  
#### To copy the private SSH key to the Windows\-based computer and save in OpenSSH format  
  
1.  Use a tool, such as WinSCP, to transfer the private key file \(`id_dsa` - with no extension\) from the UNIX or Linux computer to a directory on your Windows\-based computer.  
  
2.  Run PuTTYgen.  
  
3.  In the **PuTTY Key Generator** dialog box, click the **Load** button, and then select the private key `(id_dsa`\) that you transferred from the UNIX or Linux computer.  
  
4.  Click **Save private key** and name and save the file to the desired directory.  
  
You can use the `opsuser` account by using the SSH key and sudo elevation for specifying credentials in Operations Manager wizards and for configuring Run As accounts.  
  
## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, review [Credentials You Must Have to Access UNIX and Linux Computers](../plan/planning-security-credentials-for-accessing-unix-and-linux-computers.md)  

- Review the [Configuring SSL Ciphers](Configuring-SSL-Ciphers.md) if you need to reconfigure Operations Manager to use a different cipher.   
  
