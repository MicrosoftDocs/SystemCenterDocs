---
ms.assetid: 
title: Connect the Azure Monitor SCOM Managed Instance (preview) to Ops console
description: This article describes how to connect the Azure Monitor SCOM Managed Instance (preview) to Ops console.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 02/13/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
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
     >Don't perform this on a SCOM Managed Instance (preview) VM; do it on a separate VM. The VM needs to be a Windows Server. This server can be on-premises or on Azure.
1. **Install the Ops Console**: From the [executable file](https://go.microsoft.com/fwlink/?linkid=2212475), install the Operations console and follow the installation wizard to successfully install the Ops console.
1. **Connect SCOM Managed Instance (preview) to Ops Console**: Sign in to the Ops console and select **Connect To Server**. Add the FQDN pointing to the management servers.
         
      For a detailed procedure to connect the Ops console to a Management Group (in this case, SCOM Managed Instance (preview)), see [How to connect to the Operations and Web console](/system-center/scom/manage-consoles-how-to-connect?view=sc-om-2019&preserve-view=true)

1. **Install Agents**: Open the ports 5723/135/138/445 and [install your agents](/system-center/scom/manage-deploy-windows-agent-console?view=sc-om-2019&preserve-view=true).

1. **Connect SCOM Managed Instance (preview) to the Web Console**: To connect to the Web console, go to properties in the SCOM Managed Instance (preview) homepage, and copy the value in the *Operations Manager Web Console URL*. Paste that URL in any browser to open the web console.

## Next step

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md)

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
