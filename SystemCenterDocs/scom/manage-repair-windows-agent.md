---
ms.assetid: 
title: How to Repair an Agent
description: This article describes how to repair the installation of the Operations Manager agent on Windows computers.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 07/13/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: conceptual
---

# How to repair an agent
Use the one of the following procedures to repair the installation of the agent on agent-managed computers, including reconfiguration of the APM component for the System Center Operations Manager version 1807 agent from the Operations console.  

## To repair the installation of the agent by using the Operations console

1. Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  In the Administration pane, navigate to **Device Management\Agent Managed**.

4.  In the **Agent Managed** pane, select the one or more computers you want to repair the agent on, right-click them and then select **Repair**.

5.  In the **Repair Agents** dialog box, either leave **Use selected Management Server Action Account** selected or do the following:

    ::: moniker range="sc-om-1807"
    1. Select **Other user account**.
    
    2. Type the **User name** and **Password**, and type or select the **Domain** from the list. Select **This is a local computer account, not a domain account** if the account is a local computer account.

    >[!IMPORTANT]
    >The account must have administrative rights on the computer for the repair to succeed.

    3. Deselect the option **Install or keep APM** if you no longer intend to monitor a .NET web-based application or require the component installed on the targeted computer.  Otherwise, leave the option selected.  
    
    4. Click **Repair**.
    ::: moniker-end

    1. Select **Other user account**.
    
    2. Type the **User name** and **Password**, and type or select the **Domain** from the list. Select **This is a local computer account, not a domain account** if the account is a local computer account.

    >[!IMPORTANT]
    >The account must have administrative rights on the computer for the repair to succeed.

    3. Click **Repair**. 

4. In the **Agent Management Task Status** dialog box, the **Status** for each selected computer changes from **Queued** to **Success**; the computers are ready to be managed.

    > [!NOTE]
    > If the task fails for a computer, click the targeted computer. The reason for the failure is displayed in the **Task Output** text box.

5. Click **Close**.

## To repair the agent by using the MOMAgent.msi setup wizard

1. Log on to a managed computer with an account that is a member of the Administrators security group for the computer.

2. In **Control Panel**, click **Programs and Features**.

3. In **Programs and Features**, click **Change** for **Microsoft Monitoring Agent** setup.

4. In the **Agent Setup Wizard**, click Next.

5. In the **Program Maintenance** page, select **Repair**, and then click **Next**.

6. On the **Ready to Repair the Program** page, click **Install**.

7. On the **Completing the Microsoft Monitoring Agent Setup Wizard** page, click **Finish**.

8. Check the Application Event Log to confirm it completed successfully or for errors if the repair failed by searching at events from source **MsiInstaller**.
9. 
## To repair the agent by using MOMAgent.msi from the command line

1.  Log on to a managed computer with an account that is a member of the administrators security group for the computer.

2. Open a command prompt.

3. At the prompt, for example, type the following:

    **%WinDir%\System32\msiexec.exe /fomus <path>\MOMAgent.msi./qb** 

4. Check the Application Event Log to confirm it completed successfully or for errors if the repair failed by searching at events from source **MsiInstaller**.  

## Next steps

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](manage-deploy-config-windows-agent.md).
- 
- Review [Uninstall Agent from Windows-based Computers](manage-uninstall-windows-agent.md) to understand what options and steps need to be performed to properly uninstall  the agent from your Windows computers.  