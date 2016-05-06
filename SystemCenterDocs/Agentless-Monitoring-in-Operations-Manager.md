---
title: Agentless Monitoring in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b25d0f-9316-42d2-aeb9-4ba0b0afc6cf
---
# Agentless Monitoring in Operations Manager
[!INCLUDE[om12long](Token/om12long_md.md)] can gather performance and availability data on a computer that does not have an agent installed by using a proxy agent that is installed on another computer. Use agentless\-monitoring of computers when it is not possible or desirable to install an agent on a computer.

An agentless\-managed computer is a Windows\-based computer that is discovered by using the Operations console. You assign an management server or agent\-managed computer to provide remote \(proxy\) agent functionality for the computers.

Agentless\-managed computers are managed as if there is an agent installed on them. Not all management packs work in agentless mode. For more information, see the documentation for the management packs you are running.

> [!IMPORTANT]
> Agentless management of a computer will not work if the agentless\-managed computer and its proxy communicate through a firewall. A management server will not collect descriptions for events or publishers that are present on an agentless managed computer but are not present on the proxy agent.

For information about configuring an agent\-managed computer as a proxy for agentless\-managed computers, see [How to Configure a Proxy for Agentless Monitoring](How-to-Configure-a-Proxy-for-Agentless-Monitoring.md).

> [!IMPORTANT]
> An agentless\-managed computer places greater resource requirements on a management server than an agent\-managed computer.

To change an agentless\-managed computer to an agent\-managed computer, do the following:

1.  Delete the agentless\-managed computer from the management group by right\-clicking the computer in **Agentless Managed** in the **Administration** workspace and then clicking **Delete**.

2.  Deploy the agent to the computer. For more information, see [Managing Discovery and Agents](Managing-Discovery-and-Agents.md).

## Agentless Monitoring Compared to Agentless Exception Monitoring
Agentless monitoring provides monitoring of computers without agents by using a proxy agent and applying those management packs that support agentless monitoring. Agentless Exception Monitoring \(AEM\) redirects hardware, operating system, and application crash information to Operations Manager, which can aggregate, view, and report on error reports that are sent by the Windows Error Reporting service. For information on AEM, see [Client Monitoring Using Agentless Exception Monitoring in Operations Manager](Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md).

You can monitor a computer without an agent by using either agentless monitoring, AEM, or both.

## Agentless Monitoring in Operations Manager topics

-   [How to Configure a Computer for Agentless Management](How-to-Configure-a-Computer-for-Agentless-Management.md)

-   [How to Configure a Proxy for Agentless Monitoring](How-to-Configure-a-Proxy-for-Agentless-Monitoring.md)

## Other resources for this component

-   [TechNet Library main page for Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=223634)

-   [Operations Guide for System Center 2012 - Operations Manager](Operations-Guide-for-System-Center-2012---Operations-Manager.md)

-   [Initial Monitoring After Operations Manager Is Installed](Initial-Monitoring-After-Operations-Manager-Is-Installed.md)

-   [Managing Access in Operations Manager](Managing-Access-in-Operations-Manager.md)

-   [Getting Information from Operations Manager](Getting-Information-from-Operations-Manager.md)

-   [General Tasks in Operations Manager_1](General-Tasks-in-Operations-Manager_1.md)

-   [Maintenance of Operations Manager](Maintenance-of-Operations-Manager.md)

-   [Operations Manager Report Authoring Guide](http://go.microsoft.com/fwlink/p/?LinkID=217092)

-   [Managing Discovery and Agents](Managing-Discovery-and-Agents.md)

## See Also
[How to Configure a Computer for Agentless Management](How-to-Configure-a-Computer-for-Agentless-Management.md)
[How to Configure a Proxy for Agentless Monitoring](How-to-Configure-a-Proxy-for-Agentless-Monitoring.md)


