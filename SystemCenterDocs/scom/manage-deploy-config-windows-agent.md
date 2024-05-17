---
ms.assetid: 7a4739b5-81ef-4495-aa09-5545641d8274
title: Configure Windows Agents
description: This article describes the options and how to configure the Microsoft Monitoring Agent on Windows computers.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/17/2023
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Configure Windows agents

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

In System Center – Operations Manager, when you install an agent on a computer, a Microsoft Monitoring Agent application is added to the Control Panel. You can use the application to change the account that the agent will use when performing actions requested by the management server to remove a management group from an agent configuration and to configure the Active Directory integration setting for the agent. To perform these tasks, you must have local Administrator permissions on the computer.

> [!NOTE]
> If you want to automate the process of adding or removing management groups from an agent, you can use the [Operations Manager cmdlets](/previous-versions/system-center/hh920227(v=sc.20)) or the Agent API from the [Operations Manager Agent Configuration Library](/previous-versions/system-center/developer/hh329076(v=msdn.10)), allowing you to write scripts that can automate the agent configuration process.

> [!NOTE]
> When you save changes in the Microsoft Monitoring Agent application, the Microsoft Monitoring Agent service will be stopped and restarted.

## Configure an agent to report to multiple management groups

Use the following procedure to make an Operations Manager agent a member of multiple management groups, also referred to as multi-homing. For example, an agent can be configured to report Active Directory data to the Directory Services Management Group and Exchange data to the Messaging Management Group. An agent can be a member of up to four management groups.

You don't need to use the same deployment method for all the management groups.

> [!NOTE]
> It might take one day or longer for the discovered instances of the agent to be made part of the new management group. They will be added after the next discovery interval.

Do one of the following:

- On the agent-managed computer, in the Control Panel, double-click **Microsoft Monitoring Agent**. In Microsoft Monitoring Agent, on the **Operations Manager** tab, select **Add**, enter the information for the new management group, and then select **OK**.  

- Run the **Discovery Wizard** from the Operations Manager Operations console that is connected to the new management group, select the desired computers, and deploy the agent to them. For more information, see [Install agent on Windows using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md). (The menu item in the Operations console named **Discovery Wizard** opens the **Computer and Device Management** wizard.)  

- Run the MOMAgent.msi Windows installer package on the desired computers, and modify the installation by adding a new management group. For more information, see [Install Windows Agent Manually Using MOMAgent.msi](manage-deploy-windows-agent-manually.md).

## Change the account configuration for an agent

You can use the following procedure to change the account that the agent will use when performing actions requested by the management server.

1. On the agent-managed computer, in the Control Panel, double-click **Microsoft Monitoring Agent**.
2. On the **Operations Manager** tab, select a management group and select **Edit**.
3. In the **Agent Action Account** section, edit the account information and select **OK**.

## Remove a management group from an agent

You can use the following procedure to remove a management group from the agent configuration.

1. On the agent-managed computer, in the Control Panel, double-click **Microsoft Monitoring Agent**.
2. On the **Operations Manager** tab, select a management group, and then select **Remove**.
3. Select **OK**.

> [!NOTE]
> You can remove all management groups while leaving the agent installed. This is useful in situations such as when you want to prepare a computer for imaging and want an image with the agent installed but without assignment to a specific management group.

## Change the Active Directory Integration setting for an agent

You can use the following procedure to change the Active Directory integration setting for an agent.

1. On the agent-managed computer, in the Control Panel, double-click **Microsoft Monitoring Agent**.
2. On the **Operations Manager** tab, clear or select **Automatically update management group assignments from AD DS**. If you select this option, on agent startup, the agent will query Active Directory for a list of management groups to which it has been assigned. Those management groups, if any, will be added to the list. If you clear this option, all management groups assigned to the agent in Active Directory will be removed from the list.
3. Select **OK**.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](manage-deploy-windows-agent-console.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](manage-deploy-windows-agent-manually.md).

- To understand what options and steps need to be performed to properly uninstall the agent from your Windows computers, review [Uninstall Agent from Windows-based Computers](manage-uninstall-windows-agent.md).
