---
title: VMM networking reference: using an IPAM Server in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: db9e24e8-7fa5-4c77-bd69-c7f8dda4e23e
---
# VMM networking reference: using an IPAM Server in VMM
With [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)], you can add an IP Address Management \(IPAM\) server that runs [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)] to the resources in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. After you add the IPAM server, the IP address settings that are associated with logical networks and virtual machine networks \(VM networks\) in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] are kept in synchrony with settings that are stored in the IPAM server.

> [!NOTE]
> After you add an IPAM server to your [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] configuration, you can use the IPAM server to configure and monitor logical networks and their associated network sites and IP address pools. You can also use the IPAM server to monitor the usage of VM networks that you have configured or changed in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. However, tenants must continue to use the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server \(not IPAM\) to configure VM networks that use network virtualization—in other words, to control the address space that is typically controlled by tenants rather than by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] administrators.

Use the following procedure to add an IPAM server to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)].

## <a name="BKMK_prereq"></a>Prerequisites
Before you can add an IPAM server to your configuration in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you must perform the following actions:

1.  On a server running [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)], install the IPAM feature by using **Add Roles and Features** \(in Server Manager\) or Windows PowerShell commands. Then configure the IPAM server as described in the relevant IPAM documentation. Examples of IPAM topics on TechNet are [IP Address Management (IPAM) Overview](http://technet.microsoft.com/library/hh831353.aspx) and [Checklist: Deploy IPAM Server](http://technet.microsoft.com/library/jj878325.aspx).

    > [!NOTE]
    > The IPAM server must be installed on a domain member computer, and must meet other requirements that are described in [Install IPAM Server](http://technet.microsoft.com/library/jj878315.aspx).

2.  Create or identify a domain account and, to avoid issues with expiration of the password, ensure that the account is set to never expire. Then, on the IPAM server, ensure that the account has at least the minimum necessary permissions by adding the account to the following two groups:

    -   **IPAM ASM Administrators**: A local group that exists on all IPAM servers, and provides permissions for IP address space management \(ASM\). For more information, see [Assign Administrator Roles](http://technet.microsoft.com/library/jj878348.aspx).

    -   **Remote Management Users**: A built\-in group that provides access to WMI resources through management protocols, such as WS\-Management through the Windows Remote Management service.

3.  Confirm that the IPAM server and the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server are being kept in time synchrony. Time synchrony depends on settings for the Windows Time Service. In most configurations, if two servers are in the same forest,  Windows Time Service keeps them in synchrony. For information about the Windows Time Service command, **W32tm**, and the **\/resync** option in that command, see [W32tm](http://technet.microsoft.com/library/w32tm.aspx). If you cannot control the time synchrony of the IPAM server and the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server, see the instructions in the “Important configuration notes” at the end of this topic.

4.  Make sure that you know the fully qualified domain name \(FQDN\) of the IPAM server to use as a connection string.

5.  Make sure that you know the names of the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] host groups for which you want integration between the IPAM server and the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server. You can also choose to include all host groups in the integration.

The provider software for an IPAM server running [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)] is already included in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management server in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]. You do not have to install it. If you want to review the provider software on your [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server, open the **Settings** workspace and in the **Settings** pane, click **Configuration Providers**. The list of providers appears in the **Configuration Providers** pane.

#### To add an IPAM server in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking**, and then click **Network Service**.

    Network services include gateways, virtual switch extensions, network managers \(which include IPAM servers\), and top\-of\-rack \(TOR\) switches.

4.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Network Service**.

    The **Add Network Service Wizard** opens.

5.  On the **Name** page, type a name and optional description, and then click **Next**.

6.  On the **Manufacturer and Model** page, in the **Manufacturer** list, click **Microsoft**, and in the **Model** list, click **Microsoft Windows Server IP Address Management**. Then click **Next**.

7.  On the **Credentials** page, either click **Browse** and then on the **Select a Run As Account** dialog box, specify the account described in the previous [Prerequisites](./VMM-networking-reference--using-an-IPAM-Server-in-VMM.md#BKMK_prereq) section, or click **Create Run As Account** and create a new Run As account with the permissions that are listed in the [Prerequisites](./VMM-networking-reference--using-an-IPAM-Server-in-VMM.md#BKMK_prereq) section. After you specify the account, click **Next**.

8.  On the **Connection String** page, in the **Connection string** box, type the fully qualified domain name \(FQDN\) of the IPAM server, and then click **Next**.

    For example, you might enter the following connection string:

    **IPAMserver1.contoso.com**

    If you have configured a specific port on the IPAM server, the string can also end in that port number preceded by a colon \(for example, **:443**\). If a port number is not specified, the default port for the IPAM server is used.

9. On the **Provider** page, in the **Configuration provider** list, select **Microsoft IP Address Management Provider**, and then click **Test** to run basic validation tests with the provider. If tests indicate that the provider works as expected with the IPAM server, click **Next**.

    Results that say **Passed** or **Failed** indicate whether the provider works as expected. One possible cause of failure is insufficient permissions in the Run As account. Results that say **Implemented** and **Not implemented** are informational only, and indicate whether the provider supports a particular API.

10. On the **Host Group** page, select one or more host groups for which you want integration between the IPAM server and the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server.

11. On the **Summary** page, review and confirm the settings, and then click **Finish**.

12. Confirm that the IPAM server is listed under **Network Services**. Whenever you want to send or receive the latest settings to and from the IPAM server, you can right\-click the listing for the IPAM server and then click **Refresh**.

On the IPAM server, to view the logical networks and related settings that were configured in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], navigate to **VIRTUALIZED IP ADDRESS SPACE**, and then to **Provider IP Address Space**. For each logical network, the IPAM server will have an address space \(an overarching category that is found in IPAM, but not in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]\) with a name that is based on the name of the logical network. The logical network will be contained within the address space, with the name of the logical network displayed under the heading **VMM Logical Network**. To see the types of information that are stored in IPAM, expand the address space and select different views.

The following table can help you interpret some of the information that you see on the IPAM server:

|VMM name|IPAM name|
|------------|-------------|
|Logical network|VIRTUALIZED IP ADDRESS SPACE<br /> Provider IP Address Space: **VMM Logical Network** column|
|Network site|VIRTUALIZED IP ADDRESS SPACE<br /> Provider IP Address Space: **Network Site** column|
|IP address subnet|IP Address Subnet \(same name in IPAM as in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]\)|
|IP address pool|IP Address Range|
|VM network|VIRTUALIZED IP ADDRESS SPACE<br /> Customer IP Address Space: **VM Network** column|

