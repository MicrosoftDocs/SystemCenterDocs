---
ms.assetid: 628d7b3e-9933-4b65-b3b1-a54e1cbbaa37
title: VMM ports and protocols
description: This article provides information about ports and protocols used in a VMM 2016 deployment
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  12/15/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# VMM ports and protocols

>Applies To: System Center 2016 - Virtual Machine Manager

This article summarizes the ports and protocols used by System Center 2016 - Virtual Machine Manager (VMM).

## VMM management server (source)

Ports and protocols used to communicate from the VMM management server.

**Connection target** |  **Port/protocol** | **Modify settings**
--- | --- | ---
Hyper-V host (VMM agent) | 80: WinRM<br/><br/> 135: RPC<br/><br/> 139: NetBIOS<br/><br/> 445: SMB (over TCP) | VMM setup
Hyper-V host (file transfer) | 443: HTTPS (using BITS) |
Hyper-V host (control channel) | 5985, 5986: WS-Management | VMM setup
VM guest agent (file transfer) | 443: HTTPS (using BITS) | Registry
VM guest agent (control channel) | 5985: WS-Management |
VMware ESX 3.0/3.5 host (file transfer) | 22: SFTP |
VMware ESXi host (data channel) | 443: HTTPS (using BITS) |
WSUS server (data channel) | 80: HTTP<br/><br/> 443: HTTPS | Registry
WSUS server (control channel) | 8540, 8531: HTTPS | Registry
SQL Server database (remote) | 1433: TDS |
Load balancer | 80, 443: Load balancer config provider |
Storage management service | NA: WMI |
VMM library server on the VMM management server | 443: BITS | VMM setup
Baseboard Management Controller (BMC) | 443: HTTP (SMASH over WS-Management) | BMC device
Baseboard Management Controller (BMC) | 623: IPMI | BMC device
Hyper-V host | NA | ICMP (Ping) | Windows Firewall and network devices

## VMM management server (target)

Ports and protocols used to communicate to the VMM management server.

**Connection source** |  **Port/protocol** | **Modify settings**
--- | --- | ---
Hyper-V host in untrusted domain/perimeter network<br/><br/> (file transfer) | 443: (TCP) | VMM setup
VMM console on different computer | 8100, 8101 (HTTPS), 8102 (NET.TCP), 8103 (HTTP): WCF | VMM setup
Windows PE agent | 8101 (control), 8103 (time sync): WCF | VMM setup
WDS PXE provider) | 8102: WCF | VMM setup


## VMM admin console

Ports and protocols used by the admin console

**Connection target** |  **Port/protocol** | **Modify settings**
--- | --- | ---
VMM management server | 8100, 8101 (HTTPS), 8102 (NET.TCP), 8103 (HTTP): WCF | VMM setup
Hyper-V host | 2179: RDP (using VMConnect) | VMM console
VMware Web Services | 443: WCF | VMM console

## Storage file server

Ports and protocols used for storage connections.

**Connection target** |  **Port/protocol** | **Modify settings**
--- | --- | ---
Windows file server<br/><br/> (VMM agent) | 80: WinRM<br/><br/> 135: RPC<br/><br/> 139: NetBIOS<br/><br/> 445: SMB (over TCP) | VMM setup
Windows file server<br/><br/> (file transfer) | 443: HTTPS (using BITS) |
Windows file server<br/><br/> (control channel) | 5985/5986: WS-Management | VMM setup
Windows file server | CredSSP |
