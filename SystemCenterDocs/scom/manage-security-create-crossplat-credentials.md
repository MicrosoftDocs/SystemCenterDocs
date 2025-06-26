---
ms.assetid: d8bb718e-9ecc-4839-926f-1bc0df246bf6
title: Set credentials for accessing UNIX and Linux computers
description: This article describes how to configure credentials required to securely manage UNIX and Linux computers with Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency3, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Set credentials for accessing UNIX and Linux computers

This article contains procedures for how to set credentials in wizards for the following tasks, as set by wizards in System Center - Operations Manager:  

- Credentials for Installing Agents  
- Credentials for Run As Accounts  
- Credentials for Upgrading an Agent  
- Credentials for Uninstalling an Agent

These wizards define credentials to be authenticated on the UNIX or Linux computer and follow a similar process. For an overview of how credentials are provided, see [Planning Security Credentials for Accessing Unix and Linux Computers](plan-security-crossplat-credentials.md).  

> [!IMPORTANT]
> RunAs account passwords cannot contain "illegal" characters in the [Command Prompt](/windows-server/administration/windows-commands/cmd), such as: `& < ( ) @ ^ | "`
>
> Due to the use of WSMan for monitoring, having these characters in the password may cause monitoring to fail as they cannot be parsed correctly. To avoid grey agents and non-functioning monitoring, change the password to exclude these characters. A *maintenance* account should be OK with these symbols as this is used for SSH communication and works differently, however, to avoid potential issues down the line, please follow the same guidance for all accounts.

## Credentials for discovering UNIX and Linux computers  

The following procedure begins in **Computer and Device Management Wizard**, on the **Discovery Criteria** page, when you select the **Set Credentials** button. For more information, see [Install Agent on UNIX and Linux Using the Discovery Wizard](~/scom/manage-deploy-crossplat-agent-console.md).  

### Set a user (unprivileged) account for discovery of an installed agent with a signed certificate.  

1. On the **Credential Settings**page, select the **Default Credentials** tab, and then select the **Password** option.  

2. Enter a user name, a password, and the password confirmation.  

3. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and select **OK**.  

4. Select **OK** to return to the **Discovery Criteria** page and continue with the wizard.  

## Credentials for installing agents or signing certificates of installed agents  

The following procedures begin in the **Computer and Device Management Wizard**, on the **Discovery Criteria** page, when you select the **Set Credentials** button.  

### Set a privileged credential by using an SSH key  

1. On the **Credential Settings**page, select the **Default Credentials** tab, and then select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account has privileged access**, and then select **OK**.  

5. Select the **Agent Verification** tab, and on the **Agent Verification** page, enter a user name and password for an account on the targeted computer. This can be a user (unprivileged) account.  

6. Select **OK** to return to the **Discovery Criteria** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using an SSH key  

1. On the **Credential Settings**page, select the **Default Credentials** tab, and then select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and then select **OK**.  

5. Select the **Elevation** page, and select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer. The **su** password is also used for agent verification.  

    If you selected **sudo elevation**, select the **Agent Verification** tab, and enter a user name and password for an account on the targeted computer. This can be a user (unprivileged) account.  

6. Select **OK** to return to the **Discovery Criteria** page and continue with the wizard.  

### Set a privileged credential by using a password  

1. On the **Credential Settings** page, select the **Default Credentials** tab, and then select the **Password** option.  

2. Enter a user name, a password, and password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account has privileged access**.  

4. Select **OK** to return to the **Discovery Criteria** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using a password  

1. On the **Credential Settings** page, select the **Default Credentials** tab, and then select the **Password** option.  

2. Enter a user name, a password, and the password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account does not privileged access**, and then select **OK**.  

4. Select the **Elevation** page, and select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password you established on the UNIX or Linux computer.  

5. Select **OK** to return to the **Discovery Criteria** page and continue with the wizard.  

## Credentials for Run As accounts  

The following procedures begin in the **Create UNIX\/Linux Run As Account Wizard** when you select the type for a **Run As Account** (**Monitoring Account** or **Agent Maintenance Account**), a name and password and provide a description. For more information, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](./manage-security-config-crossplat-runas-profile.md).  

### Set a privileged credential for a monitoring account  

1. On the **Account Credentials** page, enter a user name, a password, and the password confirmation.  

2. In the **Do you want to use elevation for privileged access** list, select **Do not use elevation with this account**.  

3. Select **Next** to continue with the wizard.  

### Set an unprivileged credential with elevation for a monitoring account  

1. On the **Account Credentials** page, enter a user name, a password, and the password confirmation.  

