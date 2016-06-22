---
title: Ports and protocols for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a33f439-9e47-443d-b36c-359986260df9
---
# Ports and protocols for VMM
When you install the Virtual Machine Manager (VMM) management server, you can assign some of the ports that it will use for communications and file transfers between various VMM components and other devices. While it is a best security practice to change the default ports, not all of the ports can be changed through VMM. The default settings for the ports are listed in the following tables.

## VMM management server - source
The VMM management server communicates with various components and devices over these ports:

|Component/device connection target|Default ports(s)|Protocol(s)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper-V Host (VMM agent)|80/135/139/445|WinRM/RPC/NetBIOS/SMB (over TCP)|VMM Setup Wizard|
|Hyper-V Host (file transfer)|443|HTTPS (using BITS)||
|Hyper-V Host (control channel)|5985/5986|WS-Management|VMM Setup Wizard|
|VM Guest Agent  (file transfer)|443|HTTPS (using BITS)|Windows Registry|
|VM Guest Agent  (control channel)|5985|WS-Management||
|VMWare ESX 3.0/3.5 Host (file transfer)|22|SFTP|Windows Registry|
|VMWare ESXi Host (file transfer)|443|SSH/HTTPS (using BITS)||
|WSUS Server (data channel)|80/443|HTTP|Windows Registry|
|WSUS Server (control channel)|8530/8531|HTTPS|Windows Registry|
|SQL Server database (remote)|1433|TDS||
|Load Balancer|80/443|Load balancer config provider||
|Storage Management Service|n/a|WMI||

## VMM management server - target
The following components and devices communicate with the VMM management server over these ports:

|Component/device connection source|Default ports(s)|Protocol(s)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper-V host in untrusted domain or perimeter network (File Transfer)<br /><br />If the VMM library server is on the same computer as the VMM management server, also see the port 443 listing in the next table, [VMM Library Server](Ports-and-protocols-for-VMM.md#BKMK_library).|443|TCP|Windows Registry|
|VMM Administrator Console|8100, 8101 (HTTPS), 8102 (NET.TCP), 8103 (HTTP)|WCF|VMM Setup Wizard|
|Windows PE Agent|8101 (control), 8103 (time sync)|WCF|VMM Setup Wizard|
|WDS PXE Provider|8102|WCF|VMM Setup Wizard|

## <a name="BKMK_library"></a>VMM library server
The VMM library server communicates with various components and devices over these ports:

|Component/device connection target|Default ports(s)|Protocol(s)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper-V Host (file transfer)|443|BITS|VMM Setup Wizard|

## VMM administrator console
The VMM administrator console communicates with various components and devices over these ports:

|Component/device connection target|Default ports(s)|Protocol(s)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|VMM management server|8100, 8101 (HTTPS), 8102 (NET.TCP), 8103 (HTTP)|WCF|VMM Setup Wizard|
|Hyper-V Host|2179|RDP (using VMConnect)|VMM administrator console|
|VMWare Web Services|443|WCF|VMM administrator console|

## Other
The following miscellaneous ports are also used:

|Component/device connection target|Default ports(s)|Protocol(s)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Baseboard Management Controller|443|HTTPS (SMASH over WS-Management)|On BMC device|
|Baseboard Management Controller|623|IPMI|On BMC device|

## See Also
[Securing VMM resources](Securing-VMM-resources.md)


