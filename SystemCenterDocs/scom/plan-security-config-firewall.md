---
ms.assetid: 045b2f66-b672-4cd2-9d83-9d067b83fdaf
title: Configuring a Firewall for Operations Manager
description: This article provides design guidance for which ports and protocols need to be allowed for Operations Manager to communicate through network firewalls and proxy servers.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/24/2020
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Configuring a Firewall for Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

This section describes how to configure your firewall to allow communication between the different Operations Manager features on your network.  

> [!NOTE]
> Operations Manager uses port 389 for LDAP queries for multiple actions such as agent discovery, active directory integration, and so on. Operations Manager does not support LDAPs.
## Port assignments
The following table shows Operations Manager feature interaction across a firewall, including information about the ports used for communication between the features, which direction to open the inbound port, and whether the port number can be changed.

|Operations Manager Feature A|Port Number and Direction|Operations Manager Feature B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|Management server|1433/TCP&nbsp;--->&nbsp;<br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Operations Manager database|Yes (Setup)|WMI Port 135 (DCOM/RPC) for the initial connection and then a dynamically assigned port above 1024.  For more information, see [Special considerations for Port 135](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access#BKMK_port_135) <br>Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Management server|5723,&nbsp;5724&nbsp;--->|Management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Management server|53 (DNS)&nbsp;---><br>88 (Kerberos)&nbsp;---><br>389 (LDAP)&nbsp;--->|Domain Controllers|No|Ports 88 is used for client authentication when using Kerberos, not required if only using certificate authentication.<sup>[3](#footnote3)</sup> |
|Management server|161,162&nbsp;<--->|Network device|No|All firewalls between the management server and the network devices need to allow SNMP (UDP) and ICMP bi-directionally.|
|Gateway server|5723&nbsp;--->|Management server|No||
|Management server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Reporting data warehouse|No|Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Reporting server|5723,&nbsp;5724&nbsp;--->|Management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Operations console|5724&nbsp;--->|Management server|No||
|Operations console|80,&nbsp;443&nbsp;---><br>49152-65535&nbsp;TCP&nbsp;<--->|Management Pack Catalog web service|No|Supports downloading management packs directly in the console from the catalog.<sup>[1](#footnote1)</sup>|
|Connector framework source|51905&nbsp;--->|Management server|No||
|Web console server|5724&nbsp;--->|Management server|No||
|Web console browser|80,&nbsp;443&nbsp;--->|Web console server|Yes (IIS Admin)|Default ports for HTTP or SSL enabled.|
|Web console for Application Diagnostics|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Operations Manager database|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Web console for Application Advisor|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Reporting data warehouse|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Connected management server (Local)|5724&nbsp;--->|Connected management server (Connected)|No||
|Windows agent installed using MOMAgent.msi|5723&nbsp;--->|Management server|Yes (Setup)||
|Windows agent installed using MOMAgent.msi|5723&nbsp;--->|Gateway server|Yes (Setup)||
|Windows agent push installation, pending repair, pending update|5723/TCP<br>135/TCP<br>137/UDP<br>138/UDP<br>139/TCP<br>445/TCP<br><br>*RPC/DCOM&nbsp;High&nbsp;ports&nbsp;(2008&nbsp;OS&nbsp;and&nbsp;later)<br>Ports&nbsp;49152-65535&nbsp;TCP||Communication is initiated from MS/GW to an Active Directory domain controller and the target computer.||
|UNIX/Linux agent discovery and monitoring of agent|TCP&nbsp;1270&nbsp;<---|Management server or Gateway server|No||
|UNIX/Linux agent for installing, upgrading, and removing agent using SSH|TCP&nbsp;22&nbsp;<---|Management server or Gateway server|Yes||
|OMED Service|TCP&nbsp;8886&nbsp;<---|Management server or Gateway server|Yes||
|Gateway server|5723&nbsp;--->|Management server|Yes (Setup)||
|Agent (Audit Collection Services forwarder)|51909&nbsp;--->|Management server Audit Collection Services collector|Yes (Registry)||
|Agentless Exception Monitoring data from client|51906&nbsp;--->|Management server Agentless Exception Monitoring file share|Yes (Client Monitoring Wizard)||
|Customer Experience Improvement Program data from client|51907&nbsp;--->|Management server (Customer Experience Improvement Program End) Point|Yes (Client Monitoring Wizard)||
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

#### <a name="footnote3"></a>Kerberos Authentication <sup>3</sup>
For Windows clients, when not using certificate-based authentication, the management server(s) will attempt to use Kerberos to validate client servers are who they say they are when the agent attempts to communicate with the management group (this is true with both agents installed through the discovery wizard and manually). This validation happens by the management server reaching out to a domain controller of the domain that the client is in, whether this is the same domain, or a trusted alternate domain from where the management server sits. 

This is typically not an issue for clients in the same domain as the management servers. However, if the client is in an alternate domain (not a DMZ or Workgroup, but something like a subsidiary's domain or dev/test domains), the management server will attempt to reach the domain controllers of this alternate domain. If this cannot happen, we may see errors in the event logs like so:

From the client:
> Log Name: Operations Manager  
> Source: OpsMgr Connector  
> Event ID: 20071  
> Level: Error  
> Computer: **clientServer.domain.b.net**  
> Description:  
> The OpsMgr Connector connected to **managementServer.domain.a.net**, but the connection was closed immediately without authentication taking place.  The most likely cause of this error is a failure to authenticate either this agent or the server.  Check the event log on the server and on the agent for events which indicate a failure to authenticate.

From a management server:
> Log Name: Operations Manager  
> Source: OpsMgr Connector  
> Event ID: 20002  
> Level: Error  
> Computer: **managementServer.domain.a.net**  
> Description:  
> A device at IP [clientServerIP]:50348 attempted to connect but could not be authenticated, and was rejected.

Another symptom could be that when using the Discovery Wizard to push agents to client machines, the process gets "stuck" after the agent is installed and monitoring never completes.

To resolve this, ensure that the following ports are open, and communications are allowed, from the management servers to the domain controllers in the client's domain:
- TCP and UDP port 389 for LDAP
- TCP and UDP port 88 for Kerberos authentication
- TCP and UDP port 53 for Domain Name Service (DNS)

Once communication is confirmed between the management server and the domain controllers, restart the HealthService on the client server.
  
