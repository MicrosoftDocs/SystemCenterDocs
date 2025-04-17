---
title: FTP Integration Pack for Orchestrator in System Center
description: Integration packs are add-ons for System Center - Orchestrator. You can design runbooks in Orchestrator.
ms.custom: na
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: e0482f7f-711a-4b40-9884-1d1bd4b96bf2
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 04/16/2025
---

# FTP integration pack

In this article, you'll learn about FTP integration pack. Integration packs are add-ons for Orchestrator, a component of System Center, that can help you optimize IT operations across heterogeneous environments. You can design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and third-party products. The Integration Pack for FTP enables you to automate FTP operations, which include creating a folder, deleting a file or folder, downloading, uploading, file, and folder listing and synchronization.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System requirements

The Integration Pack for FTP requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and FTP, see the respective product documentation.
- System Center 2016 integration packs require System Center 2016 - Orchestrator
- System Center 2019 integration packs require System Center 2019 - Orchestrator
- FTP server

## Download the integration pack

::: moniker range="<=sc-orch-2019"

- To download the FTP integration pack for Orchestrator 2016, see [Microsoft Download Center space for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- To download the FTP integration pack for Orchestrator 2019, see [Microsoft Download Center space for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).

::: moniker-end

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How to add an integration pack](how-to-add-an-integration-pack.md).

## Configuring the FTP connections

A connection establishes a reusable link between Orchestrator and an FTP server. You can create as many connections as you require specifying links to multiple FTP servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

To set up an FTP connection, follow these steps:

1. In the **Orchestrator Runbook Designer**, select **Options**, and select **FTP**. The **FTP** dialog appears.
2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.
3. In the **Name** box, enter a name for the connection. This can be the name of the **FTP** server or a descriptive name to distinguish the type of connection.
4. In the **Type** box, select the â€¦ button and select a configuration type.
5. In the **Connection Type** box, select the â€¦ button and select a connection type.
6. In the **Transfer Type (FTP)** box, select the â€¦ button and select a transfer type. This configuration property applies to FTP only. This property can be left empty when the connection type is SSH File Transfer Protocol (SFTP).<br>**Note that**   Orchestrator doesn't support SFTP on computers that run Windows.
7. In the **Server** box, enter the name or IP address of the **FTP** server. If you're using the computer name, you can enter the NetBIOS name or the fully qualified domain name (FQDN).
8. In the **Port** box, enter the port number for the selected connection type.
9. In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the **FTP** server.
10. In the **Timeout** box, enter the amount of time in seconds before an FTP operation will time out.
11. In the **Certificate Path (FTP)** box, enter the path to a certificate. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
12. In the **Certificate Password (FTP)** box, enter the password for the certificate. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
13. In the **HTTP Proxy Server (FTP)** box, enter the name of the IP address of the HTTP proxy server. If you're using the computer name, you can enter the NetBIOS name or the fully qualified domain name (FQDN). This configuration property applies to FTP only. This configuration property is optional and can be left empty.
14. In the **HTTP Proxy Port (FTP)** box, enter the port number for the HTTP proxy server. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
15. In the **HTTP Proxy Username (FTP)** and **HTTP Proxy Password (FTP)**, enter the credentials that Orchestrator will use to connect to the HTTP proxy server. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
16. Select **OK** to close the configuration dialog, and select **Finish**.
