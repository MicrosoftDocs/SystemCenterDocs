---
title: Windows Azure Integration Pack for Orchestrator in System Center
description: The Integration Pack for Windows Azure is an add-on for Orchestrator in System Center that enables you to automate Windows Azure operations related to certificates, deployments, cloud services, storage, and virtual machines using Windows Azure Service Management REST API.
ms.custom: na
ms.date: 03/04/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eeca4cd9-edeb-42cd-8087-b89b16970bc9
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# Windows Azure Integration Pack for Orchestrator in System Center

The Integration Pack for Windows Azure is an add-on for Orchestrator in System Center that enables you to automate Windows Azure operations related to certificates, deployments, cloud services, storage, and virtual machines using the '2012-03-01' version of the Windows Azure Service Management REST API.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

Before you install the Integration Pack for Windows Azure, the following listed software must be installed and configured. For more information about installing and configuring Orchestrator and Windows Azure, refer to the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2019 integration packs require System Center 2019 - Orchestrator
-   Windows Azure

## Download the Integration Pack

- To download the Windows Azure integration pack, for Orchestrator 2016,  see the [Microsoft Download Center space for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- To download the Windows Azure integration pack, for Orchestrator 2019,  see the [Microsoft Download Center space for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).


## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configure the Windows Azure Connections

A connection establishes a reusable link between Orchestrator and Windows Azure. You can specify as many connections as you require to create links to multiple Windows Azure subscriptions.

### To set up a Windows Azure connection

1.  In the Runbook Designer, click **Options**, and then click **Windows Azure**. The **Windows Azure** dialog box appears.

2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This could be the name of the **Windows Azure** subscription, or a descriptive name to differentiate the type of connection.

4.  In the **Type** box, click the ... button and select a connection type.

5.  In the **Subscription ID** box, enter the subscription ID of the Windows Azure subscription to connect to.

6.  In the **PFX File Path** box, click the ... button and select the management certificate file associated with this Windows Azure subscription.
>[!NOTE]
>Your certificate file enables authentication of requests to your Windows Azure subscription, and so should be stored in a non-public folder to prevent unauthorized access.

7.  In the **PFX File Password** box, enter the password of the management certificate file associated with this Windows Azure subscription.

8.  Click **OK** to close the configuration dialog box, and then click **Finish**.
