---
ms.assetid: 
title: Create an Aquila instance
description: This article describes how to create an Aquila instance to monitor workloads using System Center Operations Manager functionality on Azure.
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 10/04/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Connect the Aquila instance to Ops console

Aquila is compatible with System Center Operations Manager 2019. [Download](https://www.microsoft.com/evalcenter/evaluate-system-center-2019) a trial version of System Center Operations Manager 2019 (available for 180 days), if you don't have the System Center Operations Manager 2019 executable files. Fill the personal details form and download SCOM_2019.exe

After you create the Aquila Instance in Azure, connect the instance to Ops Console to configure the workloads that needs to be monitored.

Follow the below steps to connect Aquila instance to Ops Console:

## Identify Server where to install Ops Console 

Identify a server where you want to install the Ops Console. Don't perform this on Aquila VM, but rather a separate VM. The VM needs to be a Windows Server. This server can be on-premesis or on Azure.

## Fulfill prerequisites to install Ops Console

Complete the prerequisites befor you install the Ops Console. Download and install the *RepotingViewer.msi* and *SQLSysClrTypes.msi* before the installation of the Ops Console. For a complete list of prerequisites, see [System Center Operations Manager 2019 - QuickStart Deployment Guide](https://kevinholman.com/2019/03/14/scom-2019-quickstart-deployment-guide/).

## Install the Ops Console

From the executable file, install the Operations Console and follow the installation wizard to successfully install the Ops Console.

## Connect Aquila to Ops Console

Login to the Ops Console and select **Connect To Server**. Add the FQDN pointing to one of the two management servers. 
   >[!Note]
   >Any one of the two management servers can be used.

For a detailed procedure to connect the Ops Console to a Management Group (in this case, Aquila instance), see [How to connect to the Operations and Web Console](/system-center/scom/manage-consoles-how-to-connect?view=sc-om-2019)

## Requirements regarding Gateway Server

If your agents are in a domain that is outside the trust boundary of the Aquila instance, you need to install a gateway server to use certificate-based authentication. 

If you only have a few agents outside the trust boundary, you can use certificates to directly connect them to the Aquila instance without a gateway server. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019). If you need to install a gateway server, identify a desired server, install the gateway server from the System Center Operations Manager executable file and follow the steps in the installation wizard.

>[!Note]
>When you install a gateway, run the `gatewayapprovaltool` before you install the gateway software on the gateway. This needs to be run from the management server side.

## Configure the Gateway Server

When you install the Gateway Server, in the *Management Group Name*, enter the name of the Aquila Instance and in the *Management Server Name*, enter the FQDN of the Management Server that you would like to link the gateway server to. You can set the second management server in Aquila as a failover server so that the gateway server can failover to it when the primary management server stops working. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019). Setting up the failover management server is a command-line based setup and needs to run from where you have the System Center Operations Manager shell or the management server.

## Install Agents

Install your agents using the [instructions](/system-center/scom/manage-deploy-windows-agent-console?view=sc-om-2019).

## Connect Aquila to the Web Console
 
To connect to the Web Console, go to properties in the Aquila homepage, and copy the value in the *SCOM web console URL*. Paste that URL in any browser to open the web console.

## Next step

> [!div class="nextstepaction"]
> [Aquila overview](aquila-overview.md)