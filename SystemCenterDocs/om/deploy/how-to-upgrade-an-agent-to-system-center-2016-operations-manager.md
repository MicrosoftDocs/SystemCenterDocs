---
title:  How to Upgrade an Agent to System Center 2016 - Operations Manager
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---


# How to Upgrade an Agent to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

Use the following procedures to upgrade to System Center 2016 - Operations Manager agents. You should first verify that the agents meet minimum supported configurations. For more information, see [System Requirements: System Center 2016 - Operations Manager](../plan/system-requirements.md).

> [!NOTE]
> If before upgrade an agent was installed using the push install method, after upgrade the server the agent will be put into a pending update state and can be upgraded through the Console. Otherwise the agent should be upgraded manually.

When you upgrade an agent, the Operations Manager installer service runs and is not removed until after the completion of the upgrade. If the agent upgrade fails, you might have to re-install the agent because the installer service was not properly removed. If you attempt to upgrade the agent again and it fails, you should re-install the agent after you have completed upgrading all features of Operations Manager.

> [!NOTE]
> If you have Audit Collection Services (ACS) enabled for an agent prior to this upgrade, it is disabled as part of the agent upgrade process. ACS must be re-enabled after upgrade completes.

If you are upgrading agents that are deployed to a computer that has other System Center 2012 R2 Operations Manager features installed, you must do the following:

-   If the agent is installed on a computer that has System Center 2012 R2 Operations Manager Operations console or Web console installed, you must first uninstall the consoles before you upgrade the agents. You can do this by uninstalling System Center 2012 R2 Operations Manager in Programs and Features. You can reinstall these consoles after upgrade is completed.

> [!NOTE]
> If UAC is enabled, you must run the agent upgrade from an elevated command prompt.

> [!NOTE]
> Information about upgraded agents might not appear in the Operations console for up to 60 minutes after performing the upgrade.

## Upgrading push-installed agents

Push-installed agents are agents that were installed by using the **Computer and Device Management Wizard**. Use the following procedures to upgrade these agents.

#### To upgrade push-installed Windows agents by using the Operations console

1.  Log on to the computer hosting the Operations Manager Operations console. Use an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.

2.  In the Operations console, click **Administration**.

    > [!NOTE]
    > When you run the Operations console on a computer that is not a management server, the **Connect To Server** dialog box appears. In the **Server name** box, type the name of the management server to which you want to connect.

3.  In the **Administration** workspace, in the navigation pane under **Device Management**, click **Pending Management**.

4.  In the **Pending Management** pane, under **Type: Agent Requires Update**, right-click each agent-managed computer listed, and then click **Approve**.

    > [!WARNING]
    > You should not approve more than 200 agents at one time.

5.  In the **Update Agents** dialog box, enter the administrator account credentials or use a selected Management Server Action Account, and then click **Update**. The upgrade status is displayed in the **Agent Management Task Status** dialog box.

6.  When the upgrade is completed, click **Close**.

## Upgrading manually installed agents

Manually-installed agents are agents that were installed manually, either from the Command Prompt, or by using the MOMAgent.msi Setup Wizard. Use the following procedure to upgrade these agents.

#### To upgrade a manually installed Windows agent by using the Setup Wizard

1.  Log on to the computer that hosts the agent with an Operations Manager Administrators role account for your Operations Manager management group.

2.  Run **Setup.exe** from the Operations Manager installation media.

3.  On the first page of the Setup Wizard, click **Local agent**. When the **Welcome to the Microsoft Monitoring Agent Upgrade Wizard** page opens, click **Next**.

4.  In the **Microsoft Monitoring Agent Setup** dialog box, click **Upgrade**. The status page displays the progress of the upgrade.

5.  When the **Completing the Microsoft Monitoring Agent Setup Wizard** page appears, click **Finish**.

#### To upgrade a manually installed Windows agent from the Command Prompt

1.  Log on to the computer that hosts the agent with an Operations Manager Administrators role account for your Operations Manager management group.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Run the following command, where D:\ is the location for the upgrade log file.

    ```
    msiexec /i MOMAgent.msi /qn /l*v D:\logs\AgentUpgrade.log
     AcceptEndUserLicenseAgreement=1

    ```

## Verifying Windows agent upgrade

#### To verify the Windows agent upgrade

1.  In the Operations console, in the navigation pane, click the **Administration** button.

2.  Under **Device Management**, click **Agent Managed**.

3.  In the Agent Managed pane, verify that the value listed in the Version column is 8.0.10918.0.

    > [!NOTE]
    > It can take up to one hour for the console to show the updated version of the agent.

## Upgrading UNIX and Linux agents

#### To upgrade UNIX and Linux agents

-   In the Operations console, in the **Administration** pane, run the **UNIX/Linux Upgrade Wizard**.

    Any existing Run As profiles and Run As accounts continue to have valid configurations. For information about changes to Run As profiles and accounts for UNIX and Linux monitoring in Operations Manager, see [Accessing UNIX and Linux Computers in Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=223881)

#### To manually upgrade UNIX and Linux agents

1.  Log on to Linux/Unix machines and copy the target agent to machines.

2.  Run the commands below on different Systems to upgrade the agents:

    -   Suse/Redhat/CentOS/Oracle Linux: `rpm -U <package>`

    -   Ubuntu/Debian: `-i <package file>`

    -   HP-UX: `swinstall -s <full path to depot> <package name>`

    -   Aix: `/usr/sbin/install -X -F -d <package file> scx.rte/`

    -   Solaris:

        -   Remove the installed package with: `pkgrm MSFTscx`

        -   Install the new package version with: `pkgadd`

#### To verify the UNIX or Linux agent upgrade

1.  In the Operations console, in the navigation pane, click **Administration**.

2.  Under **Device Management**, click **UNIX/Linux Computers**.

3.  Verify that the value listed in the Agent **Version** column is 1.6.2-336, where x is any positive integer.

    > [!NOTE]
    > It can take up to one hour for the console to show the updated version of the agent.



