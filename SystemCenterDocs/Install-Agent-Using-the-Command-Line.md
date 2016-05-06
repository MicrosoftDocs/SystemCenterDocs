---
title: Install Agent Using the Command Line
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0569325-0e89-4633-8b6b-b900afbfda54
---
# Install Agent Using the Command Line
You can use MOMAgent.msi to deploy [!INCLUDE[om12long](./Token/om12long_md.md)] agents from the command line. Deploying agents from the command line is also referred to as a manual install.

Before you begin deployment, ensure the following conditions have been met:

-   The account that is used to run MOMAgent.msi must have administrative privileges on the computers on which you are installing agents.

-   A management group \(or single management server\) must be configured to accept agents installed with MOMAgent.msi or they will be automatically rejected and therefore not display in the Operations console. For more information, see [Process Manual Agent Installations](./Process-Manual-Agent-Installations.md). If the management group or server is configured to accept manually installed agents after the agents have been manually installed, the agents will display in the console after approximately one hour.

-   If an agent is manually deployed to a domain controller and an Active Directory management pack is later deployed, errors might occur during deployment of the management pack. To prevent errors from occurring before deploying the Active Directory management pack, or to recover from errors that might have already occurred, you need to deploy the Active Directory management pack helper object by running the file OomADs.msi on the affected domain controller. The file OomADs.msi is on the computer that is hosting the agent at C:\\Program Files\\System Center Operations Manager\\Agent\\HelperObjects. After an agent has been manually deployed to a domain controller, locate OomADs.msi and double\-click the file to install the Active Directory Management Pack helper object. The Active Directory Management Pack helper object is automatically installed when the agent is deployed using the Discovery Wizard.

-   Each agent that is installed with MOMAgent.msi must be approved for a management group.

MOMAgent.msi can be found in the Operations Manager installation media and the management server installation directory.

Use the following procedure to deploy an agent. For examples of ways in which you can customize the MOMAgent.msi command, see [Examples of Using MOMAgent Command to Manage Agents](./Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md).

### To deploy the Operations Manager agent from the command line

1.  Log on to the computer where you want to install the agent by using an account with local administrator privileges.

2.  Open a command window.

3.  Run the following command:

    ```

    %WinDir%\System32\msiexec.exe /i path\Directory\MOMAgent.msi /qn USE_SETTINGS_FROM_AD={0|1} USE_MANUALLY_SPECIFIED_SETTINGS={0|1} MANAGEMENT_GROUP=MGname MANAGEMENT_SERVER_DNS=MSname MANAGEMENT_SERVER_AD_NAME =MSname SECURE_PORT=PortNumber ACTIONS_USE_COMPUTER_ACCOUNT={0|1} ACTIONSUSER=UserName ACTIONSDOMAIN=DomainName ACTIONSPASSWORD=Password AcceptEndUserLicenseAgreement=1

    ```

    > [!NOTE]
    > Ensure you use the correct 32\-bit or 64\-bit version of MOMAgent.msi for the computer you are installing the agent on.

    where:

    |||
    |-|-|
    |USE\_SETTINGS\_FROM\_AD\={0&#124;1}|Indicates whether the management group settings properties will be set on the command line. Use 0 if you want to set the properties at the command line. Use 1 to use the management group settings from Active Directory.|
    |USE\_MANUALLY\_SPECIFIED\_SETTINGS\=\={0&#124;1}|If USE\_SETTINGS\_FROM\_AD\=1, then USE\_MANUALLY\_SPECIFIED\_SETTINGS must equal 0.|
    |MANAGEMENT\_GROUP\=*MGname*|Specifies the management group that will manage the computer.|
    |MANAGEMENT\_SERVER\_DNS\=*MSname*|Specifies the fully qualified domain name for the management server. To use a gateway server, enter the gateway server FQDN as **MANAGEMENT\_SERVER\_DNS**.|
    |MANAGEMENT\_SERVER\_AD\_NAME\=*ADname*|Use this parameter if the computer's DNS and Active Directory names differ to set to the fully qualified Active Directory Domain Services name.|
    |SECURE\_PORT\=*PortNumber*|Sets the health service port number.|
    |ENABLE\_ERROR\_REPORTING\={0&#124;1}|Optional parameter. Use this parameter with “1” to opt in to error report forwarding to Microsoft. If you do not include this parameter, the agent installation defaults to “0”, which opts out of error report forwarding.|
    |QUEUE\_ERROR\_REPORTS\={0&#124;1}|Optional parameter. Use this parameter with “1” to queue error reports or with “0” to send reports immediately. If you do not include this parameter, the agent installation defaults to “0”.|
    |INSTALLDIR\=*path*|Optional parameter. Use this parameter if you want to install the agent to a folder other than the default installation path. Note that \\Agent will be appended to this value.|
    |ACTIONS\_USE\_COMPUTER\_ACCOUNT\={0&#124;1}|Indicates whether to use a specified user account \(0\) or the Local System account \(1\).|
    |ACTIONSUSER\=*UserName*|Sets the Agent Action account to *UserName*. This parameter is required if you specified ACTIONS\_USE\_COMPUTER\_ACCOUNT\=0.|
    |ACTIONSDOMAIN\= *DomainName*|Sets the domain for the Agent Action account identified with the ACTIONSUSER parameter.|
    |ACTIONSPASSWORD\= *Password*|The password for the user identified with the ACTIONSUSER parameter.|
    |NOAPM\=1|Optional parameter. Installs the Operations Manager agent without .NET Application Performance Monitoring. If you are using [!INCLUDE[avicode57](./Token/avicode57_md.md)], NOAPM\=1 leaves the AVIcode agent in place. If you are using [!INCLUDE[avicode57](./Token/avicode57_md.md)] and install the Operations Manager agent by using momagent.msi without NOAPM\=1, the AVIcode agent will not work correctly and an alert will be generated.|
    |AcceptEndUserLicenseAgreement\=1|Used to specify that you accept the End User License Agreement \(EULA\).|

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
[Examples of Using MOMAgent Command to Manage Agents](./Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](./Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](./Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](./Uninstall-Agent-from-Windows-based-Computers.md)


