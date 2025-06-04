---
ms.assetid: e68783da-5a7e-43f3-b7d1-0b82bd597d03
title: Install Agent on Windows Using the Discovery Wizard
description: This topic describes how to deploy the Operations Manager agent on Windows computers using the Discovery Wizard.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, intro-installation, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: conceptual
---

# Install Agent on Windows Using the Discovery Wizard



You can use the Operations console to search your environment for manageable objects and then deploy an agent to any object that you want to monitor. The process of searching your environment is called discovery. One of the advantages of using discovery is that it lists *all* manageable objects, including any that you might not be aware of.

The Discovery Wizard doesn't show computers that the management group is already monitoring. If you're doing a phased rollout of your management group, you can run the wizard to add new computers to the group. Also, after your initial deployment, you can use the Discovery Wizard to add newly installed computers to be managed.

When agents are pushed out to computers, System Center Operations Manager sends credentials that have local administrator rights for that computer; this is required to install the agent.

If the Discovery Wizard isn't right for your needs (for example, if you have a set list of computers to which you want to deploy agents), you have the option of manually installing agents on systems to be managed. Agents can also be embedded in the host image of the monitored computer.

Use the following procedure to discover computers running Windows and deploy the Operations Manager agent to the discovered computers from the Operations console. For a list of the supported operating system versions, see [Microsoft Monitoring Agent Operating System requirements](./system-requirements.md).

> [!NOTE]
> For information about port requirements for agents, see [Agent and Agentless Monitoring](/previous-versions/system-center/system-center-2012-R2/hh487284(v=sc.12)) in the Deployment Guide.

## Install an agent on a computer running Windows by using the Discovery Wizard

Follow these steps to install an agent on a computer running Windows by using the Discovery Wizard:

1. Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2. Select **Administration**.

3. At the bottom of the navigation pane, select **Discovery Wizard**.

4. In the **Computer and Device Management Wizard**, on the **Discovery Type** page, select **Windows computers**.

5. On the **Auto or Advanced?** page, do the following:

   1. Select either **Automatic computer discovery** or **Advanced discovery**. If you select **Automatic computer discovery**, select **Next**, and then go to step 7. If you select **Advanced discovery**, continue with the following steps.

       > [!NOTE]
       > Automatic computer discovery scans for Windows-based computers in the domain. Advanced discovery allows you to specify criteria for the computers that the wizard will return, such as computer names starting with NY.

   2. In the **Computer and Device Classes** list, select **Servers and Clients**, **Servers Only**, or **Clients Only**.

   3. In the **Management Server** list, select the management server or gateway server to discover the computers.

   4. If you selected **Servers and Clients**, you can select the **Verify discovered computers can be contacted** checkbox. This is likely to increase the success rate of agent deployment, but discovery can take longer.

       > [!NOTE]
       > If the Active Directory catalog doesn't contain the NetBIOS names for computers in a domain, select **Verify discovered computers can be contacted**. Otherwise, the **Browse, or Type In** option fails to find computers. This affects computers in the same domain as the management server, in another domain with a full trust relationship, and in untrusted domains by using a gateway server.

   5. Select **Next**.

       > [!NOTE]
       > The wizard can return approximately 4000 computers if **Verify discovered computers can be contacted** is selected, and it can return 10,000 computers if this option isn't selected. Automatic computer discovery verifies that discovered computers can be contacted. A computer that is already managed by the management group isn't returned.

6. On the **Discovery Method** page, you can locate the computers that you want to manage by either scanning or browsing Active Directory Domain Services or entering the computer names.

 If you want to scan, do the following:

 1. If it isn't already selected, select **Scan Active Directory** and select **Configure**.

 2. In the **Find Computers** dialog, enter the criteria that you want to use for discovering computers, and select **OK**.

 3. In the **Domain** list, select the domain of the computers that you want to discover.

 If you want to browse Active Directory Domain Services or enter the computer names, do the following:

   1. Select **Browse for, or type-in computer names**, select **Browse**, specify the names of the computers that you want to manage, and select **OK**.

   2. In the **Browse for, or type-in computer names** box, enter the computer names, separated by a semicolon, comma, or a new line. You can use NetBIOS computer names or fully qualified domain names (FQDN).

7. Select **Next**, and on the **Administrator Account** page, do one of the following:

   1. Select **Use selected Management Server Action Account** if it isn't already selected.

   2. Select **Other user account**, enter the **User name** and **Password**, and then select the **Domain** from the list. If the user name isn't a domain account, select **This is a local computer account, not a domain account**.

       > [!IMPORTANT]
       > The account must have administrative privileges on the targeted computers. If **This is a local computer account, not a domain account** is selected, the management server action account will be used to perform discovery.

8. Select **Discover** to display the **Discovery Progress** page. The time it takes discovery to finish depends on many factors, such as the criteria specified and the configuration of the IT environment. If a large number (100 or more) of computers are being discovered or agents are being installed, the Operations console won't be usable during discovery and agent installation.

   > [!NOTE]
   > Computers that are already managed by the management group won't be returned by the wizard.

9. On the **Select Objects to Manage** page, do the following:

    1. Select the computers that you want to be agent-managed computers.

    2. In the **Management Mode** list, select **Agent** and then select **Next**.

        > [!NOTE]
        > The discovery results show virtual nodes of clusters. Don't select any virtual nodes to be managed.

10. On the **Summary** page, do the following:  

    
    1.  Leave the **Agent installation directory** set to the default of **%ProgramFiles%\Microsoft Monitoring Agent** or enter an installation path.

        > [!IMPORTANT]
        > If a different **Agent installation directory** is specified, the root of the path must exist on the targeted computer or the agent installation fails. Subdirectories, such as **\Agent**, are created if they don't exist.

    2. Leave **Agent Action Account** set to the default, **Local System**, or select **Other** and enter the **User name**, **Password**, and **Domain**. The Agent Action Account is the default account that the agent will use to perform actions.

    3. Select **Finish**.  

11. In the **Agent Management Task Status** dialog, the **Status** for each selected computer changes from **Queued** to **Success**; the computers are ready to be managed.

    > [!NOTE]
    > If the task fails for a computer, select the targeted computer. The reason for the failure is displayed in the **Task Output** text box.

12. Select **Close**.

## Next steps

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](~/scom/manage-deploy-windows-agent-manually.md).

- To deploy the agent with APM disabled using PowerShell, see [Deploy the agent with APM disabled using PowerShell](manage-deploy-windows-agent-manually.md#deploy-the-agent-with-apm-disabled-using-powershell).

- To learn how to upgrade the agent on Windows computers from a previous version, see [How to upgrade an agent to System Center Operations Manager](deploy-upgrade-agents.md).    

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](~/scom/manage-deploy-config-windows-agent.md).

- To understand what options and steps need to be performed to properly uninstall the agent from your Windows computers, review [Uninstall Agent from Windows-based Computers](~/scom/manage-uninstall-windows-agent.md).  

- If you would like to install the Nano Server agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](manage-deploy-windows-agent-nano.md)
