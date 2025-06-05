---
ms.assetid: 017e8bb1-e523-4cc0-bf0c-2d1d4697db11
title: Process Manual Agent Installations
description: This article describes how to process Operations Manager agents deployed manually.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.custom: UpdateFrequency2, engagement-fy23
---

# Process manual agent installations



Manual installation of an agent refers to the process of running MOMAgent.msi locally on a computer that is to host a System Center Operations Manager agent. When it's installed, the agent attempts to join the specified management group by contacting a specified management server. You can use security settings at both the management group and the management server level to configure how requests from manually installed agents are processed.

::: moniker range="sc-om-2022"

>[!NOTE]
> You'll need to restart the computer after installing the Operations Manager 2022 agent.

::: moniker-end

The following three options are available to process manually installed agents.

|Option|Action|
|----------|----------|
|**Reject new manual agent installations**|Designates that all requests from a manually installed agent will be denied by Operations Manager. This is the most secure setting and is selected by default.|
|**Review new manual agent installations in pending management view**|Designates that all requests from a manually installed agent will be directed to Pending Management before being allowed to join the management group. An administrator must review the request and manually approve the agents' request.|
|**Auto-approve new manually installed agents**|This option is available only if **Review new manual agent installations in pending management view** has been selected. This setting causes Operations Manager to automatically allow any manually installed agent to join the management group. This is the least secure option.|

> [!IMPORTANT]
> A management group or management server must be configured to accept agents that are installed with MOMAgent.msi, or they will be automatically rejected and therefore not displayed in the Operations console. If a management group is configured to accept manually installed agents, the agents will display in the console approximately one hour after they are installed.

The following procedures show you how to configure settings for manual agent installations.

## Configure manual agent installation settings for a management group

Follow these steps to configure manual agent installation settings for a management group:

1.  Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Select **Administration**.

3.  In the Administration workspace, expand **Administration**, and then select **Settings**.

4.  In the **Settings** pane, expand **Type: Server**, right-click **Security**, and then select **Properties**.

5.  In the **Global Management Server Settings - Security** dialog, on the **General** tab, do one of the following:

    -   To maintain a higher level of security, select **Reject new manual agent installations**, and then select **OK**.

    -   To configure for manual agent installation, select  **Review new manual agent installations in pending management view**, and then select **OK**.

    -   Optionally, select **Auto-approve new manually installed agents**.

## Override the manual agent installation setting for a single management server

Follow these steps to override the manual agent installation setting for a single management server:

1.  Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Select **Administration**.

3.  In the **Administration** workspace, expand **Administration**, expand **Device Management**, and then select **Management Servers**.

4.  In the results pane, right-click the management server that you want to view the properties of, and then select **Properties**.

5.  In the **Management Server Properties** dialog, select the **Security** tab.

6.  On the **Security** tab, do the following:

    -   To maintain a higher level of security, select **Reject new manual agent installations**, and then select **OK**.

    -   To configure for manual agent installation, select **Review new manual agent installations in pending management view**, and then select **OK**.

    -   Optionally, select **Auto-approve new manually installed agents**.

7.  Select **OK**.

## Approve a pending agent installation when automatic approval isn't configured

Follow these steps to approve a pending agent installation when automatic approval isn't configured:

1.  In the Operations console, select **Administration**.

2.  Select **Pending Management**.

3.  In the **Pending Management** pane, select computers in **Type: Manual Agent Install**.

4.  Right-click the computers, and then select **Approve**.

5.  In the **Manual Agent Install** dialog, select **Approve**. The computers now appear in the **Agent Managed** node and are ready to be managed.

    > [!NOTE]
    > Rejected agents remain in  **Pending Management** until the agent is uninstalled for the management group.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](manage-deploy-windows-agent-console.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](manage-deploy-windows-agent-manually.md).

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](manage-deploy-config-windows-agent.md).

- To understand what options and steps need to be performed to properly uninstall  the agent from your Windows computers, review [Uninstall Agent from Windows-based Computers](manage-uninstall-windows-agent.md).  

- If you would like to install the Nano Server agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](manage-deploy-windows-agent-nano.md).
