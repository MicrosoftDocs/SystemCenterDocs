---
ms.assetid: 4d1cf6ab-ed6e-4cd8-8ab8-f5d294877e4a
title: Upgrade an Agent to System Center Operations Manager
description: This article describes how to upgrade an Operations Manager agent to System Center.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 180-days
ms.custom: UpdateFrequency.5
ms.service: system-center
monikerRange: ' >=sc-om-2019'
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade an Operations Manager agent

::: moniker range="sc-om-2025"

Use the following procedures to upgrade an agent running on Windows or Linux to System Center Operations Manager 2025. You should first verify that the agents meet the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

::: moniker-end

::: moniker range="sc-om-2019"

Use the following procedures to upgrade an agent running on Windows or Linux to System Center Operations Manager 2019. You should first verify that the agents meet the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

::: moniker-end

::: moniker range="sc-om-2022"

Use the following procedures to upgrade an agent running on Windows or Linux to System Center Operations Manager 2022. You should first verify that the agents meet the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

::: moniker-end

::: moniker range=">=sc-om-2019"

> [!NOTE]
> - To upgrade an Operations Manager agent through the console, ensure that the Run As Account used for upgrade is granted with the *Log on as a Service* right on all the Management Servers and Gateways.
For more information, see [enable service log on](enable-service-logon.md).
> - If before the upgrade an agent was installed using the push install method, after the upgrade the agent-managed computer is put into a pending update state and can be upgraded through the Operations console. Otherwise, the agent needs to be upgraded manually.

When you upgrade an agent, the Operations Manager installer service runs and isn't removed until after the completion of the upgrade. If the agent upgrade fails, you might have to reinstall the agent because the installer service wasn't properly removed. If you attempt to upgrade the agent again and it fails, you should reinstall the agent after you've completed upgrading all features of Operations Manager.

> [!NOTE]
> If you've Audit Collection Services (ACS) enabled for an agent prior to this upgrade, it's disabled as part of the agent upgrade process. ACS must be re-enabled after the upgrade completes.

::: moniker-end

::: moniker range="sc-om-2019"

If you're upgrading agents that are deployed to a computer that has other System Center 2012 R2 or 2016 Operations Manager features installed, you must do the following:

- If the agent is installed on a computer that has System Center 2012 R2 or 2016 Operations Manager Operations console or Web console installed, you must first uninstall the consoles before you upgrade the agents. You can do this by uninstalling System Center 2012 R2 or 2016 Operations Manager in Programs and Features. You can reinstall these consoles after the upgrade is completed.

::: moniker-end

::: moniker range="sc-om-2022"
If you're upgrading agents that are deployed to a computer that has other System Center 2019 Operations Manager features installed, you must do the following:

- If the agent is installed on a computer that has System Center 2019 Operations Manager Operations console or Web console installed, you must first uninstall the consoles before you upgrade the agents. You can do this by uninstalling System Center 2019 Operations Manager in Programs and Features. You can reinstall these consoles after upgrade is completed.

::: moniker-end

::: moniker range="sc-om-2025"
If you're upgrading agents that are deployed to a computer that has other System Center 2022 Operations Manager features installed, you must do the following:

- If the agent is installed on a computer that has System Center 2022 Operations Manager Operations console or Web console installed, you must first uninstall the consoles before you upgrade the agents. You can do this by uninstalling System Center 2022 Operations Manager in Programs and Features. You can reinstall these consoles after upgrade is completed.

::: moniker-end

::: moniker range=">=sc-om-2019"

> [!NOTE]
> If UAC is enabled, you must run the agent upgrade from an elevated command prompt.

> [!NOTE]
> Information about upgraded agents might not appear in the Operations console for up to 60 minutes after performing the upgrade.

## Upgrade push-installed agents

Push-installed agents are agents that were installed by using the **Computer and Device Management Wizard**. Use the following procedures to upgrade these agents.

### Upgrade push-installed Windows agents by using the Operations console

1. Sign in to the computer hosting the Operations Manager Operations console. Use an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2. In the Operations console, select **Administration**.

    > [!NOTE]
    > When you run the Operations console on a computer that isn't a management server, the **Connect To Server** dialog appears. In the **Server name** box, type the name of the management server to which you want to connect.

3. In the **Administration** workspace, in the navigation pane under **Device Management**, select **Pending Management**.

