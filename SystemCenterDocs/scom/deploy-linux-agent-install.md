---
ms.assetid: 
title:  Linux Agent for System Center Preview 1711 - Operations Manager
description: This article describes the new Linux agent and how to install it manually from the command-line.    
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

# Linux agent for Operations Manager
This article provides details of the latest version of the Linux agent for System Center  Preview 1711 - Operations Manager and the process for installing it. 

This version of the Linux agent supports [Fluentd](https://www.fluentd.org/) is an open source data collector for Linux that collects data from a variety of sources.  The existing OMI based monitoring for currently supported Linux workloads will continue to work without change.

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

Before performing either procedure, download and install the [management pack].

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
With the agent in place, you need to have Operations Manager perform a discovery to recognize the new agents.  

1.  In the Operations Console, go to **Administration**.
2.  Right-click **Device Management** and select **Discovery Wizard**.
3.	Select **UNIX/Linux Computers**  and click **Next**.
4.  Click **Add**.
4.	Enter the IP of the Linux Server under **Discover Scope** and keep the SSH Port of 22.
6.  For **Discovery Type**, keep the default of **All Computers**
8.  Either select **Use Run As Credentials** or click **Set Credentials** and select credentials with access to the agent computer.
9.  Click **Save** to save the Discovery Criteria.
5.	Select the **target resource pool** for your Linux agents.
10. Click **Discover**.
6.	Select the Linux computer that was discovered under **Manageable computers** and click **Manage**.

