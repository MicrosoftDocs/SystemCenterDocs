---
ms.assetid: 04774952-44b7-48f5-847a-194febefcc5e
title: Set up an IPAM server in the VMM fabric
description: This article describes how to add an IP Address Management server to System Center.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 03/23/2020
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---
# Set up an IPAM server in the VMM fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article explains how to add an IP Address Management (IPAM) server to the System Center - Virtual Machine Manager (VMM) networking fabric.


An IPAM server helps you to plan, track, and manage the IP address space used in your networks.

- With an IPAM server in the VMM fabric, the IP address settings that are associated with logical networks and VM networks in VMM are synchronized using settings stored on the IPAM server.
- As an administrator you can use the IPAM server to configure and monitor logical networks and their associated network sites and IP address pools. You can also use the IPAM server to monitor the usage of VM networks that you have configured or changed in VMM.
- Tenants must continue to use the VMM server (not IPAM) to configure VM networks that use network virtualization.  In other words, to control the address space that is typically controlled by tenants rather than by VMM administrators.

## Before you start

- Make sure you have an IPAM server. [Learn more](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831353(v=ws.11)?f=255&MSPPError=-2147217396). The IPAM server can be running these versions of [Windows Servers](system-requirements.md).
- Create or identify a domain account and set it to never expire. On the IPAM server add the account to these groups:
	- **IPAM ASM Administrators**: A local group that exists on all IPAM servers, and provides permissions for IP address space management (ASM). For more information, see [Assign Administrator Roles](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj878348(v=ws.11)).
	- **Remote Management Users**: A built-in group that provides access to WMI resources through management protocols, such as WS-Management through the Windows Remote Management service.
- Check that the time is synchronized on the IPAM and VMM servers. This depends on settings for the Windows Time Service. If you can't synchronize them you'll need to update permissions on the IPAM software so that VMM can query the current time setting on the server. To do this, on the IPAM server run **mimgmt.msc** to open the WMI Control (Local) snap-in. Right-click **WMI Control (Local)** > **Properties** > **Security**. Navigate to **Root\CIMV2**, click the Security button Security and select the account you configured. For **Remote Enable**, select **Allow**.
- Verify the FQDN of the IPAM server to use as a connection string.
- Verify the names of the VMM host groups for which you want to use the IPAM server.
- The provider software for an IPAM server is included in VMM. You don't need to install it. You can review settings in **Settings** > **Configuration Providers**.
- If you want to use the IPAM server to delete a logical network, delete the IP address subnets assigned to that logical network, and do not delete the name associated with the **VMM Logical Network** field on the IPAM server. The two servers will then be able to synchronize correctly, and the logical network will be deleted. If you do delete the name associated with the **VMM Logical Network** field on the IPAM server,  you must go to the VMM server and delete the network sites and the logical network. Then, after the two servers synchronize, the deletion will be complete.


## Add an IPAM server to the fabric

1. Click **Fabric** > **Home** > **Show** > **Fabric Resources** > **Fabric** > **Networking** > **Network Service**. Network services include gateways, virtual switch extensions, network managers (which include IPAM servers), and top-of-rack (TOR) switches.
2. Click **Home** >**Add** > **Add Resources** > **Network Service**.
3. In **Add Network Service Wizard** > **Name** specify a name and optional description.
4. In **Manufacturer and Model** > **Manufacturer** click **Microsoft**, and click **Model** > **Microsoft Windows Server IP Address Management**.
5. In **Credentials** page specify the account you created.
6. In **Connection String** page, in the **Connection string** box, type the FQDN of the IPAM server. If you've configured a specific port on the IPAM server, end the string with the port number (for example, **:443**). If a port number is not specified, the default port for the IPAM server is used.
7. In **Provider** > **Configuration provider** > **Microsoft IP Address Management Provider**, click **Test** to run basic validation tests with the provider. Results that say **Passed** or **Failed** indicate whether the provider works as expected. One possible cause of failure is insufficient permissions in the Run As account. Results that say **Implemented** and **Not implemented** are informational only, and indicate whether the provider supports a particular API.
8. In **Host Group** select one or more host groups for which you want integration between the IPAM server and the VMM server.
9. In **Summary**  review the  settings and click **Finish**. Check that the IPAM server is listed under **Network Services**. Right-click the server > **Refresh** to get the latest settings.
10. On the IPAM server, to view the logical networks and related settings that were configured in VMM, navigate to **VIRTUALIZED IP ADDRESS SPACE**, and then to **Provider IP Address Space**. For each logical network, the IPAM server will have an address space (an overarching category that is found in IPAM, but not in VMM) with a name that is based on the name of the logical network. The logical network will be contained within the address space, with the name of the logical network displayed under the heading **VMM Logical Network**. To see the types of information that are stored in IPAM, expand the address space and select different views.

The following table can help you interpret some of the information that you see on the IPAM server:

**VMM name** | **IPAM name**
--- | ---
Logical network | VIRTUALIZED IP ADDRESS SPACE<br /> Provider IP Address Space: **VMM Logical Network** column
Network site | VIRTUALIZED IP ADDRESS SPACE<br /> Provider IP Address Space: **Network Site** column
IP address subnet |IP Address Subnet (same name in IPAM as in VMM)
IP address pool |IP Address Range
VM network | VIRTUALIZED IP ADDRESS SPACE<br /> Customer IP Address Space: **VM Network** column

## IP address reservation

IP reservation in IPAM is honored by VMM. Please follow the steps below for reserving IP addresses.

1. In IPAM, right-click **IP Address Range** for IP address reservation.
2. Click **Edit IP Address Range** and a window opens.
3. In the opened window, there is a **Reservations** tab on the left.
3. In the **Reservations** tab you can reserve IP addresses for reservation or whether to use them as VIPs.
4. Go to VMM console. Refresh the IPAM service in the network service section.
5. Now, you can see the reserved IP addresses reflected in the pool section of the logical network.

## Next steps

[Set up logical networks](network-logical.md)