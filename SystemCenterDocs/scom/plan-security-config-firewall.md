---
ms.assetid: 045b2f66-b672-4cd2-9d83-9d067b83fdaf
title: Configure a Firewall for Operations Manager
description: This article provides design guidance for which ports and protocols need to be allowed for Operations Manager to communicate through network firewalls and proxy servers.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Configure a Firewall for Operations Manager



This section describes how to configure your firewall to allow communication between the different Operations Manager features on your network.  

> [!NOTE]
> Operations Manager does not support LDAP over SSL (LDAPS) at this time.

## Port assignments

The following table shows Operations Manager feature interaction across a firewall, including information about the ports used for communication between the features, which direction to open the inbound port, and whether the port number can be changed.

|Operations Manager Feature A|Port Number and Direction|Operations Manager Feature B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|Management server|1433/TCP&nbsp;--->&nbsp;<br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Operations Manager database|Yes (Setup)|WMI Port 135 (DCOM/RPC) for the initial connection and then a dynamically assigned port above 1024. For more information, see [Special considerations for Port 135](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access#BKMK_port_135) <br><br>Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Management server|5723/TCP,&nbsp;5724/TCP&nbsp;--->|Management server|No|Port 5724/TCP must be open to install this feature and can be closed after installation.|
|Management server, Gateway Server|53 (DNS)&nbsp;---><br>88 (Kerberos)&nbsp;---><br>389 (LDAP)&nbsp;--->|Domain Controllers|No|Port 88 is used for Kerberos authentication, and isn't required if only using certificate authentication.<sup>[3](#footnote3)</sup> |
|Management server|161,162&nbsp;<--->|Network device|No|All firewalls between the management server and the network devices need to allow SNMP (UDP) and ICMP bi-directionally.|
|Gateway server|5723/TCP&nbsp;--->|Management server|No||
|Management server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->|Reporting data warehouse|No|Ports 135,137,445,49152-65535 are only required to be open during the initial Management Server installation to allow the setup process to validate the state of the SQL services on the target machine. <sup>[2](#footnote2)</sup>|
|Reporting server|5723/TCP,&nbsp;5724/TCP&nbsp;--->|Management server|No|Port 5724/TCP must be open to install this feature and can be closed after installation.|
|Operations console|5724/TCP&nbsp;--->|Management server|No||
|Operations console|80,&nbsp;443&nbsp;---><br>49152-65535&nbsp;TCP&nbsp;<--->|Management Pack Catalog web service|No|Supports downloading management packs directly in the console from the catalog.<sup>[1](#footnote1)</sup>|
|Connector framework source|51905&nbsp;--->|Management server|No||
|Web console server|5724/TCP&nbsp;--->|Management server|No||
|Web console browser|80,&nbsp;443&nbsp;--->|Web console server|Yes (IIS Admin)|Default ports for HTTP or SSL enabled.|
|Web console for Application Diagnostics|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Operations Manager database|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Web console for Application Advisor|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Reporting data warehouse|Yes (Setup) <sup>[2](#footnote2)</sup>||
|Connected management server (Local)|5724/TCP&nbsp;--->|Connected management server (Connected)|No||
|Windows agent installed using MOMAgent.msi|5723/TCP&nbsp;--->|Management server|Yes (Setup)||
|Windows agent installed using MOMAgent.msi|5723/TCP&nbsp;--->|Gateway server|Yes (Setup)||
|Windows agent push installation, pending repair, pending update|5723/TCP<br>135/TCP<br>137/UDP<br>138/UDP<br>139/TCP<br>445/TCP<br><br>*RPC/DCOM&nbsp;High&nbsp;ports&nbsp;(2008&nbsp;OS&nbsp;and&nbsp;later)<br>Ports&nbsp;49152-65535&nbsp;TCP||No|Communication is initiated from MS/GW to an Active Directory domain controller and the target computer.|
|UNIX/Linux agent discovery and monitoring of agent|TCP&nbsp;1270&nbsp;<---|Management server or Gateway server|No||
|UNIX/Linux agent for installing, upgrading, and removing agent using SSH|TCP&nbsp;22&nbsp;<---|Management server or Gateway server|Yes||
|OMED Service|TCP&nbsp;8886&nbsp;<---|Management server or Gateway server|Yes||
|Gateway server|5723/TCP&nbsp;--->|Management server|Yes (Setup)||
|Agent (Audit Collection Services forwarder)|51909&nbsp;--->|Management server Audit Collection Services collector|Yes (Registry)||
|Agentless Exception Monitoring data from client|51906&nbsp;--->|Management server Agentless Exception Monitoring file share|Yes (Client Monitoring Wizard)||
|Customer Experience Improvement Program data from client|51907&nbsp;--->|Management server (Customer Experience Improvement Program End) Point|Yes (Client Monitoring Wizard)||
|Operations console (reports)|80&nbsp;--->|SQL Reporting Services|No|The Operations console uses Port 80 to connect to the SQL Reporting Services web site.|
|Reporting server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->|Reporting data warehouse|Yes <sup>[2](#footnote2)</sup>||
|Management server (Audit Collection Services collector)|1433/TCP&nbsp;<---<br>1434/UDP&nbsp;<---|Audit Collection Services database|Yes <sup>[2](#footnote2)</sup>||

### <a name="footnote1"></a> Management Pack Catalog web service <sup>1</sup>

To access the Management Pack Catalog web service, your firewall and/or proxy server must allow the following URL and wildcard (*):

- `https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx`
- `http://go.microsoft.com/fwlink/*`

### <a name="footnote2"></a> Identify SQL port <sup>2</sup>

- The default SQL port is 1433, however this port number can be customized based on organizational requirements. To identify the configured port, follow these steps:
    1. In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**, expand **Protocols** for \<instance name\>, and then double-click **TCP/IP**.
    2. In the **TCP/IP Properties** dialog, on the **IP Addresses** tab, note the port value for **IPAll**.  

- If using a SQL Server configured with an Always On Availability Group or after migrating an installation, do the following to identify the port:  
    1. In Object Explorer, connect to a server instance that hosts any availability replica of the availability group whose listener you want to view. Select the server name to expand the server tree.
    2. Expand the **Always On High Availability** node and the **Availability Groups** node.
    3. Expand the node of the availability group, and expand the **Availability Groups Listeners** node.
    4. Right-click the listener that you want to view, and select the **Properties** command, opening the **Availability Group Listener Properties** dialog window, where the configured port should be available.

### <a name="footnote3"></a>Kerberos authentication <sup>3</sup>

For Windows clients using Kerberos authentication, and reside in a different domain from where the management servers are located, there are extra requirements that that must be met:

1. A [two-way transitive trust](/entra/identity/domain-services/concepts-forest-trust) must be established between domains.
1. The following ports must be open between the domains:
   1. TCP/UDP port 389 for LDAP.
   1. TCP/UDP port 88 for Kerberos.
   1. TCP/UDP port 53 for Domain Name Service (DNS).

## See also

- [Kerberos authentication troubleshooting guidance](/troubleshoot/windows-server/windows-security/kerberos-authentication-troubleshooting-guidance)
- [Troubleshoot agent connectivity issues in Operations Manager](/troubleshoot/system-center/scom/troubleshoot-agent-connectivity-issues)