2. In the **Do you want to use elevation for privileged access** list, select **Elevate this account using sudo for privileged access**.  

3. Select **Next** to continue with the wizard.  

### Set a privileged credential by using an SSH key for an agent maintenance account  

1. On the **Account Credentials** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does the account have privileged access** list, select **This account has privileged access**.  

5. Select **Next** to continue with the wizard.  

### Set an unprivileged credential by using an SSH key with elevation for an agent maintenance account  

1. On the **Account Credentials** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and then select **Next**.  

5. Select the **Elevation** tab, and select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer.  

6. Select **Next** to continue with the wizard.  

### Set a privileged credential by using a password for an agent maintenance account  

1. On the **Account Credentials** page, select the **Password** option.  

2. Enter a user name, a password, and the password confirmation.  

3. In the **Does this account have privileged access** list, select **This account has privileged access**.  

4. Select **Next** to continue with the wizard.  

### Set a privileged credential by using a password with elevation for an agent maintenance account  

1. On the **Account Credentials** page, select the **Password** option.  

2. Enter a user name, a password, and the password confirmation.  

3. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and then select **Next**.  

4. Select the **Elevation** tab, and select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer.  

5. Select **Next** to continue with the wizard.  

## Credentials for upgrading an agent  

The following procedures begin in the **UNIX\/Linux Agent Upgrade Wizard** on the **Credentials** page when you select **Provide Upgrade Credentials**. For more information, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md).  

### Set a privileged credential by using an SSH key

1. On the **Credential Settings** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account has privileged access**, and then select **OK**.  

5. On the **Agent Verification** page, enter a user name and password for an account on the targeted computer. This can be a user (unprivileged) account.  

6. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using an SSH key

1. On the **Credential Settings** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and then select **OK**.  

5. Select the **Elevation** page, and select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer, and then select **OK**. The **su** password is also used for agent verification.  

    If you select **sudo elevation**, select **Agent Verification**. On the **Agent Verification** page, enter a user name and password for an account on the targeted computer. This can be a user \(unprivileged\) account.  

6. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set a privileged credential by using a password

1. On the **Credential Settings** page, select the **Password** option.  

2. Enter a user name, a password, and password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account has privileged access** .  

4. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using a password

1. On the **Credential Settings** page, select the **Password** option.  

2. Enter a user name, a password, and the password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account does not privileged access**, and then select **OK**.  

4. On the **Elevation** page, select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer.  

5. Select **OK** to return to the **Credentials** page and continue with the wizard.  

## Credentials for uninstalling an agent  

The following procedures begin in the  **UNIX\/Linux Agent Uninstall Wizard** on the **Credentials** page when you select **Provide Uninstall Credentials**. For more information, see, [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md).  

### Set a privileged credential by using an SSH key

1. On the **Credential Settings** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account has privileged access**, and then select **OK**.  

5. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using an SSH key

1. On the **Credential Settings** page, select the **SSH key** option.  

2. Enter a user name, the path, and name of the key, or select **Browse**.  

3. Enter a passphrase if the key requires it.  

4. In the **Does this account have privileged access** list, select **This account does not have privileged access**, and then select **OK**.  

5. On the **Elevation** page, select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer, and then select **OK**. The **su** password is also used for agent verification.  

6. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set a privileged credential by using a password

1. On the **Credential Settings** page, select the **Password** option.  

2. Enter a user name, a password, and password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account has privileged access** .  

4. Select **OK** to return to the **Credentials** page and continue with the wizard.  

### Set an unprivileged credential with elevation by using a password

1. On the **Credential Settings** page, select the **Password** option.  

2. Type a user name, a password, and the password confirmation.  

    This password is used for agent verification.  

3. In the **Does this account have privileged access** list, select **This account does not privileged access**, and then select **OK**.  

4. On the **Elevation** page, select **su** or **sudo elevation**.  

    If you select **su elevation**, enter the **superuser** password as established on the UNIX or Linux computer.  

5. Select **OK** to return to the **Credentials** page and continue with the wizard.  

## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, see [Credentials You Must Have to Access UNIX and Linux Computers](plan-security-crossplat-credentials.md)  

- To understand how to elevate an unprivileged account for effective monitoring of UNIX and Linux computers, see [How to Configure sudo Elevation and SSH Keys](~/scom/manage-security-create-crossplat-sudo-sshkeys.md)  

- If you need to reconfigure Operations Manager to use a different cipher, see [Configuring SSL Ciphers](~/scom/manage-security-crossplat-config-sslcipher.md).