**Important configuration notes**

-   If you want to use the IPAM server to delete a logical network, delete the IP address subnets assigned to that logical network, and do not delete the name associated with the **VMM Logical Network** field on the IPAM server. The two servers will then be able to synchronize correctly, and the logical network will be deleted. If you do delete the name associated with the **VMM Logical Network** field on the IPAM server,  you must go to the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server and delete the network sites and the logical network. Then, after the two servers synchronize, the deletion will be complete.

-   If you cannot control the time synchrony of the IPAM server and the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] server as described in the [Prerequisites](./VMM-networking-reference--using-an-IPAM-Server-in-VMM.md#BKMK_prereq) in this topic, you must update permissions on the IPAM server so that the provider software \(included in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]\) can query the current time setting on the IPAM server. To do this, on the IPAM server, run **wmimgmt.msc** to open the **WMI Control \(Local\)** snap\-in. Right\-click **WMI Control \(Local\)**, click **Properties**, and then click the **Security** tab. Navigate to **Root\\CIMV2**, click the **Security** button, select the account that you created for the [Prerequisites](./VMM-networking-reference--using-an-IPAM-Server-in-VMM.md#BKMK_prereq) in this topic, and then for **Remote Enable**, select the **Allow** box.

## See Also
[IP Address Management (IPAM) Overview](http://technet.microsoft.com/library/hh831353.aspx)
[Overview: plan logical networks, network sites, and IP address pools in VMM](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[VMM networking reference: using a virtual switch extension manager or network manager in VMM](./VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](./VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


