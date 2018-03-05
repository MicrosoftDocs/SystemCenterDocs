---
title: System Center - Orchestrator integration pack for System Center - Operations Manager
description: This article describes the System Center integration pack for System Center - Operations Manager, an add-on provided by System Center - Orchestrator.
ms.date: 01/17/2018
ms.prod: system-center-threshold
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# Integration pack for System Center - Operations Manager

The integration pack for System Center - Operations Manager is an add-in for System Center - Orchestrator. It enables you to connect an Orchestrator Runbook server to an Operations Manager management server to automate various actions.

[Learn more](https://go.microsoft.com/fwlink/?LinkID=275796) about integration packs.

## System requirements

The Operations Manager Integration Pack requires the following software to be installed and configured before you deploy the integration pack.

- System Center - Orchestrator
- The integration pack version should match the System Center version.
- System Center - Operations Manager

Install the Operations Manager console on each computer where an Orchestrator Runbook server or Runbook Designer is installed, if that server needs to interact with Operations Manager.
    - The Orchestrator Integration Library Management Pack is required by the Create Alert object.
    - The Create Alert object installs this management pack automatically in System Center Operations Manager the first time that it is run.
    - To uninstall the integration pack, remove the Orchestrator Integration Library Management Pack from System Center Operations Manager.


## Download the integration pack

Download the pack from [System Center - Orchestrator Component Add-ons and Extensions](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Register and deploy the pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to Runbook servers and Runbook Designers. [Learn more](how-to-add-an-integration-pack.md).

## Configure the connections

A connection establishes a reusable link between Orchestrator and an Operations Manager management server. You can create as many connections as you require to specify links to multiple Operations Manager management servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.



1.  In the Runbook Designer, click the **Options** menu, and select Operations Manager.
2.  On the **Connections** tab, click **Add** to begin the connection setup. The **Connection Entry** dialog box appears.
3.  In the **Name** box, type the name or IP address of the server running System Center Operations Manager.
4.  In the **Domain** box, type the domain name of the Operations Manager server, or click the ellipsis button **(...)** to browse for the domain, select it, and then click **Add**.
5.  In the **User name** and **Password** boxes, type the credentials that the Orchestrator server will use to connect to the Operations Manager server.
6. In **Monitoring Intervals\\Polling**, and **Monitoring Intervals\\Reconnect** accept the default value of ten seconds, or configure the value.(default value: 10 seconds) is a configurable property.
7.  Click **Test Connection**. When the message "Successfully connected" appears, click **OK**.
8.  Add additional connections if applicable. Click **OK** to close the configuration dialog box, and then click **Finish**.
