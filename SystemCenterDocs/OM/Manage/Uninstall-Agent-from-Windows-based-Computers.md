---
title: Uninstall Agent from Windows-based Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcdb6644-66e0-4a50-a4e0-5f23e2c3b152
---
# Uninstall Agent from Windows-based Computers
Use one of the following procedures to uninstall an [!INCLUDE[om12long](Token/om12long_md.md)] agent from an agent\-managed computer.

## <a name="bkmk_TouninstalltheagentbyusingtheOperationsconsole"></a>To uninstall the agent by using the Operations console

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Agent Managed**.

4.  In the **Agent Managed** pane, right\-click the computers for which you want to uninstall the agent, and then select **Uninstall**.

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

## <a name="bkmk_TouninstalltheagentbyusingtheMOMAgentmsiagentsetupwizard"></a>To uninstall the agent by using the MOMAgent.msi agent setup wizard

1.  Log on to a managed computer with an account that is a member of the administrators security group for the computer.

2.  In **Control Panel**, click **Uninstall a program**.

3.  In **Programs and Features**, click **System Center Operations Manager 2012 Agent**, click **Remove**, and then click **Yes**.

    > [!NOTE]
    > The **Agent Setup Wizard** can also be run by double\-clicking **MOMAgent.msi**, which is available on the Operations Manager installation media.

### To uninstall the agent by using MOMAgent.msi from the command line

1.  Log on to the managed computer with an account that is a member of the administrators security group for the computer.

2.  Open the command window.

3.  At the prompt, for example, type the following:

    **%WinDir%\\System32\\msiexec.exe \/x <path>\\MOMAgent.msi \/qb**

## <a name="bkmk_Touninstalltheagentfromacluster"></a>To uninstall the agent from a cluster

1.  Using either the Operations console method or the command line method, uninstall the agent from each node of the cluster.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Agentless Managed**.

4.  In the **Agentless Managed** pane, locate all virtual instances for the cluster, right\-click, and then select **Delete**.

## See Also
[Operations Manager Agent Installation Methods](Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Process Manual Agent Installations](Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](Configuring-Agents.md)
[Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)


