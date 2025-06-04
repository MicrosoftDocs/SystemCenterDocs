---
ms.assetid: 58ebecd6-7f88-43bb-988b-6fdca37bf742
title: Upgrading and Uninstalling Agents on UNIX and Linux Computers
description: This article describes how to upgrade and uninstall the Operations Manager agent from UNIX and Linux computers.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Upgrading and uninstalling agents on UNIX and Linux computers



This article describes how to upgrade and uninstall agents on UNIX and Linux computers using the **UNIX/Linux Agent Upgrade Wizard** and the **UNIX/Linux Agent Uninstall Wizard**. These wizards are similar in how you select the target computers and provide credentials. Both wizards require privileged credentials on the UNIX or Linux computers to complete their tasks. For more information, see [Planning Security Credentials for Accessing Unix and Linux Computers](plan-security-crossplat-credentials.md).

## Upgrading agents

You must run the **UNIX/Linux Agent Upgrade Wizard** to upgrade agents from earlier versions, or when updates are issued by Microsoft for Operations Manager.

#### To upgrade an agent

1.  In the Operations Console, select **Administration**.

2.  Select **UNIX/Linux Computers** in the **Device Management node**.

3.  In the **Actions** pane, select **Upgrade Agent** to start the **UNIX/Linux Agent Upgrade Wizard**.

4.  In the **Select Upgrade Targets** page, all applicable computers that have the installed agent will be selected by default for upgrade. Unselect any targets you don't want to upgrade.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use the existing credentials and are alerted that one or more of the selected target computers doesn't have a Run As account assigned with the required profiles, you must do one of the following:

    -   Provide specified credentials with the **Provide upgrade credentials** option.

    -   Select **Show Computers** (in the alert text) for a list of the computers that don't have the required credentials specified in Run As Accounts. Then select **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).

6.  Select **Upgrade**.

## Uninstalling agents

You can uninstall an agent from the targeted computer by using the **UNIX/Linux Agent Uninstall Wizard**. For information on manually uninstalling agents, see [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md).

#### To uninstall an agent

1.  In the Operations Console, select **Administration**.

2.  Select **UNIX/Linux Computers** in the **Device Management** node.

3.  In the **Actions** pane, select **Uninstall Agent** to start the **UNIX/Linux Agent Uninstall Wizard**.

4.  In the **Select Uninstall Targets** page, all the applicable computers that have the installed agent will be selected by default for uninstallation. Unselect any targets you don't want to uninstall.

5.  On the **Credentials** page, select one of the credentials options.

    If you select the option to use existing credentials and are alerted that one or more of the selected target computers doesn't have a Run As account assigned, you must do one of the following:

    -   Provide specified credentials with the **Provide uninstall credentials** option.

    -   Select **Show Computers** (in the alert text) for a list of computers that don't have the required credentials specified in Run As Accounts. Then select **Previous** to unselect them and try again.

    For detailed instructions on how to set credentials, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).

6.  Select **Uninstall**.

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](manage-install-crossplat-agent-cmdline.md).

- To understand how to approve agents manually installed, review [Process Manual Agent Installations](../vmm/install.md).

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](~/scom/manage-apply-overrides-object-discovery.md).

- To understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers, review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md).
