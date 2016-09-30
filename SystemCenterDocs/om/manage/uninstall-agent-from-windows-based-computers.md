---
title: Uninstall Agent from Windows-based Computers
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Uninstall Agent from Windows-based Computers

>Applies To: System Center 2016 - Operations Manager

Use one of the following procedures to uninstall an System Center Operations Manager agent from an agent-managed computer.

## Uninstall the agent by using the Operations console

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Agent Managed**.

4.  In the **Agent Managed** pane, right-click the computers for which you want to uninstall the agent, and then select **Uninstall**.

5.  In the **Uninstall Agents** dialog box, either leave **Use selected Management Server Action Account** selected or do the following:

    1.  Select **Other user account**.

    2.  Type the **User name** and **Password**, and type or select the **Domain** from the list. Select **This is a local computer account, not a domain account** if the account is a local computer account.

        > [!IMPORTANT]
        > The account must have administrative rights on the computer or the uninstall will fail.

    3.  Click **Uninstall**.

6.  In the **Agent Management Task Status** dialog box, the **Status** for each selected computer changes from **Queued** to **Success**.

    > [!NOTE]
    > If the task fails for a computer, click the computer and read the reason for the failure in the **Task Output** text box.

7.  Click **Close**.

## Uninstall the agent by using the MOMAgent.msi agent setup wizard

1.  Log on to a managed computer with an account that is a member of the administrators security group for the computer.

2.  In **Control Panel**, click **Uninstall a program**.

3.  In **Programs and Features**, click **Microsoft Monitoring Agent**, click **Remove**, and then click **Yes**.

    > [!NOTE]
    > The **Agent Setup Wizard** can also be run by double-clicking **MOMAgent.msi**, which is available on the Operations Manager installation media.

### Uninstall the agent by using MOMAgent.msi from the command line

1.  Log on to the managed computer with an account that is a member of the administrators security group for the computer.

2.  Open a command prompt.

3.  At the prompt, for example, type the following:

    **%WinDir%\System32\msiexec.exe /x <path>\MOMAgent.msi /qb**

## Uninstall the agent from a cluster

1.  Using either the Operations console method or the command line method, uninstall the agent from each node of the cluster.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Agentless Managed**.

4.  In the **Agentless Managed** pane, locate all virtual instances for the cluster, right-click, and then select **Delete**.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md).

- If you would like to install the Nano Server agent using the Discovery Wizard, from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](Install-Agent-on-Nano-Server.md).

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Agents](Configuring-Agents.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](install-windows-agent-manually-using-momagent.md).

