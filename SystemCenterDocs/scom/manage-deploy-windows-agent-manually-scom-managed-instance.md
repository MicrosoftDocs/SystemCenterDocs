---
ms.assetid: 
title: Install Windows Agent Manually Using MOMAgent.msi - Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to manually install the Azure Monitor SCOM Managed Instance (preview) agent on Windows computers.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
<<<<<<< HEAD
ms.date: 02/15/2023
ms.custom: na
=======
ms.date: 02/13/2023
ms.custom: UpdateFrequency.5
>>>>>>> ed6e0d0e81fb9863880ed5724e461bdd92acf124
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Install Windows Agent Manually Using MOMAgent.msi - Azure Monitor SCOM Managed Instance (preview)

You can use *MOMAgent.msi* to deploy Azure Monitor SCOM Managed Instance (preview) agents from the command line or by manual installation. For a list of the supported operating system versions, see [System requirements](./connect-managed-instance-ops-console.md).

For either of the methods, ensure the following conditions are met:

-   The account that is used to run *MOMAgent.msi* must have administrative privileges on the computer on which you're installing the agent.

-   Each agent must be approved by a management group. For more information, see [Process Manual Agent Installations](manage-process-manual-agent-install.md).

-   If an agent is manually deployed to a domain controller and the Active Directory management pack is later deployed, errors might occur during deployment of the management pack. The Active Directory helper object is used by the Active Directory management pack on Windows domain controllers. To prevent errors from occurring or recover from errors already occurring, you need to manually install the Windows installer package OomADs.msi on the affected domain controller.  The file can be located on the domain controller in the *%ProgramFiles%\Microsoft Monitoring Agent\Agent\HelperObjects* folder.

- SCOM Managed Instance (preview) must be configured to accept agents installed with *MOMAgent.msi*, or they'll be automatically rejected and therefore not display in the Operations console. For more information, see [Process Manual Agent Installations](manage-process-manual-agent-install.md). If the managed instance is configured to accept manually installed agents after the agents have been manually installed, the agents will display in the console after approximately one hour.


> [!NOTE]
> For information about port requirements for agents, see [Communication Between Agents and Management Servers](plan-planning-agent-deployment.md#communication-between-agents-and-management-servers).

[Download the MOMAgent.msi](https://go.microsoft.com/fwlink/?linkid=2212475).

For more information about how to deploy the Operations Manager agent from the command line, see [Deploy the Operations Manager agent from the command line](./manage-deploy-windows-agent-manually.md#to-deploy-the-operations-manager-agent-from-the-command-line).


## Next steps

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md)

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
