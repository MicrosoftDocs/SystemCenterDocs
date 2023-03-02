---
ms.assetid: 045b2f66-b672-4cd2-9d83-9d067b83fdaf
title: Configuring a Firewall for Operations Manager
description: This article provides design guidance for which ports and protocols need to be allowed for Operations Manager to communicate through network firewalls and proxy servers.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 11/24/2020
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Configuring a Firewall for Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

This section describes how to configure your firewall to allow communication between the different Operations Manager features on your network.  

>[!NOTE]
> Operations Manager uses port 389 for LDAP queries for multiple actions such as agent discovery, active directory integration, and so on. Operations Manager doesn't support LDAPs.

## Port assignments
The following table shows Operations Manager feature interaction across a firewall, including information about the ports used for communication between the features, which direction to open the inbound port, and whether the port number can be changed.

|Operations Manager Feature A|Port Number and Direction|Operations Manager Feature B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|Management server|1433/TCP&nbsp;--->&nbsp;<br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Operations Manager database|Yes (Setup)|WMI Port 135 (DCOM/RPC) for the initial connection and then a dynamically assigned port above 1024.  For more information, see [Special considerations for Port 135](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access#BKMK_port_135) <br>Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Management server|5723,&nbsp;5724&nbsp;--->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Management server|161,162&nbsp;<--->|network device|No|All firewalls between the management server and the network devices need to allow SNMP (UDP) and ICMP bi-directionally.|
|Gateway server|5723&nbsp;--->|management server|No||
|Management server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Reporting data warehouse|No|Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Reporting server|5723,&nbsp;5724&nbsp;--->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Operations console|5724&nbsp;--->|management server|No||
|Operations console|80,&nbsp;443&nbsp;---><br>49152-65535&nbsp;TCP&nbsp;<--->|Management Pack Catalog web service|No|Supports downloading management packs directly in the console from the catalog.<sup>[1](#footnote1)</sup>|
|Connector framework source|51905&nbsp;--->|management server|No||
|Web console server|5724&nbsp;--->|management server|No||
|Web console browser|80,&nbsp;443&nbsp;--->|web console server|Yes (IIS Admin)|Default ports for HTTP or SSL enabled.|
|Web console for Application Diagnostics|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Operations Manager database|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Web console for Application Advisor|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Reporting data warehouse|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Connected management server (Local)|5724&nbsp;--->|connected management server (Connected)|No||
|Windows agent installed using MOMAgent.msi|5723&nbsp;--->|management server|Yes (Setup)||
|Windows agent installed using MOMAgent.msi|5723&nbsp;--->|gateway server|Yes (Setup)||
|Windows agent push installation, pending repair, pending update|5723/TCP<br>135/TCP<br>137/UDP<br>138/UDP<br>139/TCP<br>445/TCP<br><br>*RPC/DCOM&nbsp;High&nbsp;ports&nbsp;(2008&nbsp;OS&nbsp;and&nbsp;later)<br>Ports&nbsp;49152-65535&nbsp;TCP||Communication is initiated from MS/GW to an Active Directory domain controller and the target computer.|
|UNIX/Linux agent discovery and monitoring of agent|TCP&nbsp;1270&nbsp;<---|management server or gateway server|No||
|UNIX/Linux agent for installing, upgrading, and removing agent using SSH|TCP&nbsp;22&nbsp;<---|management server or gateway server|Yes||
|OMED Service|TCP&nbsp;8886&nbsp;<---|management server or gateway server|Yes||
|Gateway server|5723&nbsp;--->|management server|Yes (Setup)||
|Agent (Audit Collection Services forwarder)|51909&nbsp;--->|management server Audit Collection Services collector|Yes (Registry)||
|Agentless Exception Monitoring data from client|51906&nbsp;--->|management server Agentless Exception Monitoring file share|Yes (Client Monitoring Wizard)||
|Customer Experience Improvement Program data from client|51907&nbsp;--->|management server (Customer Experience Improvement Program End) Point|Yes (Client Monitoring Wizard)||
|Operations console (reports)|80&nbsp;--->|SQL Reporting Services|No|The Operations console uses Port 80 to connect to the SQL Reporting Services web site.|
|Reporting server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->|Reporting data warehouse|Yes <sup>[2](#footnote2)</sup>||
|Management server (Audit Collection Services collector)|1433/TCP&nbsp;<---<br>1434/UDP&nbsp;<---|Audit Collection Services database|Yes <sup>[2](#footnote2)</sup>||

#### <a name="footnote1"></a> Management Pack Catalog Web Service <sup>1</sup>
- To access the Management Pack Catalog web service, your firewall must allow the following URL and wildcard (*):
  1. [https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx](https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx)
  2. `http://go.microsoft.com/fwlink/*`

#### <a name="footnote2"></a> Identify SQL Port <sup>2</sup>
 - If SQL Server is installed with the default port, the port number is 1433. If not the default port, it may be dynamic or non-default. To identify the port, follow these steps:
   1. In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**, expand **Protocols** for \<instance name\>, and then double-click **TCP/IP**.
   2. In the **TCP/IP Properties** dialog, on the **IP Addresses** tab, note the port value for **IPAall**.  

 - If you plan on deploying the Operations Manager databases on a SQL Server configured with an Always On Availability Group or migrate after installation, do the following to identify the port:
  
   1. In Object Explorer, connect to a server instance that hosts any availability replica of the availability group whose listener you want to view. Select the server name to expand the server tree.
   2. Expand the **Always On High Availability** node and the **Availability Groups** node.
   3. Expand the node of the availability group, and expand the **Availability Groups Listeners** node.
   4. Right-click the listener that you want to view, and select the **Properties** command. \
      This opens the **Availability Group Listener Properties** dialog. 
