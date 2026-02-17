---
ms.assetid: 628d7b3e-9933-4b65-b3b1-a54e1cbbaa37
title: Identify VMM ports and protocols
description: This article provides information about the ports and protocols used in a VMM 2016 deployment
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/15/2024
ms.topic: how-to
ms.update-cycle: 180-days
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: engagement-fy24
---

# Identify VMM ports and protocols

As part of your System Center Virtual Machine Manager (VMM) deployment, you need to allow access for the ports and protocols that the VMM server and components will use. It's important to plan this in advance. Some of the port settings are configured in VMM setup, and if you want to modify them after you set up VMM for the first time, you'll need to reinstall to do so.

## Set up exceptions

1. Identify where you need to create firewall exceptions, in accordance with the table below.
2. On the server you identify, select **Start** > **Next** > **Administrative Tools** > **Windows Firewall with Advanced Security**.
2. In the **Windows Firewall with Advanced Security on Local Computer** pane, select on **Inbound Rules**.
3. In **Actions**, select **New Rule**.
4. In the **New Inbound Rule Wizard** > **Rule Type**, select **Port**, and then select **Next**.
5. In **Protocol and Ports**, specify the port settings in accordance with the table below and continue in the wizard to create the rule.

## General ports and protocol exceptions

**Connect** |  **Port/protocol** | **Details** | **Configure**
--- | --- | --- | ---
VMM server to VMM agent on Windows Server-based hosts/remote library server | 80: WinRM; 135: RPC; 139: NetBIOS;   445: SMB (over TCP)| Used by the VMM agent <br/><br/> Inbound rule on hosts | Can't modify
VMM server to VMM agent on Windows Server-based hosts/remote library server | 443: HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on hosts | Modify in VMM setup
VMM server to VMM agent on Windows Server-based hosts/remote library server | 5985: WinRM | Control channel<br/><br/> Inbound rule on hosts | Modify in VMM setup
VMM server to VMM agent on Windows Server-based hosts/remote library server | 5986: WinRM | Control channel (SSL)<br/><br/> Inbound rule on hosts | Can't modify
VMM server to VMM guest agent (VM data channel) | 443: HTTPS | BITS data channel for file transfers<br/><br/>Inbound rule on machines running the agent<br/><br/> The VMM guest agent is a special version of the VMM agent. It's installed on VMs that are part of a service template and on Linux VMs (with or without a service template). | Can't modify
VMM server to VMM guest agent (VM control channel) | 5985: WinRM | Control channel<br/><br/> Inbound rule on machines running the agent | Can't modify
VMM host to host | 443: HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on hosts and VMM server | Modify in VMM setup
VMM server to VMware ESXi servers/Web Services | 22: SFTP<br/><br/> Inbound rule on hosts | Can't modify
VMM server to load balancer | 80: HTTP; 443: HTTPS | Channel used for load balancer management | Modify in load balancer provider
VMM server to remote SQL Server database | 1433: TDS | SQL Server listener<br/><br/> Inbound rule on SQL Server | Modify in VMM setup
VMM server to WSUS update servers | 80/8530: HTTP; 443/8531: HTTPS | Data and control channels<br/><br/> Inbound rule on WSUS server | Can't modify from VMM
VMM library server to Hyper-V hosts | 443: HTTPS | BITS data channel for file transfers<br/><br/>Inbound rule on hosts - 443 | Modify in VMM setup
VMM console to VMM | WCF: 8100 (HTTP); WCF: 8101 (HTTPS); Net.TCP: 8102 | Inbound rule on VMM console machine | Modify in VMM setup
VMM server to storage management service | WMI | Local call |  
Storage management service to SMI-S provider | CIM-XML | Provider-specific |
VMM server to Baseboard Management Controller (BMC) | 443: HTTP (SMASH over WS-Management) | Inbound rule on BMC device | Modify on BMC device
VMM server to Baseboard Management Controller (BMC) | 623: IPMI | Inbound rule on BMC device | Modify on BMC device  
VMM server to Windows PE agent | 8101: WCF; 8103: WCF | 8101 is used for control channel; 8103 is used for time sync | Modify in VMM setup
VMM server to WDS PXE provider | | 8102: WCF | Inbound rule on PXE server |
VMM server to Hyper-V host in untrusted/perimeter domain | 443: HTTPS (BITS) | BITS data channel for file transfers<br/><br/> Inbound rule on VMM server |
Library server to Hyper-V host in untrusted/perimeter domain | 443: HTTPS | BITS data channel for file transfers<br/><br/> Inbound rule on VMM library |
VMM server to Windows file server | 80: WinRM; 135: RPC; 139: NetBIOS; 445: SMB (over TCP) | Used by the VMM agent<br/><br/> Inbound rule on file server |
VMM server to Windows file server | 443: HTTPS | BITS used for file transfer<br/><br/> Inbound rule on file server |
VMM server to Windows file server | 5985/5986: WinRM | Control channel<br/><br/> Inbound rule on file server |

## VMware vCenter server and ESXi hosts management related ports and protocol exceptions

**Connect** |  **Port/protocol** | **Details** | **Configure**
--- | --- | --- | ---
VMM server to VMware vCenter server | 443: HTTPS | Inbound rule on VMware vCenter server | Can't modify
VMware vCenter server to VMM server | 443: HTTPS | Outbound rule on VMware vCenter server | Can't modify
VMM server to VMware ESXi nodes | 22: SFTP <br> 443: HTTPS | Inbound rule on ESXi nodes | Can't modify
VMware ESXi nodes to Hyper-V node | 443: HTTPS <br> 445: SMB (over TCP) | Outbound rule on ESXi nodes | Can't modify
VMware ESXi nodes to VMM server | 443: HTTPS | Outbound rule on ESXi nodes | Can't modify |


> [!NOTE]
> In addition to the above ports, VMM relies on the default dynamic port range for all its communication with Hyper-V hosts, file servers, and library servers.  [Learn more](https://support.microsoft.com/en-in/help/929851/the-default-dynamic-port-range-for-tcp-ip-has-changed-in-windows-vista) about the dynamic port range. We recommend that you reconfigure the firewalls to allow traffic between servers in the dynamic port range of 49152 through 65535.

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
> [!NOTE]
> System Center Virtual Machine Manager uses NTLM authentication protocol to perform management operations. Using Kerberos authentication protocol isn’t recommended as it can break a few VM operations.
::: moniker-end

## Next steps

You can modify some of these ports and protocols during [VMM installation](install.md).
