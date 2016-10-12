---
ms.assetid: 7a4739b5-81ef-4495-aa09-5545641d8274
title: Configuring Agents
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Configuring Agents

>Applies To: System Center 2016 - Operations Manager

In System Center 2016 - Operations Manager, when you install an agent on a computer, an Operations Manager Agent application is added to Control Panel. You can use the application to change the account that the agent will use when performing actions requested by the management server, to remove a management group from an agent configuration, and to configure the Active Directory integration setting for the agent. To perform these tasks, you must have local Administrator permissions on the computer.

> [!NOTE]
> If you want to automate the process of adding or removing management groups from an agent, you can use the Agent API that allows you to write scripts that can automate the agent configuration process. For more information, see [Using the Operations Manager Agent Configuration Library](http://go.microsoft.com/fwlink/p/?LinkID=229163).

> [!NOTE]
> When you save changes in the Operations Manager Agent application, the Health service will be stopped and restarted.

## Configuring an agent to report to multiple management groups

Use the following procedure to make an Operations Manager agent a member of multiple management groups, also referred to as *multihoming*. For example, an agent can be configured to report Active Directory data to the Networking Management Group and Exchange data to the Messaging Management Group. An agent can be a member of up to four management groups.

You do not need to use the same deployment method for all of the management groups.

> [!NOTE]
> It might take one day or longer for the discovered instances of the agent to be made part of the new management group. They will be added after the next discovery interval.

### To make an Operations Manager agent a member of multiple management groups

-   Do one of the following:

    -   On the agent-managed computer, in Control Panel, double-click Operations Manager Agent. (In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.) In **Operations Manager Agent**, on the **Management Groups** tab, click **Add**, enter the information for the new management group, and then click **OK**.

    -   Run the Discovery Wizard from the Operations Manager Operations console that is connected to the new management group, select the desired computers, and deploy the agent to them. For more information, see [Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md). (The menu item in the Operations console named Discovery Wizard opens the Computer and Device Management Wizard.)

    -   Run the MOMAgent.msi Windows Installer package on the desired computers, and modify the installation by adding a new management group. For more information, see [Install Windows Agent Manually Using MOMAgent.msi](install-windows-agent-manually-using-momagent.md).

## Changing the account configuration for an agent

You can use the following procedure to change the account that the agent will use when performing actions requested by the management server.

### To change the account configuration for an agent

1.  On the agent-managed computer, in Control Panel, double-click Operations Manager Agent. (In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.)

2.  On the **Management Group** tab, select a management group and then click **Edit**.

3.  In the **Agent Action Account** section, edit the account information and then click **OK**.

## Removing a management group from an agent

You can use the following procedure to remove a management group from the agent configuration.

### To remove a management group from an agent

1.  On the agent-managed computer, in Control Panel, double-click Operations Manager Agent. (In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.)

2.  On the **Management Group** tab, select a management group and then click **Remove**.

3.  Click **OK**.

    > [!NOTE]
    > You can remove all management groups while leaving the agent installed. This is useful in situations such as when you want to prepare a computer for imaging and want an image with the agent installed but without assignment to a specific management group.

## Changing the Active Directory integration setting for an agent

You can use the following procedure to change the Active Directory integration setting for an agent.

### To change the Active Directory integration setting for an agent

1.  On the agent-managed computer, in Control Panel, double-click Operations Manager Agent. (In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.)

2.  On the **Management Group** tab, clear or select **Automatically update management group assignments from AD DS**. If you select this option, on agent startup, the agent will query Active Directory for a list of management groups to which it has been assigned. Those management groups, if any, will be added to the list. If you clear this option, all management groups assigned to the agent in Active Directory will be removed from the list.

3.  Click **OK**.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](install-windows-agent-manually-using-momagent.md)

- Review [Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md) to understand what options and steps need to be performed to properly uninstall the agent from your Windows computers. 


