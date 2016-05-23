---
title: Process Manual Agent Installations
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba2a2815-10bf-4904-ae1c-1e572e2b5fa5
---
# Process Manual Agent Installations
Manual installation of an agent refers to the process of running MOMAgent.msi locally on a computer that is to host a [!INCLUDE[om12long](../../Token/om12long_md.md)] agent. When it is installed, the agent attempts to join the specified management group by contacting a specified management server. You can use security settings at both the management group and the management server level to configure how requests from manually installed agents are processed.

The following three options are available to process manually installed agents.

|Option|Action|
|----------|----------|
|**Reject new manual agent installations**|Designates that all requests from a manually installed agent will be denied by [!INCLUDE[om12short](../../Token/om12short_md.md)]. This is the most secure setting and is selected by default.|
|**Review new manual agent installations in pending management view**|Designates that all requests from a manually installed agent will be directed to Pending Management before being allowed to join the management group. An administrator must review the request and manually approve the agents' request.|
|**Auto\-approve new manually installed agents**|This option is available only if **Review new manual agent installations in pending management view** has been selected. This setting causes [!INCLUDE[om12short](../../Token/om12short_md.md)] to automatically allow any manually installed agent to join the management group. This is the least secure option.|

> [!IMPORTANT]
> A management group or management server must be configured to accept agents that are installed with MOMAgent.msi or they will be automatically rejected and therefore not displayed in the Operations console. If a management group is configured to accept manually installed agents, the agents will display in the console approximately one hour after they are installed.

The following procedures show you how to configure settings for manual agent installations.

### To configure manual agent installation settings for a management group

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  In the Administration workspace, expand **Administration**, and then click **Settings**.

4.  In the **Settings** pane, expand **Type: Server**, right\-click **Security**, and then click **Properties**.

5.  In the **Global Management Server Settings \- Security** dialog box, on the **General** tab, do one of the following:

    -   To maintain a higher level of security, click **Reject new manual agent installations**, and then click **OK**.

    -   To configure for manual agent installation, click  **Review new manual agent installations in pending management view**, and then click **OK**.

    -   Optionally, select **Auto\-approve new manually installed agents**.

### To override the manual agent installation setting for a single management server

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  In the **Administration** workspace, expand **Administration**, expand **Device Management**, and then click **Management Servers**.

4.  In the results pane, right\-click the management server that you want to view the properties of, and then click **Properties**.

5.  In the **Management Server Properties** dialog box, click the **Security** tab.

6.  On the **Security** tab, do the following:

    -   To maintain a higher level of security, select **Reject new manual agent installations**, and then click **OK**.

    -   To configure for manual agent installation, click **Review new manual agent installations in pending management view**, and then click **OK**.

    -   Optionally, select **Auto\-approve new manually installed agents**.

7.  Click **OK**.

### To approve a pending agent installation when automatic approval is not configured

1.  In the Operations console, click **Administration**.

2.  Click **Pending Management**.

3.  In the **Pending Management** pane, select computers in **Type: Manual Agent Install**.

4.  Right\-click the computers, and then click **Approve**.

5.  In the **Manual Agent Install** dialog box, click **Approve**. The computers now appear in the **Agent Managed** node and are ready to be managed.

    > [!NOTE]
    > Rejected agents remain in  **Pending Management**  until the agent is uninstalled for the management group.

## See Also
[Operations Manager Agent Installation Methods](Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](Configuring-Agents.md)
[Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)


