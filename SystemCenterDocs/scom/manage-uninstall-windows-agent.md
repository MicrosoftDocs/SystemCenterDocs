---
ms.assetid: 11d9cf46-2880-493f-bdf1-29263e2949f0
title: Uninstall Agent from Windows-based Computers
description: This article describes the different methods to uninstall the Operations Manager agent from Windows computers.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Uninstall Agent from Windows-based Computers



Use one of the following procedures to uninstall a System Center Operations Manager agent from an agent-managed computer.

## Uninstall the agent by using the Operations console

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, select **Administration**.

3.  In the **Administration** workspace, select **Agent Managed**.

4.  In the **Agent Managed** pane, right-click the computers for which you want to uninstall the agent, and then select **Uninstall**.

5.  In the **Uninstall Agents** dialog, either leave **Use selected Management Server Action Account** selected or do the following:

    1.  Select **Other user account**.

    2.  Enter the **User name** and **Password**, and enter or select the **Domain** from the list. Select **This is a local computer account, not a domain account** if the account is a local computer account.

        > [!IMPORTANT]
        > The account must have administrative rights on the computer or the uninstall will fail.

    3.  Select **Uninstall**.

6.  In the **Agent Management Task Status** dialog, the **Status** for each selected computer changes from **Queued** to **Success**.

    > [!NOTE]
    > If the task fails for a computer, select the computer and read the reason for the failure in the **Task Output** text box.

7.  Select **Close**.

## Uninstall the agent by using the MOMAgent.msi agent setup wizard

1.  Sign in to a managed computer with an account that is a member of the administrators security group for the computer.

2.  In **Control Panel**, select **Uninstall a program**.

3.  In **Programs and Features**, select **Microsoft Monitoring Agent**, select **Remove**, and then select **Yes**.

    > [!NOTE]
    > The **Agent Setup Wizard** can also be run by double-clicking **MOMAgent.msi**, which is available on the Operations Manager installation media.

### Uninstall the agent by using MOMAgent.msi from the command line

1.  Sign in to the managed computer with an account that is a member of the administrators security group for the computer.

2.  Open a command prompt.

3.  At the prompt, for example, enter the following:

    **%WinDir%\System32\msiexec.exe /x \<path\>\MOMAgent.msi /qb**

## Uninstall the agent from a cluster

1.  Using either the Operations console method or the command line method, uninstall the agent from each node of the cluster.

2.  In the Operations console, select **Administration**.

3.  In the **Administration** workspace, select **Agentless Managed**.

4.  In the **Agentless Managed** pane, locate all virtual instances for the cluster, right-click, and then select **Delete**.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md).

- If you would like to install the Nano Server agent using the Discovery Wizard from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](~/scom/manage-deploy-windows-agent-nano.md).

- To understand how to manage the configuration settings of a Windows agent and the options available, review [Configuring Windows Agents](manage-deploy-windows-agent-manually.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](manage-deploy-windows-agent-manually.md).
