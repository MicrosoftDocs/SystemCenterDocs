---
title: System Center Integration Pack for System Center 2016 Service Manager
description: The integration pack (IP) for System Center 2016 - Service Manager is an add-in for System Center 2016 - Orchestrator that enables you to use Service Manager to coordinate and use operational data in an existing IT environment comprised of service desk systems, configuration management systems, and event monitoring systems.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2696fb5c-0b33-48db-92da-80761a131522
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
System Center Integration Pack for System Center 2016 Service Manager
=====================================================================

Applies To: System Center 2016 - Orchestrator

The integration pack (IP) for System Center 2016 - Service Manager is an add-in for System Center 2016 - Orchestrator that enables you to use Service Manager to coordinate and use operational data in an existing IT environment comprised of service desk systems, configuration management systems, and event monitoring systems.

For more information about the System Center integration pack for System Center 2016 - Service Manager and for other options for automating Service Manager, see the [System Center 2016 Integration Guide](http://go.microsoft.com/fwlink/?LinkID=275796).

System Requirements
-------------------

The Service Manager IP requires the following software to be installed and configured before you implement the integration:

-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2016 - Service Manager
-   The Service Manager IP is supported for use only on computers set to use:
    -   The ENU Locale
    -   The U.S. English date format (month/day/year)

<br><br><strong>Important </strong><br>System Center Service Manager 2010 and System Center 2016 - Service Manager share the same version of **Microsoft.EnterpriseManagement.Core.dll**. Installation of System Center Service Manager 2010 IP and System Center 2016 - Service Manager IP on the same runbook server is not supported.<br><br>

For more information about how to install and configure Orchestrator or System Center 2016 SP1 and System Center 2016 - Service Manager, see the applicable product documentation.

Downloading the Integration Pack
--------------------------------

For information about how to obtain this integration pack, see [System Center 2016 - Orchestrator 2016 Component Add-ons and Extensions](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

Registering and Deploying the Integration Pack
----------------------------------------------

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to Runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

Configuring the System Center 2016 - Service Manager Connections
----------------------------------------------------------------

A connection establishes a reusable link between Orchestrator and a Service Manager Server. You can create as many connections as you need to specify links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

#### To configure the Service Manager connections

1.  In the Runbook Designer, click the **Options** menu, and select **SC 2016 Service Manager**. The **SC 2016 Service Manager** dialog box appears.

2.  On the **Connections** tab, click **Add** to begin the connection setup.

3.  In the **Name** box, enter a name for the connection. This could be the name of the Service Manager server, or a descriptive name to distinguish the type of connection.

4.  In the **Server** box, click the ellipsis button **(...)**. Select the Service Manager server, and then click **OK**.

5.  In the **Credentials** section, type the **Domain**, **User name**, and **Password** that the Orchestrator server will use to connect to the Service Manager computer.

6.  In the **Monitoring Intervals** section, enter the **Polling** and **Reconnect** intervals that the Orchestrator server will use with the connection to the Server Manager computer. The default is **10 seconds**.

7.  Click **Test Connection**. When the success message appears, click **OK**.

8.  Add additional connections if applicable. Click **OK** to close the configuration dialog box, and then click **Finish**.