4. In the **Pending Management** pane, under **Type: Agent Requires Update**, right-click each agent-managed computer listed, and select **Approve**.

    > [!WARNING]
    > You shouldn't approve more than 200 agents at one time.

5. In the **Update Agents** dialog, enter the administrator account credentials or use a selected Management Server Action Account, and select **Update**. The upgrade status is displayed in the **Agent Management Task Status** dialog.

6. When the upgrade is completed, select **Close**.

## Upgrade manually installed agents

Manually installed agents are agents that were installed manually either from the Command Prompt or by using the MOMAgent.msi Setup Wizard. Use the following procedure to upgrade these agents. Navigate to the Operations Manager installation folder to locate the Agent installation files for Windows: `C:\Program Files\Microsoft System Center\Operations Manager\Server\AgentManagement\amd64`

#### Upgrade a manually installed Windows agent by using the Setup Wizard

1. Sign in to the computer that hosts the agent with an Operations Manager Administrators role account for your Operations Manager management group.

2. Run **Setup.exe** from the Operations Manager installation media.

3. On the first page of the Setup Wizard, select **Local agent**. When the **Welcome to the Microsoft Monitoring Agent Upgrade Wizard** page opens, select **Next**.

4. In the **Microsoft Monitoring Agent Setup** dialog, select **Upgrade**. The status page displays the progress of the upgrade.

5. When the **Completing the Microsoft Monitoring Agent Setup Wizard** page appears, select **Finish**.

#### Upgrade a manually installed Windows agent from the Command Prompt

1. Sign in to the computer that hosts the agent with an Operations Manager Administrators role account for your Operations Manager management group.

2. Open a Command Prompt window by using the **Run as Administrator** option.

3. Run the following command, where D:\ is the location for the upgrade log file.

    ```
    msiexec /i MOMAgent.msi /qn /l*v D:\logs\AgentUpgrade.log AcceptEndUserLicenseAgreement=1
    ```

## Verify Windows agent upgrade

To verify the Windows agent upgrade, follow these steps:

1. In the Operations console, in the navigation pane, select the **Administration** button.

2. Under **Device Management**, select **Agent Managed**.

::: moniker-end

::: moniker range="sc-om-2019"

3. In the Agent Managed pane, verify that the value listed in the **Version** column is 10.19.10050.0.

::: moniker-end

::: moniker range="sc-om-2022"

3. In the Agent Managed pane, verify that the value listed in the **Version** column is 10.22.10118.0.

::: moniker-end

::: moniker range="sc-om-2025"

3.  In the Agent Managed pane, verify that the value listed in the **Version** column is \<build number\>.

::: moniker-end

::: moniker range=">=sc-om-2019"

   > [!NOTE]
   > It can take up to one hour for the console to show the updated version of the agent.

## Upgrade UNIX and Linux agents

To upgrade UNIX and Linux agents, follow these steps:

- In the Operations console, in the **Administration** pane, run the **UNIX/Linux Upgrade Wizard**.

    Any existing Run As profiles and Run As accounts continue to have valid configurations. For information about changes to Run As profiles and accounts for UNIX and Linux monitoring in Operations Manager, see [Accessing UNIX and Linux Computers in Operations Manager](/previous-versions/system-center/system-center-2012-R2/hh212886(v=sc.12)).

#### Manually upgrade UNIX and Linux agents

Navigate to the Operations Manager installation folder to locate the Agent installation files for UNIX/Linux: `C:\Program Files\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits`

1. Sign in to Linux/Unix machines and copy the agent (scx-\<version\>.universalr.\<version\>.\<arch\>.sh) to the Linux server. This should be done via SCP or FTP in binary mode..

2. Install the package with the following command.

    `sh ./scx-<version>.universalr.<version>.<arch>.sh –-upgrade --enable-opsmgr`

3. Verify the package is installed with the following command.

    `rpm -q scx`

4. Verify that the Microsoft SCX CIM Server is running with the following command.

    `scxadmin -status`

#### Verify the UNIX or Linux agent upgrade from the console

1. In the Operations console, in the navigation pane, select **Administration**.

2. Under **Device Management**, select **UNIX/Linux Computers**.

3. Verify that the value listed in the Agent **Version** column is 1.6.10-2.

    > [!NOTE]
    > It can take up to one hour for the console to show the updated version of the agent.

::: moniker-end

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).  

- To understand the options and steps for installing agents and discovering objects to be monitored by Operations Manager, review information in the [Managing Discovery and Agents](welcome.md) section.
