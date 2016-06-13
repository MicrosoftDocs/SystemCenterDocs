---
title: Configuring Agents
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb877f14-01d6-4f3c-80b6-4c3468ee1dba
---
# Configuring Agents
In [!INCLUDE[om12long](../../includes/om12long_md.md)], when you install an agent on a computer, an Operations Manager Agent application is added to Control Panel. You can use the application to change the account that the agent will use when performing actions requested by the management server, to remove a management group from an agent configuration, and to configure the Active Directory integration setting for the agent. To perform these tasks, you must have local Administrator permissions on the computer.

> [!NOTE]
> If you want to automate the process of adding or removing management groups from an agent, you can use the Agent API that allows you to write scripts that can automate the agent configuration process. For more information, see [Using the Operations Manager Agent Configuration Library](http://go.microsoft.com/fwlink/p/?LinkID=229163).

> [!NOTE]
> When you save changes in the Operations Manager Agent application, the Health service will be stopped and restarted.

-   [Configuring an Agent to Report to Multiple Management Groups](Configuring-Agents.md#bkmk_configuringanagenttoreporttomultiplemanagementgorups)

-   [Changing the Account Configuration for an Agent](Configuring-Agents.md#bkmk_ChangingtheAccountConfigurationforanAgent)

-   [Removing a Management Group from an Agent](Configuring-Agents.md#bkmk_RemovingaManagementGroupfromanAgent)

-   [Changing the Active Directory Integration Setting for an Agent](Configuring-Agents.md#bkmk_ChangingtheActiveDirectoryIntegrationSettingforanAgent)

## <a name="bkmk_configuringanagenttoreporttomultiplemanagementgorups"></a>Configuring an Agent to Report to Multiple Management Groups
Use the following procedure to make an Operations Manager agent a member of multiple management groups, also referred to as *multihoming*. For example, an agent can be configured to report Active Directory data to the Networking Management Group and Exchange data to the Messaging Management Group. An agent can be a member of up to four management groups.

You do not need to use the same deployment method for all of the management groups.

> [!NOTE]
> It might take one day or longer for the discovered instances of the agent to be made part of the new management group. They will be added after the next discovery interval.

#### To make an Operations Manager agent a member of multiple management groups

-   Do one of the following:

    -   On the agent\-managed computer, in Control Panel, double\-click Operations Manager Agent. \(In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.\) In **Operations Manager Agent**, on the **Management Groups** tab, click **Add**, enter the information for the new management group, and then click **OK**.

    -   Run the Discovery Wizard from the Operations Manager Operations console that is connected to the new management group, select the desired computers, and deploy the agent to them. For more information, see [Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md). \(The menu item in the Operations console named Discovery Wizard opens the Computer and Device Management Wizard.\)

    -   Run the MOMAgent.msi on the desired computers, and modify the installation by adding a new management group. For more information, see [Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md).

## <a name="bkmk_ChangingtheAccountConfigurationforanAgent"></a>Changing the Account Configuration for an Agent
You can use the following procedure to change the account that the agent will use when performing actions requested by the management server.

#### To change the account configuration for an agent

1.  On the agent\-managed computer, in Control Panel, double\-click Operations Manager Agent. \(In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.\)

2.  On the **Management Group** tab, select a management group and then click **Edit**.

3.  In the **Agent Action Account** section, edit the account information and then click **OK**.

## <a name="bkmk_RemovingaManagementGroupfromanAgent"></a>Removing a Management Group from an Agent
You can use the following procedure to remove a management group from the agent configuration.

#### To remove a management group from an agent

1.  On the agent\-managed computer, in Control Panel, double\-click Operations Manager Agent. \(In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.\)

2.  On the **Management Group** tab, select a management group and then click **Remove**.

3.  Click **OK**.

    > [!NOTE]
    > You can remove all management groups while leaving the agent installed. This is useful in situations such as when you want to prepare a computer for imaging and want an image with the agent installed but without assignment to a specific management group.

## <a name="bkmk_ChangingtheActiveDirectoryIntegrationSettingforanAgent"></a>Changing the Active Directory Integration Setting for an Agent
You can use the following procedure to change the Active Directory integration setting for an agent.

#### To change the Active Directory integration setting for an agent

1.  On the agent\-managed computer, in Control Panel, double\-click Operations Manager Agent. \(In the category view of Control Panel in Windows Server 2008, Operations Manager Agent is in the **System and Security** category.\)

2.  On the **Management Group** tab, clear or select **Automatically update management group assignments from AD DS**. If you select this option, on agent startup, the agent will query Active Directory for a list of management groups to which it has been assigned. Those management groups, if any, will be added to the list. If you clear this option, all management groups assigned to the agent in Active Directory will be removed from the list.

3.  Click **OK**.

## See Also
[Operations Manager Agent Installation Methods](Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Process Manual Agent Installations](Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
[Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)


