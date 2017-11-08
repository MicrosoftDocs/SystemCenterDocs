---
ms.assetid: 58ebecd6-7f88-43bb-988b-6fdca37bf742
title: Upgrading and Uninstalling Agents on UNIX and Linux Computers
description: This article describes how to upgrade and uninstall the Operations Manager agent from UNIX and Linux computers.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Upgrading and uninstalling agents on UNIX and Linux computers

This topic describes how to upgrade and uninstall agents on UNIX and Linux computers, using the **UNIX/Linux Agent Upgrade Wizard** and the **UNIX/Linux Agent Uninstall Wizard**. These wizards are similar in how you select the target computers and provide credentials. Both wizards require privileged credentials on the UNIX or Linux computers to complete their tasks, for more information see [Planning Security Credentials for Accessing Unix and Linux Computers](plan-security-crossplat-credentials.md).

## Upgrading agents

You must run the **UNIX/Linux Agent Upgrade Wizard** to upgrade agents from earlier versions, or when updates are issued by Microsoft, for of Operations Manager.

#### To upgrade an agent

1.  In the Operations Console click **Administration**.

2.  Click **UNIX/Linux Computers** in the **Device Management node**.

3.  In the **Actions** pane, click **Upgrade Agent** to start the **UNIX/Linux Agent Upgrade Wizard**.

4.  In the **Select Upgrade Targets** page, all applicable computers that have the installed agent will be selected by default for upgrade. Unselect any targets you do not want to upgrade.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use existing credentials and are alerted that one or more of the selected target computers does not have a Run As account assigned with the required profiles, you must do one of the following:

    -   Provide specified credentials with the **Provide upgrade credentials** option.

    -   Click **Show Computers** (in the alert text) for a list of the computers that do not have the required credentials specified in Run As Accounts. Then click **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).

6.  Click **Upgrade**.

## Uninstalling agents

You can uninstall an agent from the targeted computer by using the **UNIX/Linux Agent Uninstall Wizard**. For information on manually uninstalling agents, see [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md).

#### To uninstall an agent

1.  In the Operations Console click **Administration**.

2.  Click **UNIX/Linux Computers** in the **Device Management** node.

3.  In the **Actions** pane, click **Uninstall Agent** to start the **UNIX/Linux Agent Uninstall Wizard**.

4.  In the **Select Uninstall Targets** page, all applicable computers that have the installed agent will be selected by default for uninstallation. Unselect any targets you do not want to uninstall.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use existing credentials and are alerted that one or more of the selected target computers does not have a Run As account assigned, you must do one of the following:

    -   Provide specified credentials with the **Provide uninstall credentials** option.

    -   Click **Show Computers** (in the alert text) for a list of the computers does not have the required credentials specified in Run As Accounts. Then click **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).

6.  Click **Uninstall**.

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](manage-install-crossplat-agent-cmdline.md).

- To understand how to approve agents manually installed, review [Process Manual Agent Installations](~/vmm/install.md).

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](~/scom/manage-apply-overrides-object-discovery.md).

- Review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md) to understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers.



