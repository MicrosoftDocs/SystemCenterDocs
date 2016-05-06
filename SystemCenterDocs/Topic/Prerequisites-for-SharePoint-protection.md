---
title: Prerequisites for SharePoint protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43c4c017-3f87-4beb-b72c-1ec89216725c
---
# Prerequisites for SharePoint protection
Before you deploy DPM to protect SharePoint do the following:

1.  Review the [release notes](http://technet.microsoft.com/en-us/library/jj860394.aspx) and The [Unsupported scenarios in DPM](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc) for any SharePoint issues.

2.  Verify the support for SharePoint versions and backup scenarios in the [Support Matrix for DPM Protection](assetId:///52bed83a-f484-4925-af77-377073737fc4).

3.  Note that:

    -   You’ll need to install the DPM protection agent on every server in the SharePoint farm, including SQL Servers. See [Installing Protection Agents](http://go.microsoft.com/fwlink/p/?LinkId=227121). The  only exception is that you only install it on a single Web Front End \(WFE\) server. For example if you have a single farm with two WFE servers, an index server and a two\-node SQL Server cluster you’d install the agent on the index server, both nodes in the SQL Server cluster, and one of the WFE servers. This is because WFE servers don’t host content. DPM only needs the agent on one of them to serve as the entry point for protection.

    -   By default when you protect SharePoint all content databases \(and the SharePoint\_Config and SharePoint\_AdminContent\* databases\) will be protected. If you want to add customizations such as search indexes, templates or application service databases, or the user profile service you’ll need to configure these for protection separately. Be sure that you enable protection for all folders that include these types of features or customization files.

    -   Remember that for DPM runs as Local System and to backup SQL Server databases it needs sysadmin privileges on that account for the SQL server. On the SQL Server you want to back up set  NT AUTHORITY\\SYSTEM to sysadmin.

    -   For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] folder is located. This space is required for catalog generation. To enable you to use [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] to perform a specific recovery of items \(site collections, sites, lists, document libraries, folders, individual documents, and list items\), catalog generation creates a list of the URLs contained within each content database. You can view the list of URLs in the recoverable item pane in the **Recovery** task area of [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Administrator Console.

    -   n the SharePoint farm, if you have SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front\-end Web server that DPM will protect.

    -   Protecting application store items isn’t supported with SharePoint 2013.

    -   DPM doesn’t support protecting remote FILESTREAM. The FILESTREAM should be part of the database.

    -   Before you can protect a computer running Office SharePoint Server 2007, you must apply the update in KB941422.

    -   If you use the Office SharePoint Server Search service, before you can protect Office SharePoint Server 2007 SP1 data, you must apply updated in Microsoft KB articles:

        -   [951695](http://go.microsoft.com/fwlink/?LinkID=186530)

        -   [941422](http://go.microsoft.com/fwlink/?LinkID=100392)

