---
ms.assetid: 
title: Connect the Operations Manager managed instance (preview) to Ops console
description: This article describes how to connect the Operations Manager managed instance (preview) to Ops console.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/11/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Connect the Operations Manager managed instance (preview) to Ops console

Operations Manager managed instance (preview) is compatible with System Center Operations Manager 2019. [Download](https://www.microsoft.com/evalcenter/evaluate-system-center-2019) a trial version of System Center Operations Manager 2019 (available for 180 days) if you don't have the System Center Operations Manager 2019 executable files. Fill the personal details form and download SCOM_2019.exe

After you create the Operations Manager managed instance (preview) in Azure, connect the instance to Ops Console to configure the workloads that need to be monitored.

## Procedure to connect Operations Manager managed instance (preview) to Ops console

Follow the below steps to connect an Operations Manager managed instance (preview) to Ops Console:

1. Identify server to install Ops Console: Identify a server where you want to install the Ops Console. Don't perform this on an Operations Manager managed instance (preview) VM, but rather on a separate VM. The VM needs to be a Windows Server. This server can be on-premises or on Azure.
1. Prerequisites to install Ops Console: Complete the [prerequisites](https://kevinholman.com/2019/03/14/scom-2019-quickstart-deployment-guide/) before you install the Ops Console. Download and install the *ReportingViewer.msi* and *SQLSysClrTypes.msi* before you install the Ops Console. 
1. Install the Ops Console: From the executable file, install the Operations Console and follow the installation wizard to successfully install the Ops Console.
1. Connect Operations Manager managed instance (preview) to Ops Console: Log in to the Ops Console and select **Connect To Server**. Add the FQDN pointing to one of the two management servers. 
   >[!Note]
   >Any one of the two management servers can be used.

    For a detailed procedure to connect the Ops Console to a Management Group (in this case, Operations Manager managed instance (preview)), see [How to connect to the Operations and Web Console](/system-center/scom/manage-consoles-how-to-connect?view=sc-om-2019&preserve-view=true)
1. Gateway Server requirements: If your agents are in a domain that is outside the trust boundary of the Operations Manager managed instance (preview), you need to install a gateway server to use certificate-based authentication. 

    If you only have a few agents outside the trust boundary, you can use certificates to directly connect them to the Operations Manager managed instance (preview) without a gateway server. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019&preserve-view=true). If you need to install a gateway server, identify a desired server, install the gateway server from the System Center Operations Manager executable file and follow the steps in the installation wizard.

    >[!Note]
    >When you install a gateway, run the `gatewayapprovaltool` before you install the gateway software on the gateway. This needs to be run from the management server side.

1. Configure the Gateway Server: When you install the Gateway Server, enter the following:
   - *Management Group Name*: The name of the Operations Manager managed instance (preview).
   - *Management Server Name*: The FQDN of the Management Server that you would link the gateway server to. 
    You can set the second management server in Operations Manager managed instance (preview) as a failover server so that the gateway server can fail over to it when the primary management server stops working. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019&preserve-view=true). Setting up the failover management server is a command-line based setup and needs to run from where you have the System Center Operations Manager shell or the management server.

1. Install Agents: Install your agents using the [instructions](/system-center/scom/manage-deploy-windows-agent-console?view=sc-om-2019&preserve-view=true).

1. Connect Operations Manager managed instance (preview) to the Web Console: To connect to the Web Console, go to properties in the Operations Manager managed instance (preview) homepage, and copy the value in the *Operations Manager Web Console URL*. Paste that URL in any browser to open the web console.

## Next step

> [!div class="nextstepaction"]
> [Operations Manager managed instance (preview) overview](operations-manager-managed-instance-overview.md)