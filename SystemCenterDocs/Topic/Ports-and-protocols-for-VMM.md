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
When you install the [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] management server, you can assign some of the ports that it will use for communications and file transfers between various [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] components and other devices. While it is a best security practice to change the default ports, not all of the ports can be changed through [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. The default settings for the ports are listed in the following tables.

## [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server \- source
The [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server communicates with various components and devices over these ports:

|Component\/device connection target|Default ports\(s\)|Protocol\(s\)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper\-V Host \([!INCLUDE[vmm12short](../Token/vmm12short_md.md)] agent\)|80\/135\/139\/445|WinRM\/RPC\/NetBIOS\/SMB \(over TCP\)|VMM Setup Wizard|
|Hyper\-V Host \(file transfer\)|443|HTTPS \(using BITS\)||
|Hyper\-V Host \(control channel\)|5985\/5986|WS\-Management|VMM Setup Wizard|
|VM Guest Agent  \(file transfer\)|443|HTTPS \(using BITS\)|Windows Registry|
|VM Guest Agent  \(control channel\)|5985|WS\-Management||
|VMWare ESX 3.0\/3.5 Host \(file transfer\)|22|SFTP|Windows Registry|
|VMWare ESXi Host \(file transfer\)|443|SSH\/HTTPS \(using BITS\)||
|WSUS Server \(data channel\)|80\/443|HTTP|Windows Registry|
|WSUS Server \(control channel\)|8530\/8531|HTTPS|Windows Registry|
|SQL Server database \(remote\)|1433|TDS||
|Load Balancer|80\/443|Load balancer config provider||
|Storage Management Service|n\/a|WMI||

## [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server \- target
The following components and devices communicate with the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server over these ports:

|Component\/device connection source|Default ports\(s\)|Protocol\(s\)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper\-V host in untrusted domain or perimeter network \(File Transfer\)<br /><br />If the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server is on the same computer as the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server, also see the port 443 listing in the next table, [VMM Library Server](../Topic/Ports-and-protocols-for-VMM.md#BKMK_library).|443|TCP|Windows Registry|
|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Administrator Console|8100, 8101 \(HTTPS\), 8102 \(NET.TCP\), 8103 \(HTTP\)|WCF|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Setup Wizard|
|Windows PE Agent|8101 \(control\), 8103 \(time sync\)|WCF|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Setup Wizard|
|WDS PXE Provider|8102|WCF|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Setup Wizard|

## <a name="BKMK_library"></a>[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server
The [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library server communicates with various components and devices over these ports:

|Component\/device connection target|Default ports\(s\)|Protocol\(s\)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Hyper\-V Host \(file transfer\)|443|BITS|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Setup Wizard|

## [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] administrator console
The [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] administrator console communicates with various components and devices over these ports:

|Component\/device connection target|Default ports\(s\)|Protocol\(s\)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server|8100, 8101 \(HTTPS\), 8102 \(NET.TCP\), 8103 \(HTTP\)|WCF|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] Setup Wizard|
|Hyper\-V Host|2179|RDP \(using VMConnect\)|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] administrator console|
|VMWare Web Services|443|WCF|[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] administrator console|

## Other
The following miscellaneous ports are also used:

|Component\/device connection target|Default ports\(s\)|Protocol\(s\)|Where to change port settings|
|---------------------------------------|----------------------|-----------------|---------------------------------|
|Baseboard Management Controller|443|HTTPS \(SMASH over WS\-Management\)|On BMC device|
|Baseboard Management Controller|623|IPMI|On BMC device|

## See Also
[Securing VMM resources](../Topic/Securing-VMM-resources.md)

