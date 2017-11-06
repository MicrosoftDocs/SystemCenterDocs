---
title: System Center Integration Pack for System Center 2016 Operations Manager
description: The System Center Integration Pack for System Center 2016 Operations Manager is an add-in for System Center 2016 - Orchestrator.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 75c8aa38-f58a-4f31-8f88-73a8cc93919a
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# System Center Integration Pack for System Center 2016 Operations Manager

The System Center Integration Pack for System Center 2016 Operations Manager is an add-in for System Center 2016 - Orchestrator. It enables you to connect an Orchestrator Runbook server to an Operations Manager management server to automate various actions.

For more information about the System Center integration pack for System Center 2016 - Operations Manager and for other options for automating System Center 2016 - Operations Manager, see the [System Center 2016 Integration Guide](https://go.microsoft.com/fwlink/?LinkID=275796).

## System Requirements

The Operations Manager Integration Pack requires the following software to be installed and configured before you deploy the integration pack. For more information about installing and configuring the software for Orchestrator and Operations Manager, see the respective product documentation:

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2016 Service Pack 1 (SP1) integration packs require Orchestrator in System Center 2016 Service Pack 1 (SP1)
-   System Center 2016 - Operations Manager
    -   Install the Operations Manager console on each computer where an Orchestrator Runbook server or Runbook Designer is installed, if that server needs to interact with Operations Manager.
    -   The Orchestrator Integration Library Management Pack is required by the Create Alert object. The Create Alert object installs this management pack automatically in System Center Operations Manager the first time that it is run. To uninstall this integration pack, remove the Orchestrator Integration Library Management Pack from System Center Operations Manager.

## Downloading the Integration Pack

For information about how to download this integration pack, see [System Center 2016 - Orchestrator 2016 Component Add-ons and Extensions](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configuring the System Center 2016 Operations Manager Connections

A connection establishes a reusable link between Orchestrator and an Operations Manager management server. You can create as many connections as you require to specify links to multiple Operations Manager management servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

### To create up a System Center 2016 Operations Manager connection

1.  In the Runbook Designer, click the **Options** menu, and select **SC 2016 Operations Manager**. The **SC 2016 Operations Manager** dialog box appears.
2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Connection Entry** dialog box appears.
3.  In the **Name** box, type the name or IP address of the server running System Center Operations Manager.
4.  In the **Domain** box, type the domain name of the Operations Manager server, or click the ellipsis button **(...)** to browse for the domain, select it, and then click **Add**.
5.  In the **User name** and **Password** boxes, type the credentials that the Orchestrator server will use to connect to the Operations Manager server.
6.  Click **Test Connection**. When the message "Successfully connected" appears, click **OK**.
7.  Add additional connections if applicable. Click **OK** to close the configuration dialog box, and then click **Finish**.

For System Center 2016 SP1 only: Three new Operations Manager Connection properties were added:

-   **Monitoring Intervals\\Polling** (default value: 10 seconds) is a configurable property.
-   **Monitoring Intervals\\Reconnect** (default value: 10 seconds) is a configurable property.
-   **Name**
