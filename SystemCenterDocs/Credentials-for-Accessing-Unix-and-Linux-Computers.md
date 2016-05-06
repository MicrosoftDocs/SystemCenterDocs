---
title: Credentials for Accessing Unix and Linux Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 840ea9cc-9407-4bfe-afcd-2ce62aa6cf7d
---
# Credentials for Accessing Unix and Linux Computers
This topic describes the credentials required to install, maintain, upgrade, and uninstall agents on a UNIX or Linux computer.

## Credentials for Installing Agents
[!INCLUDE[om12short](./Token/om12short_md.md)] uses the Secure Shell \(SSH\) protocol to install an agent and Web Services for Management \(WS\-Management\) to discover previously installed agents. Installation requires a privileged account on the UNIX or Linux computer. There are two ways to provide credentials to the targeted computer, as obtained by the **Computer and Device Management Wizard**:

-   Specify a user name and password.

    The SSH protocol uses the password to install an agent or the WS\-Management protocol if the agent was already installed by using a signed certificate.

-   Specify a user name and an SSH key. The key can include an optional passphrase.

If you are not using the credentials for a privileged account, you can provide additional credentials so that your account becomes  a privileged account through elevation of privilege on the UNIX or Linux computer.

The installation is not completed until the agent is verified. Agent verification is performed by the WS\-Management protocol that uses credentials maintained on the management server, separate from the privileged account that is used to install the agent. You are required to provide a user name and password for agent verification if you have done one of the following:

-   Provided a privileged account by using a key.

-   Provided an unprivileged account to be elevated by using sudo with a key.

-   Ran the wizard with the **Discovery Type** set to **Discover only computers with the UNIX\/Linux agent installed**.

Alternatively, you can install the agent, including its certificate, manually on the UNIX or Linux computer and then discover that computer. This method is the most secure way to install agents. For more information, see [Install the Agent and Certificate on UNIX and Linux Computers Using the Command Line](./Install-the-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md).

### Credentials for Monitoring Operations and Performing Agent Maintenance
[!INCLUDE[om12short](./Token/om12short_md.md)] contains three predefined profiles to use in monitoring UNIX and Linux computers and performing agent maintenance:

-   UNIX\/Linux action account

    This profile is an unprivileged account profile that is required for basic health and performance monitoring.

-   UNIX\/Linux privileged account

    This profile is a privileged account profile used for monitoring protected resources such as log files.

-   UNIX\/Linux maintenance account

    This profile is used for privileged maintenance operations, such as updating and removing agents.

In the UNIX and Linux management packs, all the rules, monitors, tasks, recoveries, and other management pack elements are configured to use these profiles. Consequently, there is no requirement to define additional profiles by using the Run As Profiles Wizard unless special circumstances dictate it. The profiles are not cumulative in the scope. For example, the UNIX\/Linux maintenance account profile cannot be used in place of the other profiles simply because it is configured by using a privileged account.

In [!INCLUDE[om12short](./Token/om12short_md.md)], a profile cannot function until it is associated with at least one Run As account. The credentials for accessing the UNIX or Linux computers are configured in the Run As accounts. Because there are no predefined Run As accounts for UNIX and Linux monitoring, you must create them.

To create a Run As account, you must run the **UNIX\/Linux Run As Account Wizard** that is available when you select **UNIX\/Linux Accounts** in the **Administration** workspace. The wizard creates a Run As account based on the choice of a Run As account type. There are two Run As account types:

-   Monitoring account

    Use this account for ongoing health and performance monitoring in operations that communicate by using WS\-Management.

-   Agent maintenance account

    Use this account for agent maintenance such as updating and uninstalling in operations that communicate by using SSH.

These Run As account types can be configured for different levels of access according to the credentials that you supply. Credentials can be unprivileged or privileged accounts or unprivileged accounts that will be elevated to privileged accounts. The following table shows the relationships between profiles, Run As accounts, and levels of access.

|Profiles|Run As account type|Allowable Access Levels|
|------------|-----------------------|---------------------------|
|UNIX\/Linux action account|Monitoring account|-   Unprivileged<br />-   Privileged<br />-   Unprivileged, elevated to privileged|
|UNIX\/Linux privileged account|Monitoring account|-   Privileged<br />-   Unprivileged, elevated to privileged|
|UNIX\/Linux maintenance account|Agent maintenance account|-   Privileged<br />-   Unprivileged, elevated to privileged|

Note that there are three profiles, but only two Run As Account types.

When you specify a Monitoring Run As Account Type, you must specify a user name and password for use by the WS\-Management protocol. When you specify an Agent Maintenance Run As Account Type, you must specify how the credentials are supplied to the targeted computer by using the SSH protocol:

-   Specify a user name and a password.

-   Specify a user name and a key. You can include an optional passphrase.

After you created the Run As accounts, you must edit the UNIX and Linux profiles to associate them with the Run As accounts you created.  For detailed instructions, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](https://technet.microsoft.com/library/hh212926.aspx)

### Credentials for Upgrading and Uninstalling Agents
The **UNIX\/Linux Agent Upgrade Wizard** and the **UNIX\/Linux Agent Uninstall Wizard** provide credentials to their targeted computers. The wizards first prompt you to select the targeted computers to upgrade or uninstall, followed by options on how to provide the credentials to the targeted computer:

-   **Use existing associated Run As Accounts**

    Select this option to use the credentials associated with the UNIX\/Linux action account profile and the UNIX\/Linux maintenance account profile.

    The wizard alerts you if one or more of the selected computers do not have an associated Run As account in the required profiles, in which case you must go back and clear those computers that do not have an associated Run As account, or specify credentials.

-   **Specify credentials**

    Select this option to specify Secure Shell \(SSH\) credentials by using a user name and password or a user name and a key. You can optionally provide a passphrase with a key. If the credentials are not for a privileged account, you can have them elevated to a privileged account on the target computered by using the UNIX su or sudo elevation programs. The ‘su’ elevation requires a password. If you use sudo elevation, you are prompted for a user name and password for agent verification by using an unprivileged account.


