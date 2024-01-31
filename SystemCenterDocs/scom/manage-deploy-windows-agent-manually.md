---
ms.assetid: 46f21e10-1ba5-4715-a99c-d4ceb861a093
title: Install Windows Agent Manually Using MOMAgent.msi
description: This article describes how to manually install the Operations Manager agent manually on Windows computers.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/17/2023
ms.custom: UpdateFrequency2, intro-installation, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Install Windows Agent Manually Using MOMAgent.msi

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

You can use `MOMAgent.msi` to deploy System Center Operations Manager agents from the command line or by using the Setup Wizard. Deploying agents from the command line is also referred to as a manual install. For a list of the supported operating system versions, see [Microsoft Monitoring Agent Operating System requirements](./system-requirements.md).

Before you use either method to manually deploy the agent, ensure the following conditions are met:

-   The account that is used to run MOMAgent.msi must have administrative privileges on the computer on which you're installing agent.

-   Each agent that is installed with the Setup Wizard or from the command line must be approved by a management group. For more information, see [Process Manual Agent Installations](manage-process-manual-agent-install.md).

-   If an agent is manually deployed to a domain controller and the Active Directory management pack is later deployed, errors might occur during deployment of the management pack. The Active Directory helper object is used by the Active Directory management pack on Windows domain controllers. The Active Directory Management Pack helper object is normally installed automatically when the agent is deployed using the Discovery Wizard. To prevent errors from occurring or recover from errors already occurring, you need to manually install the Windows installer package OomADs.msi on the affected domain controller. The file can be located on the domain controller in the *%ProgramFiles%\Microsoft Monitoring Agent\Agent\HelperObjects* folder.

-   A management group (or single management server) must be configured to accept agents installed with MOMAgent.msi, or they'll be automatically rejected and therefore not display in the Operations console. For more information, see [Process Manual Agent Installations](manage-process-manual-agent-install.md). If the management group or server is configured to accept manually installed agents after the agents have been manually installed, the agents will display in the console after approximately one hour.


