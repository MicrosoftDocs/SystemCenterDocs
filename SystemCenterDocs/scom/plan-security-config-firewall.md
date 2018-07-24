---
ms.assetid: 045b2f66-b672-4cd2-9d83-9d067b83fdaf
title:  Configuring a Firewall for Operations Manager
description: This article provides design guidance for which ports and protocols need to be allowed for Operations Manager to communicate through network firewalls and proxy servers.
author: mgoedtel
ms.author: magoedte
manager: carmomm
ms.date: 07/20/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# Configuring a Firewall for Operations Manager

This section describes how to configure your firewall to allow communication between the different Operations Manager features on your network.  

## Port assignments
The following table shows Operations Manager feature interaction across a firewall, including information about the ports used for communication between the features, which direction to open the inbound port, and whether the port number can be changed.

|Operations Manager Feature A|Port Number and Direction|Operations Manager Feature B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|Management server|1433/TCP ---> <br>  1434/UDP ---> <br>  135/TCP (DCOM/RPC) ---> |Operations Manager database|Yes (Setup)|WMI Port 135 (DCOM/RPC) for the initial connection and then a dynamically assigned port above 1024.  For further information, see [Special considerations for Port 135](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access#BKMK_port_135)|
|Management server|5723, 5724 --->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|management server|161,162 <--->|network device|No|All firewalls between the management server and the network devices need to allow SNMP (UDP) and ICMP bi-directionally.|
|Gateway server|5723 --->|management server|No||
|Management server|1433/TCP ---><br>  1434/UDP --->|Reporting data warehouse|No||
|Reporting server|5723, 5724 --->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Operations console|5724 --->|management server|No||
|Connector framework source|51905 --->|management server|No||
|Web console server|5724 --->|management server|No||
|Web console browser|80,443 --->|web console server|Yes (IIS Admin)|Default ports for HTTP or SSL enabled.|
|Web console for Application Diagnostics|1433/TCP ---><br>  1434 --->|Operations Manager database|Yes (Setup)||
|Web console for Application Advisor|1433/TCP ---><br>  1434 --->|Reporting data warehouse|Yes (Setup)||
|Connected management server (Local)|5724 --->|connected management server (Connected)|No||
|Windows agent installed using MOMAgent.msi|5723 --->|management server|Yes (Setup)||
|Windows agent installed using MOMAgent.msi|5723 --->|gateway server|Yes (Setup)||
|Windows agent push installation, pending repair, pending update|5723/TCP, 135/TCP, 137/UDP, 138/UDP, 139/TCP, 445/TCP<br>  *RPC/DCOM High ports (2008 OS and later) Ports 49152-65535 TCP||Communication is initiated from MS/GW to an Active Directory domain controller and the target computer.|
|UNIX/Linux agent discovery and monitoring of agent|TCP 1270 <---|management server or gateway server|No||
|UNIX/Linux agent for installing, upgrading, and removing agent using SSH|TCP 22 <---|management server or gateway server|Yes||
|OMED Service|TCP 8886 <---|management server or gateway server|Yes||
|Gateway server|5723 --->|management server|Yes (Setup)||
|Agent (Audit Collection Services forwarder)|51909 --->|management server Audit Collection Services collector|Yes (Registry)||
|Agentless Exception Monitoring data from client|51906 --->|management server Agentless Exception Monitoring file share|Yes (Client Monitoring Wizard)||
|Customer Experience Improvement Program data from client|51907 --->|management server (Customer Experience Improvement Program End) Point|Yes (Client Monitoring Wizard)||
|Operations console (reports)|80 --->|SQL Reporting Services|No|The Operations console uses Port 80 to connect to the SQL Reporting Services web site.|
|Reporting server|1433/TCP ---><br>  1434/UDP --->|Reporting data warehouse|Yes||
|Management server (Audit Collection Services collector)|1433/TCP <---<br>  1434/UDP <---|Audit Collection Services database|Yes||

If SQL Server is installed with a default instance, the port number is 1433. If SQL Server is installed with a named instance, by default it is configured with a dynamic port. To identify the port, do the following: 

1. In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**, expand **Protocols** for <instance name>, and then double-click **TCP/IP**.
2. In the **TCP/IP Properties** dialog box, on the **IP Addresses** tab, note the port value for **IPAall**.  

If you plan on deploying the Operations Manager databases on a SQL Server configured with an Always On Availability Group or migrate after installation, do the following to identify the port:

1. In Object Explorer, connect to a server instance that hosts any availability replica of the availability group whose listener you want to view. Click the server name to expand the server tree.
2. Expand the **Always On High Availability** node and the **Availability Groups** node.
3. Expand the node of the availability group, and expand the **Availability Groups Listeners** node.
4. Right-click the listener that you want to view, and select the **Properties** command.
This opens the **Availability Group Listener Properties** dialog box.

