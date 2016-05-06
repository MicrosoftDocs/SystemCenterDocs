---
title: How to Set Credentials for Accessing UNIX and Linux Computers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c7ff14e-cb78-4cd2-b5b5-bf67513b7f29
---
# How to Set Credentials for Accessing UNIX and Linux Computers
This topic contains procedures for how to set credentials in wizards for the following tasks, as set by wizards in [!INCLUDE[om12long](./Token/om12long_md.md)]:

-   [Credentials for Installing Agents](./How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md#BKMK_Installing)

-   [Credentials for Run As Accounts](./How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md#BKMK_RunAs)

-   [Credentials for Upgrading an Agent](./How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md#BKMK_Upgrade)

-   [Credentials for Uninstalling an Agent](./How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md#BKMK_Uninstall)

These wizards define credentials to be authenticated on the UNIX or Linux computer and follow a similar process. For an overview of how credentials are provided, see [Accessing UNIX and Linux Computers in Operations Manager](./Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md).

## <a name="BKMK_Discovering"></a>Credentials for Discovering UNIX and Linux Computers
The following procedure begins in **Computer and Device Management Wizard**, on the **Discovery Criteria** page, when you click the **Set Credentials** button. For more information, see [Install Agent on UNIX and Linux Using the Discovery Wizard](./Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md).

#### To set a user \(unprivileged\) account for discovery of an installed agent with a signed certificate.

1.  On the **Credential Settings**page, click the **Default Credentials** tab, and then click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

3.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **OK**.

4.  Click **OK** to return to the **Discovery Criteria** page and continue with the wizard.

## <a name="BKMK_Installing"></a>Credentials for Installing Agents or Signing Certificates of Installed Agents
The following procedures begin in the **Computer and Device Management Wizard**, on the **Discovery Criteria** page, when you click the **Set Credentials** button.

#### To set a privileged credential by using an SSH key

1.  On the **Credential Settings**page, click the **Default Credentials** tab, and then click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account has privileged access**, and then click **OK**.

5.  Click the **Agent Verification** tab, and on the **Agent Verification** page, type a user name and password for an account on the targeted computer. This can be a user \(unprivileged\) account.

6.  Click **OK** to return to the **Discovery Criteria** page and continue with the wizard.

#### To set a unprivileged credential with elevation by using an SSH key

1.  On the **Credential Settings**page, click the **Default Credentials** tab, and then click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **OK**.

5.  Click the **Elevation** page, and select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer. The **su** password is also used for agent verification.

    If you selected **sudo elevation**, click the **Agent Verification** tab, and type a user name and password for an account on the targeted computer. This can be a user \(unprivileged\) account.

6.  Click **OK** to return to the **Discovery Criteria** page and continue with the wizard.

#### To set a privileged credential by using a password

1.  On the **Credential Settings** page, click the **Default Credentials** tab, and then click the **Password** option.

2.  Type a user name, a password, and password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, click **This account has privileged access**.

4.  Click **OK** to return to the **Discovery Criteria** page and continue with the wizard.

#### To set an unprivileged credential with elevation by using a password

1.  On the **Credential Settings** page, click the **Default Credentials** tab, and then click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, click **This account does not privileged access**, and then click **OK**.

4.  Click the **Elevation** page, and select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password you established on the UNIX or Linux computer.

5.  Click **OK** to return to the **Discovery Criteria** page and continue with the wizard.

## <a name="BKMK_RunAs"></a>Credentials for Run As Accounts
The following procedures begin in the **Create UNIX\/Linux Run As Account Wizard** when you select the type for a **Run As Account** \(**Monitoring Account** or **Agent Maintenance Account**\), a name and password and provided a description. For more information, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](./How-to-Configure-Run-As-Accounts-and-Profiles-for-UNIX-and-Linux-Access.md).

#### To set a privileged credential for a monitoring account

1.  On the **Account Credentials** page, type a user name, a password, and the password confirmation.

2.  In the **Do you want to use elevation for privileged access** list, click **Do not use elevation with this account**.

3.  Click **Next** to continue with the wizard.

#### To set an unprivileged credential with elevation for a monitoring account

1.  On the **Account Credentials** page, type a user name, a password, and the password confirmation.

2.  In the **Do you want to use elevation for privileged access** list, click **Elevate this account using sudo for privileged access**.

3.  Click **Next** to continue with the wizard.

#### To set a privileged credential by using an SSH key for an agent maintenance account

1.  On the **Account Credentials** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does the account have privileged access** list, click **This account has privileged access**.

5.  Click **Next** to continue with the wizard.

#### To set an unprivileged credential by using an SSH key with elevation for an agent maintenance account

1.  On the **Account Credentials** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **Next**.

5.  Select the **Elevation** tab, and select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer.

6.  Click **Next** to continue with the wizard.

#### To set a privileged credential by using a password for an agent maintenance account

1.  On the **Account Credentials** page, click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

3.  In the **Does this account have privileged access** list, click **This account has privileged access**.

4.  Click **Next** to continue with the wizard.

#### To set a privileged credential by using a password with elevation for an agent maintenance account

1.  On the **Account Credentials** page, click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

3.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **Next**.

4.  Click the **Elevation** tab, and select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer.

5.  Click **Next** to continue with the wizard.

## <a name="BKMK_Upgrade"></a>Credentials for Upgrading an Agent
The following procedures begin in the **UNIX\/Linux Agent Upgrade Wizard** on the **Credentials** page, when you select **Provide Upgrade Credentials**. For more information, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md).

#### To set a privileged credential by using an SSH key

1.  On the **Credential Settings** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account has privileged access**, and then click **OK**.

5.  On the **Agent Verification** page, type a user name and password for an account on the targeted computer. This can be a user \(unprivileged\) account.

6.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set a unprivileged credential with elevation by using an SSH key

1.  On the **Credential Settings** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **OK**.

5.  Click the **Elevation** page, and select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer, and then click **OK**. The **su** password is also used for agent verification.

    If you select **sudo elevation**, click **Agent Verification**. On the **Agent Verification** page, type a user name and password for an account on the targeted computer. This can be a user \(unprivileged\) account.

6.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set a privileged credential by using a password

1.  On the **Credential Settings** page, click the **Password** option.

2.  Type a user name, a password, and password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, click **This account has privileged access** .

4.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set an unprivileged credential with elevation by using a password

1.  On the **Credential Settings** page, click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, click **This account does not privileged access**, and then click **OK**.

4.  On the **Elevation** page, select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer.

5.  Click **OK** to return to the **Credentials** page and continue with the wizard.

## <a name="BKMK_Uninstall"></a>Credentials for Uninstalling an Agent
The following procedures begin in the  **UNIX\/Linux Agent Uninstall Wizard**, on the **Credentials** page, when you select **Provide Uninstall Credentials**. For more information, see, [Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md).

#### To set a privileged credential by using an SSH key

1.  On the **Credential Settings** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account has privileged access**, and then click **OK**.

5.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set a unprivileged credential with elevation by using an SSH key

1.  On the **Credential Settings** page, click the **SSH key** option.

2.  Type a user name, the path, and name of the key, or click **Browse**.

3.  Enter a passphrase if the key requires it.

4.  In the **Does this account have privileged access** list, click **This account does not have privileged access**, and then click **OK**.

5.  On the **Elevation** page, select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer, and then click **OK**. The **su** password is also used for agent verification.

6.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set a privileged credential by using a password

1.  On the **Credential Settings** page, click the **Password** option.

2.  Type a user name, a password, and password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, select **This account has privileged access** .

4.  Click **OK** to return to the **Credentials** page and continue with the wizard.

#### To set an unprivileged credential with elevation by using a password

1.  On the **Credential Settings** page, click the **Password** option.

2.  Type a user name, a password, and the password confirmation.

    This password is used for agent verification.

3.  In the **Does this account have privileged access** list, click **This account does not privileged access**, and then click **OK**.

4.  On the **Elevation** page, select **su** or **sudo elevation**.

    If you select **su elevation**, type the **superuser** password as established on the UNIX or Linux computer.

5.  Click **OK** to return to the **Credentials** page and continue with the wizard.

## See Also
[Credentials You Must Have to Access UNIX and Linux Computers](./Credentials-You-Must-Have-to-Access-UNIX-and-Linux-Computers.md)
[Accessing UNIX and Linux Computers in Operations Manager](./Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[How to Configure sudo Elevation and SSH Keys](./How-to-Configure-sudo-Elevation-and-SSH-Keys.md)
[Required Capabilities for UNIX and Linux Accounts](./Required-Capabilities-for-UNIX-and-Linux-Accounts.md)
[Configuring SSL Ciphers](./Configuring-SSL-Ciphers.md)


