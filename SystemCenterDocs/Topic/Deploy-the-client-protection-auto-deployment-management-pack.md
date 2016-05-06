---
title: Deploy the client protection auto-deployment management pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78b4e7ef-3abc-48ce-a407-146378c4f069
---
# Deploy the client protection auto-deployment management pack
You can deploy the Operations Manager [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] Client Protection Auto\-Deployment management pack to do the following:

-   Discover [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers in your environment.

-   Discover protected client computers under each [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

-   Include one or more [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers for auto deployment.

-   Exclude one or more [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers from auto deployment.

-   Specify the maximum [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] capacity for protecting client machines \(default is 1000\).

-   Discover client machines from Active Directory for specified domains.

-   Specify client exclusions.

-   Specify default protection group settings for auto deployment.

-   Filter protected clients and create batches of client machines for protection on each [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)].

-   Auto\-protect clients on all [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers every day.

-   Identify successful\/failed clients for each assignment from [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server’s event log.

## Setting up the management pack
**Operations Manager**: On the Operations Manager server on which auto protection will be enabled, download and install the ClientAD.msi which includes the management pack.

**DPM**: On the DPM servers install Operations Manager agents. Then from the Operations Manager console, enable client auto\-deployment.

**Client computers**: When the client computer connects to the network, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] will automatically back up its data.

Here’s the topology:

![](../Image/ClientAutoDeploymentTopology.gif)

The process is a follows:

1.  Download and install the ClientAD.msi [Client Auto Deployment management pack \)\(ClientAD.msi\)](http://go.microsoft.com/fwlink/?LinkId=207880) and install it on an Operations Manager server. The management pack is included in the download.

2.  Install the Operations Manager agents on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers that protect the client computers. This ensures that the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers discoverable by the Operations Manager server. Operations Manager runs discovery once every 24 hours.

3.  After it’s found at least one [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server Operations Manager server creates a list of all the client computers in the protected domains on [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers that have auto\-protection enabled.

4.  Operations Manager then compares the list of computer with the list of protected and excluded computers and creates a list of the computers that need protection but aren’t part of a protection group. Using this list, Operations Manager creates protection groups assigning a maximum of 100 laptop computers per [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server per day.

5.  When a computer connects to the network, System Center Configuration Manager installs the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] protection agent on the computer and assigns it to the appropriate [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

6.  After a computer’s added to a protection group, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] triggers backups based on the protection group settings.

## Views
The [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Client Auto Deployment management pack provides the following views on the Operations Manager console:

|View Name|Description|
|-------------|---------------|
|Auto deployment alerts|Alerts caused by auto deployment operations such as AD query failed, Auto protection failed due to System Center Operation Manager reboot, and so on.|
|Auto deployment DPM server state|All the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers discovered with details such as [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Version, Available free capacity, Included\/excluded status, and so on.|
|Auto deployment server state|State of auto deployment server.|
|DPM server alerts|Alerts specific to auto protection of a [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server such as Create protection group failure, SLA threshold not met, and so on.|
|Protected clients state|View of all protected clients in different [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers.|
|Stale clients state|View of client computers that have not been backed up for 90 days \(by default\) or the period specified by the administrator.|

## Next steps
Check the [Client auto deployment prerequisites \[TO DELETE\]\]](assetId:///7a12b23e-9cc2-4ed0-bb84-6319159f64b6).

