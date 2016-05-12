---
title: Managing Certificates for UNIX and Linux Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41f74547-a776-414c-80d9-9b8dbb93a1e0
---
# Managing Certificates for UNIX and Linux Computers
With [!INCLUDE[om12long](Token/om12long_md.md)], you can deploy agents to UNIX or Linux computers. Kerberos authentication is not possible. Therefore, certificates are used between the management server and the UNIX or Linux computers. In this scenario, the certificates are self\-signed by the management server. \(Although it is possible to use third\-party certificates, they are not needed.\)

There are two methods you can use to deploy agents. You can use the Discovery Wizard or you can manually install an agent. Of these two methods, manually installing an agent is the more secure option. When you use the Discovery Wizard to push agents to UNIX or Linux computers, you trust that the computer that you are deploying to is really the computer that you think it is. When you use the Discovery Wizard to deploy agents, it involves greater risk than when you deploy to computers on the public network or in a perimeter network.

When you use the Discovery Wizard to deploy an agent, the Discovery Wizard performs the following functions:

|||
|-|-|
|Deployment|The Discovery Wizard copies the agent package to the UNIX or Linux computer and then starts the installation process.|
|Certificate Signing|Operations Manager retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.|
|Discovery|The Discovery Wizard discovers the computer and tests to see that the certificate is valid. If the Discovery Wizard verifies that the computer can be discovered and that the certificate is valid, the Discovery Wizard adds the newly discovered computer to the Operations Manager database.|

When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard: deployment and certificate signing. Then, you use the Discovery Wizard to add the computer to the Operations Manager database.

If there are existing certificates on the system, they are reused during agent installation. New certificates are not created. Certificates are not automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the \/etc\/opt\/microsoft\/scx\/ssl folder. To regenerate the certificates during instalation, you must remove this folder before agent installation.

For instructions on how to manually deploy an agent, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md), and then use the following procedure to install the certificates.

## UNIX and Linux Firewall Considerations
If you have a firewall on your UNIX or Linux computer, you must open port 1270 \(inbound\). This port number is not configurable. If you are deploying agents in a low security environment and you use the Discovery Wizard to deploy and sign the certificates, you must open the SSH port. The SSH port number is configurable. By default, SSH uses inbound TCP port 22.

## See Also
[Operations Manager Agent Installation Methods](Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Process Manual Agent Installations](Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](Configuring-Agents.md)
[Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)


