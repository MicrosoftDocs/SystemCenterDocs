---
title: FTP Integration Pack for Orchestrator in System Center
description: Integration packs are add-ons for System Center - Orchestrator. You can design runbooks in Orchestrator.
ms.custom: na
ms.date: 04/04/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e0482f7f-711a-4b40-9884-1d1bd4b96bf2
author: jyothisuri
ms.author: jsuri
manager: evansma
---

# FTP integration pack

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

Integration packs are add-ons for Orchestrator, a component of System Center, that can help you optimize IT operations across heterogeneous environments. You can design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and by third party products. The Integration Pack for FTP enables you to automate FTP operations which include creating a folder, deleting a file or folder, downloading, uploading, file and folder listing and synchronization.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System requirements

The Integration Pack for FTP requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and FTP, refer to the respective product documentation.
-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2019 integration packs require System Center 2019 - Orchestrator
-   FTP server

## Download the integration pack

- To download the FTP integration pack for Orchestrator 2016, see [Microsoft Download Center space for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- - To download the FTP integration pack for Orchestrator 2019, see [Microsoft Download Center space for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How to add an integration pack](how-to-add-an-integration-pack.md).

## Configuring the FTP connections

A connection establishes a reusable link between Orchestrator and an FTP server. You can create as many connections as you require specifying links to multiple FTP servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.
To set up an FTP connection

1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **FTP**. The **FTP** dialog box appears.
2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.
3.  In the **Name** box, enter a name for the connection. This can be the name of the **FTP** server, or a descriptive name to distinguish the type of connection.
4.  In the **Type** box, click the â€¦ button and select a configuration type.
5.  In the **Connection Type** box, click the â€¦ button and select a connection type.
6.  In the **Transfer Type (FTP)** box, click the â€¦ button and select a transfer type. This configuration property applies to FTP only. This property can be left empty when the connection type is SSH File Transfer Protocol (SFTP).<br>**Note:**   Orchestrator does not support SFTP on computers that run Windows.
7.  In the **Server** box, type the name or IP address of the **FTP** server. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).
8.  In the **Port** box, type the port number for the selected connection type.
9.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the **FTP** server.
10.  In the **Timeout** box, type the amount of time in seconds before an FTP operation will time out.
11. In the **Certificate Path (FTP)** box, type the path to a certificate. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
12.  In the **Certificate Password (FTP)** box, type the password for the certificate. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
13.  In the **HTTP Proxy Server (FTP)** box, type the name of IP address of the HTTP proxy server. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN). This configuration property applies to FTP only. This configuration property is optional and can be left empty.
14.  In the **HTTP Proxy Port (FTP)** box, type the port number for the HTTP proxy server. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
15.  In the **HTTP Proxy Username (FTP)** and **HTTP Proxy Password (FTP)**, type the credentials that Orchestrator will used to connect to the HTTP proxy server. This configuration property applies to FTP only. This configuration property is optional and can be left empty.
16.  Click **OK** to close the configuration dialog box, and then click **Finish**.
