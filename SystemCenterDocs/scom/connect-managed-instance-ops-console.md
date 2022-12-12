---
ms.assetid: 
title: Connect the Azure Monitor SCOM Managed Instance (preview) to Ops console
description: This article describes how to connect the Azure Monitor SCOM Managed Instance (preview) to Ops console.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 12/09/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Connect the Azure Monitor SCOM Managed Instance (preview) to Ops console

Azure Monitor SCOM Managed Instance (preview) is compatible with [System Center Operations Manager 2022](https://www.microsoft.com/download/details.aspx?id=104038).

After you create the SCOM Managed Instance (preview) in Azure, connect the instance to Ops console to configure the workloads and monitor.

## Connect SCOM Managed Instance (preview) to Ops console

Follow the below steps to connect a SCOM Managed Instance (preview) to Ops console:

1. **Identify server to install Ops Console**: Identify a server where you want to install the Ops console. 
     >[!Note]
     >Don't perform this on a SCOM Managed Instance (preview) VM, do it on a separate VM. The VM needs to be a Windows Server. This server can be on-premises or on Azure.
1. **Install the Ops Console**: From the [executable file](https://go.microsoft.com/fwlink/?linkid=2212475), install the Operations console and follow the installation wizard to successfully install the Ops console.
1. **Connect SCOM Managed Instance (preview) to Ops Console**: Log in to the Ops console and select **Connect To Server**. Add the FQDN pointing to the management servers.
         
      For a detailed procedure to connect the Ops console to a Management Group (in this case, SCOM Managed Instance (preview)), see [How to connect to the Operations and Web console](/system-center/scom/manage-consoles-how-to-connect?view=sc-om-2019&preserve-view=true)
1. **Gateway Server requirements**: If your agents are in a domain that is outside the trust boundary of the SCOM Managed Instance (preview), you need to install a gateway server to use certificate-based authentication. 

    If you only have a few agents outside the trust boundary, you can use certificates to directly connect them to the SCOM Managed Instance (preview) without a gateway server. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019&preserve-view=true). If you need to install a gateway server, identify a desired server, install the gateway server from the System Center Operations Manager executable file and follow the steps in the installation wizard.

    >[!Note]
    >When you install a gateway, run the `gatewayapprovaltool` before you install the gateway software on the gateway. This needs to be run from the management server side.

1. **Configure the Gateway Server**: When you install the Gateway Server, enter the following:
   - *Management Group Name*: The name of the SCOM Managed Instance (preview).
   - *Management Server Name*: The FQDN of the Management Server that you would link the gateway server to. 
    You can set the second management server in SCOM Managed Instance (preview) as a failover server so that the gateway server can fail over to it when the primary management server stops working. For more information, see [Install a gateway server](/scom/deploy-install-gateway-server?view=sc-om-2019&preserve-view=true). Setting up the failover management server is a command-line based setup and needs to run from where you have the System Center Operations Manager shell or the management server.

1. **Install Agents**: For Agents open the ports 5723/135/138/445 and [install your agents](/system-center/scom/manage-deploy-windows-agent-console?view=sc-om-2019&preserve-view=true).

1. **Connect SCOM Managed Instance (preview) to the Web Console**: To connect to the Web console, go to properties in the SCOM Managed Instance (preview) homepage, and copy the value in the *Operations Manager Web Console URL*. Paste that URL in any browser to open the web console.

## Next step

[SCOM Managed Instance (preview) overview](operations-manager-managed-instance-overview.md)