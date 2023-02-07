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

|Operations&nbsp;Manager&nbsp;Feature&nbsp;A|Port&nbsp;Number&nbsp;and&nbsp;Direction|Operations&nbsp;Manager&nbsp;Feature&nbsp;B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|Management&nbsp;server|1433/TCP&nbsp;--->&nbsp;<br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->&nbsp;&nbsp;&nbsp;|Operations&nbsp;Manager&nbsp;database|Yes&nbsp;(Setup)|WMI&nbsp;Port&nbsp;135&nbsp;(DCOM/RPC)&nbsp;for&nbsp;the&nbsp;initial&nbsp;connection&nbsp;and&nbsp;then&nbsp;a&nbsp;dynamically&nbsp;assigned&nbsp;port&nbsp;above&nbsp;1024.&nbsp;&nbsp;For&nbsp;more&nbsp;information,&nbsp;see&nbsp;[Special&nbsp;considerations&nbsp;for&nbsp;Port&nbsp;135](/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access#BKMK_port_135)&nbsp;<br>Ports&nbsp;135,137,445,49152-65535&nbsp;are&nbsp;only&nbsp;required&nbsp;to&nbsp;be&nbsp;open&nbsp;during&nbsp;the&nbsp;initial&nbsp;Management&nbsp;Server&nbsp;installation&nbsp;to&nbsp;allow&nbsp;the&nbsp;setup&nbsp;process&nbsp;to&nbsp;validate&nbsp;the&nbsp;state&nbsp;of&nbsp;the&nbsp;SQL&nbsp;services&nbsp;on&nbsp;the&nbsp;target&nbsp;machine.&nbsp;<sup>[2](#footnote2)</sup>|
|Management&nbsp;server|5723,&nbsp;5724&nbsp;--->|management&nbsp;server|No|Port&nbsp;5724&nbsp;must&nbsp;be&nbsp;open&nbsp;to&nbsp;install&nbsp;this&nbsp;feature&nbsp;and&nbsp;can&nbsp;be&nbsp;closed&nbsp;after&nbsp;this&nbsp;feature&nbsp;has&nbsp;been&nbsp;installed.|
|Management&nbsp;server|161,162&nbsp;<--->|network&nbsp;device|No|All&nbsp;firewalls&nbsp;between&nbsp;the&nbsp;management&nbsp;server&nbsp;and&nbsp;the&nbsp;network&nbsp;devices&nbsp;need&nbsp;to&nbsp;allow&nbsp;SNMP&nbsp;(UDP)&nbsp;and&nbsp;ICMP&nbsp;bi-directionally.|
|Gateway&nbsp;server|5723&nbsp;--->|management&nbsp;server|No||
|Management&nbsp;server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->&nbsp;<br>135/TCP&nbsp;(DCOM/RPC)&nbsp;--->&nbsp;<br>137/UDP&nbsp;--->&nbsp;<br>445/TCP&nbsp;--->&nbsp;<br>49152-65535&nbsp;--->&nbsp;&nbsp;&nbsp;|Reporting&nbsp;data&nbsp;warehouse|No|Ports&nbsp;135,137,445,49152-65535&nbsp;are&nbsp;only&nbsp;required&nbsp;to&nbsp;be&nbsp;open&nbsp;during&nbsp;the&nbsp;initial&nbsp;Management&nbsp;Server&nbsp;installation&nbsp;to&nbsp;allow&nbsp;the&nbsp;setup&nbsp;process&nbsp;to&nbsp;validate&nbsp;the&nbsp;state&nbsp;of&nbsp;the&nbsp;SQL&nbsp;services&nbsp;on&nbsp;the&nbsp;target&nbsp;machine.&nbsp;<sup>[2](#footnote2)</sup>|
|Reporting&nbsp;server|5723,&nbsp;5724&nbsp;--->|management&nbsp;server|No|Port&nbsp;5724&nbsp;must&nbsp;be&nbsp;open&nbsp;to&nbsp;install&nbsp;this&nbsp;feature&nbsp;and&nbsp;can&nbsp;be&nbsp;closed&nbsp;after&nbsp;this&nbsp;feature&nbsp;has&nbsp;been&nbsp;installed.|
|Operations&nbsp;console|5724&nbsp;--->|management&nbsp;server|No||
|Operations&nbsp;console|80,&nbsp;443&nbsp;---><br>49152-65535&nbsp;TCP&nbsp;<--->|Management&nbsp;Pack&nbsp;Catalog&nbsp;web&nbsp;service|No|Supports&nbsp;downloading&nbsp;management&nbsp;packs&nbsp;directly&nbsp;in&nbsp;the&nbsp;console&nbsp;from&nbsp;the&nbsp;catalog.<sup>[1](#footnote1)</sup>|
|Connector&nbsp;framework&nbsp;source|51905&nbsp;--->|management&nbsp;server|No||
|Web&nbsp;console&nbsp;server|5724&nbsp;--->|management&nbsp;server|No||
|Web&nbsp;console&nbsp;browser|80,&nbsp;443&nbsp;--->|web&nbsp;console&nbsp;server|Yes&nbsp;(IIS&nbsp;Admin)|Default&nbsp;ports&nbsp;for&nbsp;HTTP&nbsp;or&nbsp;SSL&nbsp;enabled.|
|Web&nbsp;console&nbsp;for&nbsp;Application&nbsp;Diagnostics|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Operations&nbsp;Manager&nbsp;database|Yes&nbsp;(Setup)&nbsp;<sup>[2](#footnote2)</sup>||
|Web&nbsp;console&nbsp;for&nbsp;Application&nbsp;Advisor|1433/TCP&nbsp;---><br>&nbsp;1434&nbsp;--->|Reporting&nbsp;data&nbsp;warehouse|Yes&nbsp;(Setup)&nbsp;<sup>[2](#footnote2)</sup>||
|Connected&nbsp;management&nbsp;server&nbsp;(Local)|5724&nbsp;--->|connected&nbsp;management&nbsp;server&nbsp;(Connected)|No||
|Windows&nbsp;agent&nbsp;installed&nbsp;using&nbsp;MOMAgent.msi|5723&nbsp;--->|management&nbsp;server|Yes&nbsp;(Setup)||
|Windows&nbsp;agent&nbsp;installed&nbsp;using&nbsp;MOMAgent.msi|5723&nbsp;--->|gateway&nbsp;server|Yes&nbsp;(Setup)||
|Windows&nbsp;agent&nbsp;push&nbsp;installation,&nbsp;pending&nbsp;repair,&nbsp;pending&nbsp;update|5723/TCP<br>135/TCP<br>137/UDP<br>138/UDP<br>139/TCP<br>445/TCP<br><br>*RPC/DCOM&nbsp;High&nbsp;ports&nbsp;(2008&nbsp;OS&nbsp;and&nbsp;later)<br>Ports&nbsp;49152-65535&nbsp;TCP||Communication&nbsp;is&nbsp;initiated&nbsp;from&nbsp;MS/GW&nbsp;to&nbsp;an&nbsp;Active&nbsp;Directory&nbsp;domain&nbsp;controller&nbsp;and&nbsp;the&nbsp;target&nbsp;computer.|
|UNIX/Linux&nbsp;agent&nbsp;discovery&nbsp;and&nbsp;monitoring&nbsp;of&nbsp;agent|TCP&nbsp;1270&nbsp;<---|management&nbsp;server&nbsp;or&nbsp;gateway&nbsp;server|No||
|UNIX/Linux&nbsp;agent&nbsp;for&nbsp;installing,&nbsp;upgrading,&nbsp;and&nbsp;removing&nbsp;agent&nbsp;using&nbsp;SSH|TCP&nbsp;22&nbsp;<---|management&nbsp;server&nbsp;or&nbsp;gateway&nbsp;server|Yes||
|OMED&nbsp;Service|TCP&nbsp;8886&nbsp;<---|management&nbsp;server&nbsp;or&nbsp;gateway&nbsp;server|Yes||
|Gateway&nbsp;server|5723&nbsp;--->|management&nbsp;server|Yes&nbsp;(Setup)||
|Agent&nbsp;(Audit&nbsp;Collection&nbsp;Services&nbsp;forwarder)|51909&nbsp;--->|management&nbsp;server&nbsp;Audit&nbsp;Collection&nbsp;Services&nbsp;collector|Yes&nbsp;(Registry)||
|Agentless&nbsp;Exception&nbsp;Monitoring&nbsp;data&nbsp;from&nbsp;client|51906&nbsp;--->|management&nbsp;server&nbsp;Agentless&nbsp;Exception&nbsp;Monitoring&nbsp;file&nbsp;share|Yes&nbsp;(Client&nbsp;Monitoring&nbsp;Wizard)||
|Customer&nbsp;Experience&nbsp;Improvement&nbsp;Program&nbsp;data&nbsp;from&nbsp;client|51907&nbsp;--->|management&nbsp;server&nbsp;(Customer&nbsp;Experience&nbsp;Improvement&nbsp;Program&nbsp;End)&nbsp;Point|Yes&nbsp;(Client&nbsp;Monitoring&nbsp;Wizard)||
|Operations&nbsp;console&nbsp;(reports)|80&nbsp;--->|SQL&nbsp;Reporting&nbsp;Services|No|The&nbsp;Operations&nbsp;console&nbsp;uses&nbsp;Port&nbsp;80&nbsp;to&nbsp;connect&nbsp;to&nbsp;the&nbsp;SQL&nbsp;Reporting&nbsp;Services&nbsp;web&nbsp;site.|
|Reporting&nbsp;server|1433/TCP&nbsp;---><br>1434/UDP&nbsp;--->|Reporting&nbsp;data&nbsp;warehouse|Yes&nbsp;<sup>[2](#footnote2)</sup>||
|Management&nbsp;server&nbsp;(Audit&nbsp;Collection&nbsp;Services&nbsp;collector)|1433/TCP&nbsp;<---<br>1434/UDP&nbsp;<---|Audit&nbsp;Collection&nbsp;Services&nbsp;database|Yes&nbsp;<sup>[2](#footnote2)</sup>||

#### <a name="footnote1"></a> Management Pack Catalog Web Service <sup>1</sup>
- To access the Management Pack Catalog web service, your firewall must allow the following URL:
  1. [https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx](https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx)

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
