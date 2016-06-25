---
title: Upgrading and Uninstalling Agents on UNIX and Linux Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bf69867-ff73-48e0-b8b5-83b3b104b046
---
# Upgrading and Uninstalling Agents on UNIX and Linux Computers
This topic describes how to upgrade and uninstall agents on UNIX and Linux computers, using the **UNIX/Linux Agent Upgrade Wizard** and the **UNIX/Linux Agent Uninstall Wizard**. These wizards are similar in how you select the target computers and provide credentials. Both wizards require privileged credentials on the UNIX or Linux computers to complete their tasks, for more information see [Accessing UNIX and Linux Computers in Operations Manager](https://technet.microsoft.com/library/hh212886%28v=sc.12%29.aspx).

## Upgrading Agents
You must run the **UNIX/Linux Agent Upgrade Wizard** to upgrade agents from earlier versions, or when updates are issued by Microsoft, for of Operations Manager.

#### To Upgrade an Agent

1.  In the Operations Console click **Administration**.

2.  Click **UNIX/Linux Computers** in the **Device Management node**.

3.  In the **Actions** pane, click **Upgrade Agent** to start the **UNIX/Linux Agent Upgrade Wizard**.

4.  In the **Select Upgrade Targets** page, all applicable computers that have the installed agent will be selected by default for upgrade. Unselect any targets you do not want to upgrade.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use existing credentials and are alerted that one or more of the selected target computers does not have a Run As account assigned with the required profiles, you must do one of the following:

    -   Provide specified credentials with the **Provide upgrade credentials** option.

    -   Click **Show Computers** (in the alert text) for a list of the computers that do not have the required credentials specified in Run As Accounts. Then click **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](https://technet.microsoft.com/library/hh287150%28v=sc.12%29.aspx).

6.  Click **Upgrade**.

## Uninstalling Agents
You can uninstall an agent from the targeted computer by using the **UNIX/Linux Agent Uninstall Wizard**. For information on manually uninstalling agents, see [Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md).

#### To Uninstall an Agent

1.  In the Operations Console click **Administration**.

2.  Click **UNIX/Linux Computers** in the **Device Management** node.

3.  In the **Actions** pane, click **Uninstall Agent** to start the **UNIX/Linux Agent Uninstall Wizard**.

4.  In the **Select Uninstall Targets** page, all applicable computers that have the installed agent will be selected by default for uninstallation. Unselect any targets you do not want to uninstall.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use existing credentials and are alerted that one or more of the selected target computers does not have a Run As account assigned, you must do one of the following:

    -   Provide specified credentials with the **Provide uninstall credentials** option.

    -   Click **Show Computers** (in the alert text) for a list of the computers does not have the required credentials specified in Run As Accounts. Then click **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](https://technet.microsoft.com/library/hh287150%28v=sc.12%29.aspx).

6.  Click **Uninstall**.

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
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)


