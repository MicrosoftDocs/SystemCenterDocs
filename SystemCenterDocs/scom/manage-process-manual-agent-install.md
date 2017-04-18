---
ms.assetid: 017e8bb1-e523-4cc0-bf0c-2d1d4697db11
title: Process Manual Agent Installations
description: This article describes how to process Operations Manager agents deployed manually.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Process manual agent installations

>Applies To: System Center 2016 - Operations Manager

Manual installation of an agent refers to the process of running MOMAgent.msi locally on a computer that is to host a System Center Operations Manager agent. When it is installed, the agent attempts to join the specified management group by contacting a specified management server. You can use security settings at both the management group and the management server level to configure how requests from manually installed agents are processed.

The following three options are available to process manually installed agents.

|Option|Action|
|----------|----------|
|**Reject new manual agent installations**|Designates that all requests from a manually installed agent will be denied by Operations Manager. This is the most secure setting and is selected by default.|
|**Review new manual agent installations in pending management view**|Designates that all requests from a manually installed agent will be directed to Pending Management before being allowed to join the management group. An administrator must review the request and manually approve the agents' request.|
|**Auto-approve new manually installed agents**|This option is available only if **Review new manual agent installations in pending management view** has been selected. This setting causes Operations Manager to automatically allow any manually installed agent to join the management group. This is the least secure option.|

> [!IMPORTANT]
> A management group or management server must be configured to accept agents that are installed with MOMAgent.msi or they will be automatically rejected and therefore not displayed in the Operations console. If a management group is configured to accept manually installed agents, the agents will display in the console approximately one hour after they are installed.

The following procedures show you how to configure settings for manual agent installations.

## To configure manual agent installation settings for a management group

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  In the Administration workspace, expand **Administration**, and then click **Settings**.

4.  In the **Settings** pane, expand **Type: Server**, right-click **Security**, and then click **Properties**.

5.  In the **Global Management Server Settings - Security** dialog box, on the **General** tab, do one of the following:

    -   To maintain a higher level of security, click **Reject new manual agent installations**, and then click **OK**.

    -   To configure for manual agent installation, click  **Review new manual agent installations in pending management view**, and then click **OK**.

    -   Optionally, select **Auto-approve new manually installed agents**.

## To override the manual agent installation setting for a single management server

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  In the **Administration** workspace, expand **Administration**, expand **Device Management**, and then click **Management Servers**.

4.  In the results pane, right-click the management server that you want to view the properties of, and then click **Properties**.

5.  In the **Management Server Properties** dialog box, click the **Security** tab.

6.  On the **Security** tab, do the following:

    -   To maintain a higher level of security, select **Reject new manual agent installations**, and then click **OK**.

    -   To configure for manual agent installation, click **Review new manual agent installations in pending management view**, and then click **OK**.

    -   Optionally, select **Auto-approve new manually installed agents**.

7.  Click **OK**.

## To approve a pending agent installation when automatic approval is not configured

1.  In the Operations console, click **Administration**.

2.  Click **Pending Management**.

3.  In the **Pending Management** pane, select computers in **Type: Manual Agent Install**.

4.  Right-click the computers, and then click **Approve**.

5.  In the **Manual Agent Install** dialog box, click **Approve**. The computers now appear in the **Agent Managed** node and are ready to be managed.

    > [!NOTE]
    > Rejected agents remain in  **Pending Management**  until the agent is uninstalled for the management group.

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md).

- If you would like to manually install the Windows agent from the command line or automate the deployment using a script or other automation solution, review [Install Windows Agent Manually Using MOMAgent.msi](~/scom/manage-deploy-windows-agent-manually.md).

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](~/scom/manage-deploy-config-windows-agent.md).

- Review [Uninstall Agent from Windows-based Computers](~/scom/manage-uninstall-windows-agent.md) to understand what options and steps need to be performed to properly uninstall  the agent from your Windows computers.  

- If you would like to install the Nano Server agent from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](~/scom/manage-deploy-windows-agent-nano.md)

