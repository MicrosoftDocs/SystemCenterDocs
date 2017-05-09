---
ms.assetid: 628d7b3e-9933-4b65-b3b1-a54e1cbbaa37
title: Identify VMM ports and protocols
description: This article provides information about the ports and protocols used in a VMM 2016 deployment
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  05/07/2017
ms.topic:  reference
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Identify VMM ports and protocols

>Applies To: System Center 2016 - Virtual Machine Manager

As part of your Virtual Machine Manager (VMM) deployment, you need to plan for the ports and protocols that the Virtual Machine Manager (VMM) 2016 server and components will use, and ensure they're allowed in your infrastructure. It's important to plan this in advance. Some of the port settings are configured in VMM setup, and if you want to modify them after you set up VMM for the first time, you will need to reinstall to do so.

## Set up exceptions 

1. Identify where you need to create the firewall exception, in accordance with the table below.
2. On the server you identify, click **Start** > **Next** > **Administrative Tools** > **Windows Firewall with Advanced Security**.
2. In the **Windows Firewall with Advanced Security on Local Computer** pane, click on **Inbound Rules**.
3. In **Actions**, click **New Rule**.
4. In the **New Inbound Rule Wizard** > **Rule Type**, click on Port, and then click on Next.
5. In **Protocol and Ports**, specify the port settings in accordance with the table below, and continue in the wizard to create the rule.

## Port and protocol exceptions

**Connect** |  **Port/protocol** | **Details** | **Configure**
--- | --- | --- | ---
VMM server to VMM agent on Windows Server-based hosts/remote library server | 443:HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on hosts | Modify in VMM setup
VMM server to VMM agent on Windows Server-based hosts/remote library server | 5985:WinRM | Control channel<br/><br/> Inbound rule on hosts | Modify in VMM setup
VMM server to VMM agent on Windows Server-based hosts/remote library server | 5986:WinRM | Control channel (SSL)<br/><br/> Inbound rule on hosts | Can't modify
VMM server to VMM guest agent (VM data channel) | 443:HTTPS | BITS data channel for file transfers<br/><br/>Inbound rule on machines running the agent<br/><br/> The VMM guest agent is a special version of the VMM agent. It's is installed on VMs that are part of a service template, and on Linux VMs (with or without a service template). | Can't modify
VMM server to VMM guest agent (VM control channel) | 5985:WinRM | Control channel<br/><br/> Inbound rule on machines running the agent | Can't modify
VMM host to host | 443:HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on hosts | Modify in VMM setup
VMM server to VWware ESXi servers/Web Services | 22:SFTP<br/><br/> Inbound rule on hosts | Can't modify
VMM server to load balancer | 80:HTTP; 443:HTTPS | Channel used for load balancer management | Modify in load balancer provider 
VMM server to remote SQL Server database | 1433:TDS | SQL Server listener<br/><br/> Inbound rule on SQL Server | Modify in VMM setup
VMM server to WSUS update servers | 80/8530:HTTP; 443/8531:HTTPS | Data and control channels<br/><br/> Inbound rule on WSUS server | Can't modify from VMM
VMM library server to Hyper-V hosts | 443:HTTPS | BITS data channel for file transfers<br/><br/>Inbound rule on hosts - 443 | Modify in VMM setup
VMM console to VMM | WCF:8100 (HTTP); WCF:8101 (HTTPS); Net.TCP: 8102 | Inbound rule on VMM console machine | Modify in VMM setup 
VMM server to storage management service | WMI | Local call |  
Storage management service to SMI-S provider | CIM-XML | Provider-specific | 
VMM server to Baseboard Management Controller (BMC) | 443: HTTP (SMASH over WS-Management) | Inbound rule on BMC device | Modify on BMC device
VMM server to Baseboard Management Controller (BMC) | 623: IPMI | Inbound rule on BMC device | Modify on BMC device  
VMM server to Windows PE agent | 8101:WCF; 8103:WCF | 8101 is used for control channel, 8103 is used for time sync | Modify in VMM setup
VMM server to WDS PXE provider | | 8102: WCF | Inbound rule on PXE server |
VMM server to Hyper-V host in untrusted/perimeter domain | 443:HTTPS (BITS) | BITS data channel for file transfers<br/><br/> Inbound rule on VMM server | 
Library server to Hyper-V host in untrusted/perimeter domain | 443:HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on VMM library | 
VMM server to Windows file server | 80: WinRM; 135: RPC; 139: NetBIOS; 445: SMB (over TCP) | Used by the VMM agent<br/><br/> Inbound rule on file server |   
VMM server to Windows file server | 443:HTTPS | BITS used for file transfer<br/><br/> Inbound rule on file server | 
VMM server to Windows file server | 5985/5986:WinRM | Control channel<br/><br/> Inbound rule on file server | 

## Next steps

You can modify some of these ports and protocols during [VMM installation](install.md).




