---
title: HP Operations Manager Integration Pack for System Center 2016 - Orchestrator
description: The Integration Pack for HP Operations Manager is an add-on for System Center 2016 - Orchestrator that enables you to automate the consolidation and correlation of fault and performance events across you entire physical and virtual IT infrastructure.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fbb368f4-4512-4960-a98d-66e36ee49d29
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
HP Operations Manager Integration Pack for System Center 2016 - Orchestrator
============================================================================

Applies To: System Center 2016 - Orchestrator

The Integration Pack for HP Operations Manager is an add-on for System Center 2016 - Orchestrator that enables you to automate the consolidation and correlation of fault and performance events across you entire physical and virtual IT infrastructure.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more information, see the [Privacy Statement for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

System Requirements
-------------------

The Integration Pack for HP Operations Manager requires the following software to be installed and configured prior to implementing the integration. For more information about installing and configuring Orchestrator and the HP Operations Manager application, refer to the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   HP Operations Manager 9.x

Downloading the Integration Pack
--------------------------------

To download this integration pack, see [HP Operations Manager Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=54102).

Registering and Deploying the Integration Pack
----------------------------------------------

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

Configuring the HP Operations Manager Connections
-------------------------------------------------

A connection establishes a reusable link between Orchestrator and an HP Operations Manager server. You can create as many connections as you require to specify links to multiple servers running HP Operations Manager. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

#### To set up an HP Operations Manager configuration

1.  In the Runbook Designer, click the **Options** menu, and select **HP Operations Manager**. The HP Operations Manager dialog box appears.

2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This could be the name of the HP Operations Manager server or a descriptive name to distinguish the type of connection.

4.  Click the ellipsis button **(...)** next to the Type field and then select **HPOM Configuration**.

5.  In the **HPOM Host** box, type the name or IP address of the HP Operations Manager computer. If you are using the computer name, you can type the NetBIOS name or the fully qualified domain name (FQDN).

6.  In the **HPOM Port** box, type the port used to connect to the HP Operations Manager computer. By default the **HPOM Port** is set to 443.

7.  In the **HPOM Username** and **HPOM Password** boxes, type the credentials that Orchestrator will use to connect to the HP Operations Manager server. When a connection is used for a **Launch Tool** activity, an HPOM Administrator account must be used. All other activities can use an HPOM User account.

8.  Click **OK** to close the configuration dialog box.

9.  Add additional connections if applicable.

10. Click **Finish**.