> [!NOTE]
> For information about port requirements for agents, see [Communication Between Agents and Management Servers](plan-planning-agent-deployment.md#communication-between-agents-and-management-servers).

::: moniker range="sc-om-2016"
MOMAgent.msi can be found in the Operations Manager installation media and in the following folder on a System Center - Operations Manager management server *%ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\AgentManagement\<platform\>*.  
::: moniker-end

::: moniker range=">=sc-om-1801"
MOMAgent.msi can be found in the Operations Manager installation media and in the following folder on a System Center - Operations Manager management server - *%ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\<platform\>*.
::: moniker-end

::: moniker range=">=sc-om-2016 <=sc-om-1801"
> [!IMPORTANT]
>  The Application Performance Monitoring (APM) feature in System Center 2016 Operations Manager and version 1801 agent causes a crash with IIS Application Pools that are running under the .NET Framework 2.0 runtime. By default when the agent is installed on a Windows computer, the APM components are installed by default. To avoid issues and prevent installation of the APM components on target Windows servers when you deploy the agent, add the `NOAPM=true` parameter
::: moniker-end

## Deploy the Operations Manager agent with the Agent Setup Wizard

Follow these steps to deploy the Operations Manager agent with the Agent Setup Wizard:

1.  Use local administrator privileges to sign in to the computer where you want to install the agent.

2.  On the Operations Manager installation media, double-click **Setup.exe**.

3.  In **Optional Installations**, select **Local agent**.

4.  On the **Welcome** page, select **Next**.

5.  On the **Important Notice** page, review the Microsoft software license terms and select **I Agree**.

6.  On the **Destination Folder** page, leave the installation folder set to the default, or select **Change** and type a path, and select **Next**.

6.  On the **Agent Setup Options** page, you can choose whether you want to **connect the agent to Operations Manager**. When you connect the agent to Operations Manager, you can manually choose the management group that this agent will participate with in monitoring. If you don't select this option, the agent can still collect Application Performance Monitoring data locally. You can change your selection in the **Monitoring Agent** item in Control Panel.  

7.  On the **Management Group Configuration** page, do the following:

    a. Enter the name of the management group in the **Management Group Name** field and the (which server?) server name in the **Management Server** field.

       > [!NOTE]
       > To use a gateway server, enter the gateway server name in the **Management Server** text box.

    b. Enter a value for **Management Server Port**, or leave the default of 5723.

    c. Enter **Next**.

8.  On the **Agent Action Account** page, leave it set to the default of **Local System**, or select **Domain or Local Computer Account**; enter the **User Account**, **Password**, and **Domain or local computer**; and select **Next**.

9. On the **Ready to Install** page, review the settings and select **Install** to display the **Installing Microsoft Monitoring Agent** page.

11. When the **Completing the Microsoft Monitoring Agent Setup Wizard** page appears, select **Finish**.

## Deploy the Operations Manager agent from the command line

Follow these steps to deploy the Operations Manager agent from the command line:

1.  Sign in to the computer where you want to install the agent by using an account with local administrator privileges.

2.  Open a command prompt as an administrator.

3.  Run the following command:

    ```

    %WinDir%\System32\msiexec.exe /i path\Directory\MOMAgent.msi /qn USE_SETTINGS_FROM_AD={0|1} USE_MANUALLY_SPECIFIED_SETTINGS={0|1} MANAGEMENT_GROUP=MGname MANAGEMENT_SERVER_DNS=MSname MANAGEMENT_SERVER_AD_NAME =MSname SECURE_PORT=PortNumber ACTIONS_USE_COMPUTER_ACCOUNT={0|1} ACTIONSUSER=UserName ACTIONSDOMAIN=DomainName ACTIONSPASSWORD=Password AcceptEndUserLicenseAgreement=1

    ```

    > [!NOTE]
    > Ensure you use the correct 32-bit or 64-bit version of MOMAgent.msi for the computer you're installing the agent on.

    where:

    |Parameter | Value|
    |-------------|-------------|
    |USE_SETTINGS_FROM_AD={0&#124;1}|Indicates whether the management group settings properties will be set on the command line. Use 0 if you want to set the properties at the command line. Use 1 to use the management group settings from Active Directory.|
    |USE_MANUALLY_SPECIFIED_SETTINGS=={0&#124;1}|If USE_SETTINGS_FROM_AD=1, then USE_MANUALLY_SPECIFIED_SETTINGS must equal 0.|
    |MANAGEMENT_GROUP=*MGname*|Specifies the management group that will manage the computer.|
    |MANAGEMENT_SERVER_DNS=*MSname*|Specifies the fully qualified domain name for the management server. To use a gateway server, enter the gateway server FQDN as **MANAGEMENT_SERVER_DNS**.|
    |MANAGEMENT_SERVER_AD_NAME=*ADname*|Use this parameter if the computer's DNS and Active Directory names differ to set to the fully qualified Active Directory Domain Services name.|
    |SECURE_PORT=*PortNumber*|Sets the health service port number.|
    |ENABLE_ERROR_REPORTING={0&#124;1}|Optional parameter. Use this parameter with **1** to opt in to error report forwarding to Microsoft. If you don't include this parameter, the agent installation defaults to **0**, which opts out of error report forwarding.|
    |QUEUE_ERROR_REPORTS={0&#124;1}|Optional parameter. Use this parameter with **1** to queue error reports or with **0** to send reports immediately. If you don't include this parameter, the agent installation defaults to **0**.|
    |INSTALLDIR=*path*|Optional parameter. Use this parameter if you want to install the agent to a folder other than the default installation path. Note that \Agent will be appended to this value.|
    |ACTIONS_USE_COMPUTER_ACCOUNT={0&#124;1}|Indicates whether to use a specified user account (0) or the Local System account (1).|
    |ACTIONSUSER=*UserName*|Sets the Agent Action account to *UserName*. This parameter is required if you specified ACTIONS_USE_COMPUTER_ACCOUNT=0.|
    |ACTIONSDOMAIN= *DomainName*|Sets the domain for the Agent Action account identified with the ACTIONSUSER parameter.|
    |ACTIONSPASSWORD= *Password*|The password for the user identified with the ACTIONSUSER parameter.|
    |NOAPM=1|Optional parameter. Installs the Operations Manager agent without .NET Application Performance Monitoring. If you're using AVIcode 5.7, NOAPM=1 leaves the AVIcode agent in place. If you're using AVIcode 5.7 and install the Operations Manager agent by using momagent.msi without NOAPM=1, the AVIcode agent won't work correctly and an alert will be generated.|
    |AcceptEndUserLicenseAgreement=1|Used to specify that you accept the End User License Agreement (EULA). This parameter is required when you use /qn to perform a fully silent installation of the agent.|


## Examples of installing the agent from the command line

The following examples show different ways in which you can install the MOMAgent.msi Windows Installer package manually from the command line. You can perform new installations of agents, upgrade agents from previous releases of Operations Manager, uninstall the agent, or change the configuration of an agent (such as the management group or management server associated with the agent).

### Agent installation using a specific Action Account

The following example shows a fresh installation of an agent and uses a specific Action Account.

```
msiexec.exe /i path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentinstall.log USE_SETTINGS_FROM_AD=0 MANAGEMENT_GROUP=<MG_Name> MANAGEMENT_SERVER_DNS=<MSDNSName> MANAGEMENT_SERVER_AD_NAME=<MSDNSName> ACTIONS_USE_COMPUTER_ACCOUNT=0 ACTIONSUSER=<AccountUser> ACTIONSDOMAIN=<AccountDomain> ACTIONSPASSWORD=<AccountPassword> USE_MANUALLY_SPECIFIED_SETTINGS=1 AcceptEndUserLicenseAgreement=1

```

### Agent installation using the Local System account

The following example shows a fresh installation of an agent and uses the Local System for the Action Account.

```
msiexec.exe /i path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentinstall.log USE_SETTINGS_FROM_AD=0 MANAGEMENT_GROUP=<MG_Name> MANAGEMENT_SERVER_DNS=<MSDNSName> MANAGEMENT_SERVER_AD_NAME=<MSDNSName> ACTIONS_USE_COMPUTER_ACCOUNT=1 USE_MANUALLY_SPECIFIED_SETTINGS=1 AcceptEndUserLicenseAgreement=1

```

### Agent installation with Active Directory integration and using a specific Action Account

The following example installs an agent by using Active Directory and a specific Action Account.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentInstall.log USE_SETTINGS_FROM_AD=1 USE_MANUALLY_SPECIFIED_SETTINGS=0 ACTIONS_USE_COMPUTER_ACCOUNT=0 ACTIONSUSER=<AccountUser> ACTIONSDOMAIN=<AccountDomain> ACTIONSPASSWORD=<AccountPassword> AcceptEndUserLicenseAgreement=1

```

### Agent installation with Active Directory integration and using the Local System account

The following example installs an agent by using Active Directory and the Local system account for the Action Account.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentInstall.log USE_SETTINGS_FROM_AD=1 ACTIONS_USE_COMPUTER_ACCOUNT=1 USE_MANUALLY_SPECIFIED_SETTINGS=0 AcceptEndUserLicenseAgreement=1

```

### Agent upgrade from a previous release of Operations Manager

The following example upgrades an agent.

```
msiexec /i path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentUpgrade.log AcceptEndUserLicenseAgreement=1

```

### Uninstall the agent

The following example uninstalls an agent.

```
msiexec /x path\Directory\MOMAgent.msi /qn /l*v %temp%\OMAgentUninstall.log

```

## Deploy the agent with APM disabled using PowerShell

The following example shows how you install the Windows agent from PowerShell with the Application Performance Monitoring (APM) component disabled.

```
$PrimaryMS = Get-SCOMManagementServer -Name <MSDNSName>
Install-SCOMAgent -DNSHostName 'ComputerA.contoso.com' -PrimaryManagementServer $PrimaryMS -NoAPM

```

## Repair the agent and disable APM using PowerShell

The following example shows how you repair the Windows agent from PowerShell and disable the Application Performance Monitoring (APM) component.

```
Get-SCOMAgent -DNSHostName "ComputerA.contoso.net" | Repair-SCOMAgent -NoAPM

```

## Next steps

- To deploy the Windows agent from the Operations console using the Discovery Wizard, review [Install Agent on Windows Using the Discovery Wizard](~/scom/manage-deploy-windows-agent-console.md).

- If you would like to install the Nano Server agent using the Discovery Wizard, from the command line or automate the deployment using a script or other automation solution, review [Install Agent on Nano Server](manage-deploy-windows-agent-nano.md).

- To learn how to upgrade the agent on Windows computers from a previous version, see [How to upgrade an agent to System Center Operations Manager](deploy-upgrade-agents.md).

- To understand how to manage the configuration settings of a Windows agent and options available, review [Configuring Windows Agents](~/scom/manage-deploy-config-windows-agent.md).

- To understand what options and steps need to be performed to properly uninstall  the agent from your Windows computers, review [Uninstall Agent from Windows-based Computers](~/scom/manage-uninstall-windows-agent.md).
