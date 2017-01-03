---
title: Exchange Users Integration Pack for Orchestrator in System Center 2016
description: Integration packs are add-ons for System Center 2016 - Orchestrator, a component of System Center 2016.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a7359ab-604e-4e05-89f3-09eb13a14c58
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Exchange users integration pack
======================================================================

Applies To: System Center 2016 Orchestrator

Integration packs are add-ons for Orchestrator, a component of System Center 2016. Integration packs optimize IT operations across various environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and third party products. The Integration Pack for Exchange Users facilitates the automation of user-centric tasks, such as actions to send email messages, create appointments, or update tasks.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator 2016 Privacy Statement](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System requirements
-------------------

Prior to implementing the Exchange Users Integration Pack, the following listed software must be installed and configured. For more information about installing and configuring Orchestrator and the Exchange Users Integration Pack, refer to the respective product documentation.

-   System Center 2016 - Orchestrator
-   Microsoft .NET Framework 3.5
-   Microsoft Exchange 2010 Service Pack 1 or Microsoft Exchange 2013 or Microsoft Exchange Online/Office 365

## Downloading the integration pack
--------------------------------

To download this the Exchange Users Integration Pack, go to the [Download Center site](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and deploying the integration pack
----------------------------------------

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see How to Install an Integration Pack.

## Configuring the Exchange users integration pack connections
---------------------------------------------------------

A connection establishes a reusable link between the Orchestrator and an Exchange server. You can specify as many connections as necessary to create links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

The integration pack supports two types of Exchange configurations: the basic Exchange Configuration connection and the Exchange Item Type configuration.

The basic Exchange Configuration contains connection information that is used by activities where the item type is either implicit or not required, such as the Send E-Mail and Delete Item activities.

### To set up an Exchange configuration connection

1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **Exchange User**. The **Exchange User** dialog box appears.

2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This can be the name of the computer running Exchange Server or a descriptive name to distinguish the type of connection.

4.  In the **Type** box, select **Exchange Configuration**.

5.  In the **Exchange Server Address** box, type the name or IP address of the Exchange server. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN). You may leave the **Exchange Server Address** box empty if you enable the **Use Autodiscover** option.

6.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the Exchange server.

7.  In the **Domain** box, type the name of the domain that will authorize access.

8.  In the **Timeout** box, enter a timeout value or leave the default.

9.  Click **OK**.

10.  Add any additional connections if applicable, and then click **Finish**.

The Exchange Item Type Configuration contains connection information and lets users specify an Exchange item type. The Exchange Item Configuration activity is used by activities that dynamically generate optional and required properties, filter and published data, as is the case with the Create Item and Get Item activities.

### To set up an Exchange item type connection

1.  In the **Orchestrator Runbook Designer**, click **Options**, and then click **Exchange User**. The **Exchange User** dialog box appears.

2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This can be the name of the Exchange server or a descriptive name to distinguish the type of connection.

4.  In the Type box, select **Exchange Configuration (Item Activity)**.

5.  In the **Exchange Server Address** box, type the name or IP address of the Exchange server. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN). You may leave the **Exchange Server Address** box empty if you enable the **Use Autodiscover** option.

6.  In the **Username** and **Password** boxes, type the credentials that Orchestrator will use to connect to the Exchange server.

7.  In the **Domain** box, type the name of the domain that will authorize access.

8.  In the **Timeout** box, enter a timeout value or leave the default.

9.  In the **Item Type** box, enter a valid Exchange Item Type.

10.  Add any additional connections if applicable, and then click **Finish**.
