---
ms.assetid: 332a9aa5-3176-4f39-b854-5a9817997eb5
title: Managing Certificates for UNIX and Linux Computers
description: This article describes how to manage certificates required for authentication with UNIX and Linux computers with Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 03/21/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Managing certificates for UNIX and Linux computers

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

With System Center Operations Manager, you can deploy agents to UNIX or Linux computers. Kerberos authentication is not possible. Therefore, certificates are used between the management server and the UNIX or Linux computers. In this scenario, the management server acts as a standalone certificate authority. (Although it is possible to use third-party certificates, they are not needed.)

::: moniker range="sc-om-2022"

Prior to Operations Manager 2016, the Linux Agent used to generate certificates and encrypt it with SHA1. From 2016, the Linux Agent generates a SHA1 certificate and then, as part of the discovery process, the certificate gets encrypted with SHA256.

With Operations Manager 2022, the certificate gets encrypted with SHA256.

::: moniker-end

There are two methods you can use to deploy agents. You can use the Discovery Wizard or you can manually install an agent. Of these two methods, manually installing an agent is the more secure option. When you use the Discovery Wizard to push agents to UNIX or Linux computers, you trust that the computer that you are deploying to is really the computer that you think it is. When you use the Discovery Wizard to deploy agents, it involves greater risk than when you deploy to computers on the public network or in a perimeter network.

When you use the Discovery Wizard to deploy an agent, the Discovery Wizard performs the following functions:

- Deployment - The Discovery Wizard copies the agent package to the UNIX or Linux computer and then starts the installation process.

- Certificate Signing - Operations Manager retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.

- Discovery - The Discovery Wizard discovers the computer and tests to see that the certificate is valid. If the Discovery Wizard verifies that the computer can be discovered and that the certificate is valid, the Discovery Wizard adds the newly discovered computer to the Operations Manager database.

When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard: deployment and certificate signing. Then, you use the Discovery Wizard to add the computer to the Operations Manager database.

If there are existing certificates on the system, they are reused during agent installation. New certificates are not created. Certificates are not automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the /etc/opt/microsoft/scx/ssl folder. To regenerate the certificates during installation, you must remove this folder before agent installation.

For instructions on how to manually deploy an agent, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](manage-install-crossplat-agent-cmdline.md), and then use the following procedure to install the certificates.

## UNIX and Linux firewall considerations

If you have a firewall on your UNIX or Linux computer, you must open port 1270 (inbound). This port number is not configurable. If you are deploying agents in a low security environment and you use the Discovery Wizard to deploy and sign the certificates, you must open the SSH port. The SSH port number is configurable. By default, SSH uses inbound TCP port 22.  For more information about firewall configuration for Operations Manager, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md)

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](manage-install-crossplat-agent-cmdline.md).

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md).

- Review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md) to understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers.
