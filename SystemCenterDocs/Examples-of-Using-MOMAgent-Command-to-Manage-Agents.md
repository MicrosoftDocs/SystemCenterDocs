---
title: Examples of Using MOMAgent Command to Manage Agents
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7fb8119-565a-4796-a639-5051a9c52a75
---
# Examples of Using MOMAgent Command to Manage Agents
The following examples show different ways in which you can use the MOMAgent command. You can use this command to perform new installations of agents, upgrade agents from previous releases of Operations Manager, or change the configuration of an agent \(such as the management group or management server associated with the agent\).

### Agent installation using a specific Action Account
The following example shows a fresh installation of an agent and uses a specific Action Account.

```
msiexec.exe /i path\Directory\MOMAgent.msi /qn /l*v %temp% MOMAgentinstall.log USE_SETTINGS_FROM_AD=0 MANAGEMENT_GROUP=<MG_Name> MANAGEMENT_SERVER_DNS=<MSDNSName> MANAGEMENT_SERVER_AD_NAME=<MSDNSName> ACTIONS_USE_COMPUTER_ACCOUNT=0 ACTIONSUSER=<AccountUser> ACTIONSDOMAIN=<AccountDomain> ACTIONSPASSWORD=<AccountPassword> USE_MANUALLY_SPECIFIED_SETTINGS=1

```

### Agent installation using the Local System account
The following example shows a fresh installation of an agent and uses the Local System for the Action Account.

```
msiexec.exe /i path\Directory\MOMAgent.msi /qn /l*v %temp%\MOMAgentinstall.log USE_SETTINGS_FROM_AD=0 MANAGEMENT_GROUP=<MG_Name> MANAGEMENT_SERVER_DNS=<MSDNSName> MANAGEMENT_SERVER_AD_NAME=<MSDNSName> ACTIONS_USE_COMPUTER_ACCOUNT=1 USE_MANUALLY_SPECIFIED_SETTINGS=1

```

### Agent installation with Active Directory integration and using a specific Action Account
The following example installs an agent by using Active Directory and a specific Action Account.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%mominst.NoGroupSpecified.log USE_SETTINGS_FROM_AD=1 USE_MANUALLY_SPECIFIED_SETTINGS=0 ACTIONS_USE_COMPUTER_ACCOUNT=0 ACTIONSUSER=<AccountUser> ACTIONSDOMAIN=<AccountDomain> ACTIONSPASSWORD=<AccountPassword>

```

### Agent installation with Active Directory integration and using the Local System account
The following example installs an agent by using Active Directory and the Local system account for the Action Account.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%\ mominst.NoGroupSpecified.log USE_SETTINGS_FROM_AD=1 ACTIONS_USE_COMPUTER_ACCOUNT=1 USE_MANUALLY_SPECIFIED_SETTINGS=0

```

### Agent upgrade from a previous release of Operations Manager
The following example upgrades an agent.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%\MOMAgentUpgrade.log

```

### Uninstall the agent
The following example uninstalls an agent.

```
msiexec /x path\Directory\MOMAgent.msi /qn %temp%\MOMAgentUpgrade.log

```

## See Also
[Operations Manager Agent Installation Methods](./Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](./Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](./Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](./Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](./Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](./Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Process Manual Agent Installations](./Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](./Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](./Configuring-Agents.md)
[Install Agent Using the Command Line](./Install-Agent-Using-the-Command-Line.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](./Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](./Uninstall-Agent-from-Windows-based-Computers.md)


