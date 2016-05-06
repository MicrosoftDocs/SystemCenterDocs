---
title: Agent and Agentless Monitoring
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 281ae464-56b3-44b9-b760-13779a9056f5
---
# Agent and Agentless Monitoring
This section covers the environmental prerequisites for devices that will have agents installed and devices that will be monitored in an agentless fashion.

## Clients with Agents Installed
The three main activities involved with agent administration are discovery of target devices, deployment or installation of agents to those devices, and ongoing management of the agents. Agents that lie outside a trust boundary require a few more prerequisites than agents that lie inside a trust boundary.

### Agents Inside a Trust Boundary

#### Discovery
Discovery requires that the TCP 135 \(RPC\), RPC range, and TCP 445 \(SMB\) ports remain open and that the SMB service is enabled. For UNIX\\Linux computers, default discovery and management occurs over TCP 1270, troubleshooting, and diagnostics discovery occur over SSH, TCP 22. Discovery and deployment over SSH, default TCP 22, can also be enabled to allow [!INCLUDE[om12short](../Token/om12short_md.md)] to install the WSMAN communication layer on the discovered UNIX\/Linux computer.

#### Installation
After a target device has been discovered, an agent can be deployed to it. Agent installation requires the following:

-   Opening Remote procedure call \(RPC\) ports beginning with endpoint mapper TCP 135 and the Server Message Block \(SMB\) port TCP\/UDP 445.

-   Enabling the File and Printer Sharing for Microsoft Networks and the Client for Microsoft Networks services \(this ensures that the SMB port is active\).

-   If enabled, Windows Firewall Group Policy settings for **Allow remote administration exception** and **Allow file and printer sharing exception** must be set to **Allow unsolicited incoming messages from:** to the IP address and subnets for the primary and secondary management servers for the agent.

-   An account that has local administrator rights on the target computer.

-   Windows Installer 3.1. To install, see [Windows Installer 3.1](http://go.microsoft.com/fwlink/p/?LinkId=86322) \(article 893803\) in the Microsoft Knowledge Base.

-   Microsoft Core XML services \(MSXML\) 6 on the [!INCLUDE[om12short](../Token/om12short_md.md)] product installation media in the \\msxml subdirectory.

> [!NOTE]
> Push agent installation will install MSXML 6 on the targeted device if it is not there.

#### Ongoing Management
Ongoing management of an agent requires that the TCP 135 \(RPC\), RPC range, and TCP 445 \(SMB\) ports remain open and that the SMB service remains enabled.

### Agents Outside a Trust Boundary
For agents that lie outside the trust boundary of the management servers, the environmental prerequisites are the same as for those that lie inside a trust boundary, plus some additions.

Because the device is going to have an installed agent, the software, service, and port requirements remain the same. However, because there is no underlying infrastructure to support Kerberos authentication, certificates must be used on both sides of the connection.

To simplify the cross trust boundary configuration, you can install an [!INCLUDE[om12short](../Token/om12short_md.md)] gateway server in the same trust boundary as the devices that you will monitor. The gateway server acts as a proxy so that all communication between the management server and agents is routed through the gateway server. This communication is done over a single port, TCP 5723, and requires certificates on the management server and the gateway server. In addition, the gateway server performs discovery and installation, and relays ongoing administration traffic on behalf of the management server to the agents. The use of gateway servers also reduces the volume of network traffic and is therefore useful in low bandwidth conditions

Gateway servers can also discover and manage UNIX\/Linux computers; this is done over TCP ports 1270 and as needed SSH TCP 22, this port is configurable.

For more information about gateway server configuration, see [Deploying a Gateway Server](assetId:///b890d6e8-1363-423d-bf2b-7c7cf6d6ce5b).

### Manually Installed Agents
Discovery is not performed for manually installed agents, so there are fewer requirements.

## Agentless Monitoring
Agentless monitoring of devices is performed by either a management server or by another device that does have an agent, called a proxy agent. An agentless managed device must not be separated from its management server or proxy agent by a firewall because monitoring is performed over RPC. The action account of the agent that is performing the monitoring must have local administrative rights on the device that is being monitored.

## See Also
[Environmental Prerequisites for Operations Manager for System Center 2012](assetId:///95d59f73-5aa9-4616-b98c-30680406959a)

