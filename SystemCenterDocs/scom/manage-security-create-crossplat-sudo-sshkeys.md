---
ms.assetid: 68d9b467-12db-4fec-af94-9f9fa15c5f86
title: Configure sudo Elevation and SSH Keys
titlesuffix: Microsoft System Center Operations Manager
description: This article describes how to configure sudo and SSH keys for an unprivileged account and secure communication with Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Configure sudo elevation and SSH keys

With Operations Manager, you can provide credentials for an unprivileged account to be elevated on a UNIX or Linux computer using sudo, allowing the user to run programs or access files that have the security privileges of another user account. For agent maintenance, you also have the ability to use Secure Shell (SSH) keys instead of a password for secure communication between Operations Manager and the targeted computer.  

> [!NOTE]
> Operations Manager supports SSH Key-based authentication with key file data in the PuTTY Private Key (PPK) format. Currently supports SSH v.1 RSA keys and SSH v.2 RSA and DSA keys.

To obtain and configure the SSH key from the UNIX and Linux computer, you need the following software on your Windows-based computer:  

- A file transfer tool, such as WinSCP, to transfer files from the UNIX or Linux computer to the Windows-based computer.  
- The PuTTY program, or a similar program, to run commands on the UNIX or Linux computer.  
- The PuTTYgen program to save the private SHH key in OpenSSH format on the Windows-based computer.  

> [!NOTE]  
> The sudo program exists at different locations on UNIX and Linux operating systems. To provide uniform access to sudo, the UNIX and Linux agent installation script creates the symbolic link `/etc/opt/microsoft/scx/conf/sudodir` to point to the directory expected to contain the sudo program. The agent then uses this symbolic link to invoke sudo.
> When the agent is installed this symbolic link is created automatically, there are no additional actions required on standard UNIX and Linux configurations; however, if you have sudo installed at a non-standard location, you should change the symbolic link to point to the directory where sudo is installed. If you change the symbolic link, its value is preserved across uninstall, re-install, and upgrade operations with the agent.  

## Configure an account for sudo elevation

> [!NOTE]
> The information provided in this section walks through configuring an example user, `scomuser`, and grants it full rights on the client computer.
>
> If you already have user accounts and/or want to setup **Low Privilege** monitoring, sudoers templates are available and grant only the permissions needed for successful monitoring and maintenance operations. For more information, see: [Sudoers templates for elevation in UNIX/Linux monitoring](manage-security-unix-linux-sudoers-templates.md)

The following procedures create an account and sudo elevation by using `scomuser` for a user name.  

### Create a user

1. Sign in the UNIX or Linux computer as `root`
2. Add the user: `useradd scomuser`
3. Add a password and confirm the password: `passwd scomuser`

You can now configure sudo elevation and create an SSH key for `scomuser`, as described in the following procedures.

### Configure sudo elevation for the user

1. Sign in the UNIX or Linux computer as `root`
2. Use the visudo program to edit the sudo configuration in a vi text editor. Run the following command: `visudo`
3. Find the following line: `root ALL=(ALL)  ALL`
4. Insert the following line after it: `scomuser ALL=(ALL) NOPASSWD: ALL`
5. TTY allocation isn't supported. Ensure the following line is commented out: `# Defaults requiretty`

    > [!IMPORTANT]
    > This step is required for sudo to work.

6. Save the file and exit visudo:
    - Press `ESC` then `: (colon)` followed by `wq!`, and then press `Enter` to save your changes and exit gracefully.
7. Test the configuration by entering in the following two commands. The result should be a listing of the directory without being prompted for a password:

    ```bash
    su - scomuser
    sudo ls /etc
    ```

You can now access the `scomuser` account by using its password and sudo elevation, allowing you to specify credentials in task and discovery wizards, and within RunAs Accounts.

## Create an SSH key for authentication  

> [!TIP]
> SSH keys are only used for agent maintenance operations and are not used for monitoring, ensure you're creating the key for the correct user if using multiple accounts.

The following procedures create an SSH key for the `scomuser` account that was created in the previous examples.  

### Generate the SSH key

1. Sign in as `scomuser`.  
2. Generate the key by using the Digital Signature Algorithm \(DSA\) algorithm: `ssh-keygen -t dsa`  
    - Note the optional passphrase if you provided it.

The **ssh-keygen** utility creates the `/home/scomuser/.ssh` directory with the private key file `id_dsa` and the public key file `id_dsa.pub` inside, these files are used in the following procedure.

#### Configure a user account to support the SSH key  

1. At the command prompt, type the following commands. To navigate to the user account directory: `cd /home/scomuser`  
2. Specify exclusive owner access to the directory: `chmod 700 .ssh`  
3. Navigate to the .ssh directory: `cd .ssh`  
4. Create an authorized keys file with the public key: `cat id_dsa.pub >> authorized_keys`  
5. Give the user read and write permissions to the authorized keys file: `chmod 600 authorized_keys`  

You can now copy the private SSH key to the Windows\-based computer, as described in the next procedure.  

#### Copy the private SSH key to the Windows\-based computer and save in OpenSSH format

1. Use a tool, such as WinSCP, to transfer the private key file `id_dsa` (with no extension) from the client to a directory on your Windows-based computer.  
2. Run PuTTYgen.  
3. In the **PuTTY Key Generator** dialog box, select the **Load** button, and then select the private key `id_dsa` that you transferred from the UNIX or Linux computer.  
4. Select **Save private key** and name and save the file to the desired directory.
5. You can use the exported file within a maintenance RunAs account configured for `scomuser`, or when performing maintenance tasks through the console.

You can use the `scomuser` account by using the SSH key and sudo elevation for specifying credentials in Operations Manager wizards and for configuring Run As accounts. 

> [!IMPORTANT]
> **PPK file version 2 is the only version currently supported for System Center Operations Manager.**
>
> By default, PuTTYgen is set to use PPK file version 3. You may change the PPK file version to 2 by going to the toolbar and selecting Key > Parameters for saving key files..., then select the radio button for 2 for PPK file version.
>
> :::image type="content" source="media/manage-security-create-crossplat-sudo-sshkeys/puttygen-key-generator-private-key-file-parameters.png" alt-text="Screenshot of PuTTY Key Generator showing that where to select the PPK file version for the private key.":::

## Next steps

- Review [Credentials You Must Have to Access UNIX and Linux Computers](plan-security-crossplat-credentials.md) to understand how to authenticate and monitor your UNIX and Linux computers.
- Review [Configuring SSL Ciphers](manage-security-crossplat-config-sslcipher.md) if you need to reconfigure Operations Manager to use a different cipher.
