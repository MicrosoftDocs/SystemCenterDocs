---
ms.assetid: 
title:  Install agent and certificate on Linux computers using the command line
description: This article describes the new Linux agent and how to install manually on System Center Preview 1711 - Operations Manager.    
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/3/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# Install agent and certificate on Linux computers using the command line
This article provides details of the latest version of the Linux agent for System Center  Preview 1711 - Operations Manager and the process for installing it. 

This version of the Linux agent supports [Fluentd](https://www.fluentd.org/), an open source data collector for Linux that collects data from a variety of sources.  The existing OMI based monitoring for currently supported Linux workloads will continue to work without change.

## What's new in this Technical Preview 
1. A new converter plugin is included that enables customers to use third party plugins for Operations Manager log file monitoring.
2. Added support to Server Authentication.
3. Added support to additional Linux distros.


## Supported platforms
The Linux distributions in the following table are supported in this technical preview.

| Linux Operating System | Version Supported |
|:---|:---|
| Red Hat Enterprise Linux Server | 5 (x86/x64)<br>6 (x86/x64)<br>7 (x86/x64) |
| Cent OS | 5 (x86/x64)<br>6 (x86/x64)<br>7 (x64) |
| Ubuntu | 12.04 LTS (x86/x64)<br>14.04 LTS (x86/x64)<br>16.04 LTS (x86/x64) |
| Debian | 6 (x86/x64)<br>7 (x86/x64)<br>8 (x86/x64) |
| Oracle Linux | 5 (x86/x64)<br>6 (x86/x64)<br>7 (x64) |
| SUSE Linux Enterprise Server | 11 (x86/x64)<br>12 (x64) |
Technical preview will only support new installations. Upgrade from existing SCOM/OMS agents is not currently supported. 

## Agent installation

You can choose to install the latest version of the Linux agent for Operations Manager using automatic discovery or manual installation.  Automatic discovery hasn't changed since the previous version, and you can follow the same procedure at [Discover and install agent on UNIX and Linux](manage-deploy-crossplat-agent-console.md).

Use the following procedures to manually install agents to UNIX and Linux computers. The agent packages can be found in the the following folder on a management server - %ProgramFiles%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits after you import the required management packs for the specific version of UNIX/Linux you need to monitor. The management pack are available in the Operations Manager installation media, in the \ManagementPacks directory.

## Manual installation
The agent is provided as a self-extracting, installable shell script bundle. This bundle contains both Debian and RPM packages for each of the agent components and can be installed directly or extracted to retrieve the individual packages. Separate bundles are available for x64 and x86 architectures. 

The following sections describe the steps required to manually install the Linux agent.

### Install agent
1. The agent install bundles will be located in **%Program Files%\Microsoft System Center\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits**.  Transfer the appropriate bundle (x86 or x64) to the Linux computer, using scp/sftp.
2. Install the bundle with the following command.  The **enable-opsmgr** parameter ensures that port 1270 is open for the management server to communicate with the agent.

    sudo sh ./omsagent-1.4.0-45.universald.1.x64.sh --install --enable-opsmgr

1. Run the omsadmin.sh command supplying **scom** for your workspace id.  This command must be run as root (with sudo elevation). This script will generate a certificate at **/etc/opt/microsoft/omsagent/scom/certs/scom-cert.pem** which will need to be signed by the Management Server in a later step.

    /opt/microsoft/omsagent/bin/omsadmin.sh -w scom

2. Create a configuration file called **omsadmin.conf** in **/etc/opt/microsoft/omsagent/scom/conf/** with the following contents.  Fill in the name of the machine and use **8886** for the port of the OMED service.

    WORKSPACE_ID=scom
    SCOM_ENDPOINT=https://<FQDN_OF_OM_MACHINE>:<PORT_OF_OMED_SERVICE>

### Configure certificates
In the previous version of the Linux agent, the management server accessed each Linux computer with a server authentication certificate.  With the new agent, Fluentd acts as the client accessing the management server, so the certificate requires client authentication.  You need to obtain a new certificate to work with the new agent. Operations Manager will use the new certificate for Fluentd communications and the old certificate for other communications.

1. Locate**/etc/opt/omi/ssl/omi-host-<hostname>.pem** and **/etc/opt/microsoft/omsagent/scom/certs/scom-cert.pem** on the Linux computer and copy them to any location on the management server.  
4. Open a command prompt on the management server and run the following command to sign your certificate.

    scxcertconfig -sign omi-host-<hostname>.pem omi_new.pem and scxcertconfig -sign scom-cert.pem scom-cert_new.pem

5.  Copy the file - **omi_new.pem** to **/etc/opt/omi/ssl/** and **scom-cert_new.pem** to **/etc/opt/microsoft/omsagent/scom/certs/** on the Linux computer.  Remove the old certificate files and rename the new certificate files to replace them.

### Restart the agent

1. Restart the agent with the following command.

    scxadmin –restart


### Discovery
After you have manually deployed agents to UNIX and Linux computers, they still need to be discovered by Operations Manager by using the Discovery Wizard. For the Discovery type, select Discover only computers with the UNIX/Linux agent installed. For more information see [Install Agent on UNIX and Linux using the Discovery Wizard](manage-deploy-crossplat-agent-console.md).

Next steps
- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](manage-apply-overrides-object-discovery.md).
- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](manage-upgrade-uninstall-crossplat-agent.md).
- Review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md) to understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers. 