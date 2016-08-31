---
title:  Install Agent Using the MOMAgent.msi Setup Wizard
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Install Agent Using the MOMAgent.msi Setup Wizard

>Applies To: System Center 2016 - Operations Manager

Use the following procedure to deploy the System Center Operations Manager agent on computers running Windows by using the MOMAgent.msi setup wizard. For a list of the supported operating system versions, see [Supported Configurations](../plan/system-requirements.md).

Before you use the Setup Wizard, ensure the following conditions are met:

-   Each agent that is installed with the Setup Wizard must be approved by a management group. For more information, see [Process Manual Agent Installations](Process-Manual-Agent-Installations.md).

-   If an agent is manually deployed to a domain controller and an Active Directory management pack is later deployed, errors might occur during deployment of the management pack. To prevent errors from occurring before deploying the Active Directory management pack, or to recover from errors that might have already occurred, you need to deploy the Active Directory management pack helper object by running the file OomADs.msi on the affected domain controller. The file OomADs.msi is on the computer that is hosting the agent at C:\Program Files\System Center Operations Manager\Agent\HelperObjects. After an agent has been manually deployed to a domain controller, locate OomADs.msi and double-click the file to install the Active Directory Management Pack helper object. The Active Directory Management Pack helper object is automatically installed when the agent is deployed using the Discovery Wizard.

> [!NOTE]
> For information about port requirements for agents, see [Communication Between Agents and Management Servers](../plan/planning-agents.md#communication-between-agents-and-management-servers).

### To deploy the Operations Manager agent with the Agent Setup Wizard

1.  Use local administrator privileges to log on to the computer where you want to install the agent.

2.  On the Operations Manager installation media, double-click **Setup.exe**.

3.  In **Optional Installations**, click **Local agent**.

4.  On the **Welcome** page, click **Next**.

5.  On the **Destination Folder** page, leave the installation folder set to the default, or click **Change** and type a path, and then click **Next**.

6.  On the **Management Group Configuration** page, do one of the following:

    -   Leave the **Specify Management Group information** check box selected, and then click **Next**.

    -   Clear the **Specify Management Group information** check box if management group information has been published to Active Directory Domain Services, and then click **Next**.

        > [!NOTE]
        > Step 7 is bypassed by the Agent Setup Wizard if the **Specify Management Group information** check box is cleared.

7.  On the **Management Group Configuration** page, do the following:

    1.  Type the name of the management group in the **Management Group Name** field and the (which server?) server name in the **Management Server** field.

        > [!NOTE]
        > To use a gateway server, enter the gateway server name in the **Management Server** text box.

    2.  Type a value for **Management Server Port**, or leave the default of 5723.

    3.  Click **Next**.

8.  On the **Agent Action Account** page, leave it set to the default of **Local System**, or select **Domain or Local Computer Account**; type the **User Account**, **Password**, and **Domain or local computer**; and then click **Next**.

9. On the **Microsoft Update** page, select **Use Microsoft Update when I check for updates (recommended)** or **I don't want to use Microsoft Update**, and then click **Next**.

10. On the **Ready to Install** page, review the settings and then click **Install** to display the **Installing System Center Operations Manager Agent** page.

11. When the **Completing the Operations Manager Agent Setup Wizard** page appears, click **Finish**.

## Next steps

- To deploy the Windows agent from the Operations console, review [Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
- Before you manually install the Windows agent, you should first review the [Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
- After manually installing the Operations Manager agent on Windows or UNIX and Linux computers, you need to [Process Manual Agent Installations](Process-Manual-Agent-Installations.md)
- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Agents](Configuring-Agents.md)
- Review [Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md) to understand what options and steps need to be performed to properly uninstalling the agent from your Windows computers.  



