---
title: System Center Integration Pack for Microsoft SharePoint
description: Integration packs are add-ons for Orchestrator, a component of Microsoft System Center 2016, that helps you optimize IT operations across heterogeneous environments.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e9d99612-366f-47be-aa7b-39713095e285
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# System Center Integration Pack for Microsoft SharePoint

Applies To: System Center 2016 - Orchestrator

Integration packs are add-ons for Orchestrator, a component of Microsoft System Center 2016, that helps you optimize IT operations across heterogeneous environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and by non-Microsoft products.

The System Center Integration Pack for Microsoft SharePoint enables the automation of common tasks in SharePoint, for example, to create list items, to upload and download documents, and to monitor a list for changes.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience that you want. For more information, see the [System Center Orchestrator 2016 Privacy Statement](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

The integration pack for SharePoint requires the following software to be installed and configured before you implement the integration. For more information about installing and configuring System Center 2016 and the Integration Pack for SharePoint, refer to the respective product documentation.

-   System Center 2016 Orchestrator
-   Microsoft .NET Framework 4
-   Microsoft SharePoint 2013

## Downloading the Integration Pack

To download this integration pack, see the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=309210).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures about how to install integration packs, see [How to install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configuring the SharePoint Integration Pack Connections

A connection establishes a reusable link between Orchestrator and a SharePoint site. You can create as many connections as you require to specify links to multiple sites. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

#### To set up an SharePoint connection

1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **Microsoft SharePoint.** The **Microsoft SharePoint** dialog box appears.
2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.
3.  In the **Name** box, enter a name for the connection. This name can be the name of the SharePoint site or a descriptive name to distinguish the type of connection.
4.  In the **Type** box, select **SharePoint Configuration.**
5.  In the **SharePoint Site** box, enter the URL of the SharePoint site that you want to integrate with.
6.  In the **User Name** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the SharePoint site.
7.  In the **Domain** box, enter the name of the domain to authorize access.
8.  In the **SharePoint Online** box, enter **False**.
9.  In the **Default Monitor Interval (seconds)** box, enter a time-out value, in seconds, or keep the default value.

10. In the **Default Maximum Items** box, enter a maximum value, or keep the default value.
11. Click **OK**.
12. Add additional connections, if applicable, and then click **Finish**.

