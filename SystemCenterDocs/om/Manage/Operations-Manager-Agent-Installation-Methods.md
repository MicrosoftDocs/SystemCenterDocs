---
title: Operations Manager Agent Installation Methods
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc9ac08d-1643-4573-a17b-73001d0ac97e
---
# Operations Manager Agent Installation Methods
An Operations Manager *agent* is a service that is installed on a computer. The agent collects data, compares sampled data to predefined values, creates alerts, and runs responses. A management server receives and distributes configurations to agents on monitored computers. There are several methods you can use to install an Operations Manager agent on a computer.

To install the agent by using the Discovery Wizard, firewall ports must be open on the agent-managed computers.  Also, you must have an account that is a local administrator on the computer on which you want to install the agent.

> [!NOTE]
> For information about port requirements for agents, see [Agents and Agentless Monitoring in Operations Manager](https://technet.microsoft.com/en-us/library/hh212910.aspx) in the Operations Manager 2012 Deployment Guide.

Agents that are installed by using the Discovery Wizard can be managed from the Operations console, such as updating agent versions, applying patches, and configuring the management server that the agent reports to.

When you install the agent using a manual method, updates to the agent must also be performed manually. You will be able to use Active Directory integration to assign agents to management groups. For more information, see [Integrating Active Directory and Operations Manager](https://technet.microsoft.com/en-us/library/hh212829.aspx)

## Agent Installation Methods

> [!NOTE]
> -   You can use the Discovery Wizard in the Operations console, sometimes called a *push installation*. (All other methods are considered manual installations.) This method works for computers running Windows, UNIX, and Linux operating systems.
> -   You can run the Setup Wizard from the Operations Manager installation media and install the agent directly on a computer running Windows.
> -   You can install an agent directly on a computer running Windows, UNIX, and Linux operating systems by using a command line.

[Install the Agent Using the Discovery Wizard](Install-the-Agent-Using-the-Discovery-Wizard.md)

[Install the Agent Using the Command Line](Install-the-Agent-Using-the-Command-Line.md)

[Install the Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-the-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)

[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)


