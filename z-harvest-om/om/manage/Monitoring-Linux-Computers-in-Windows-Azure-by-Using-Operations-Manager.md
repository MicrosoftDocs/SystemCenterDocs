---
title: Monitoring Linux Computers in Windows Azure by Using Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 801c28e1-653c-4c70-8889-fb4e7d5c7ce3
author:mgoedtel
manager:cfreemanwa
---
# Monitoring Linux Computers in Windows Azure by Using Operations Manager
[!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] provides monitoring of Linux computers both in your data center and hosted as persistent virtual machines in Windows Azure. This topic describes considerations for monitoring of Linux virtual machines in Windows Azure.  
  
## <a name="bkmk_topologies"></a>Supported Topologies  
Monitoring of Linux computers running as persistent virtual machines in Windows Azure is supported in the following topologies:  
  
-   [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] and supporting services \(SQL Server and Active Directory\) deployed in your on\-premises data center with a site\-to\-site VPN connection to the Windows Azure virtual network where the Linux virtual machines are deployed.  
  
    -   More information about Windows Azure site\-to\-site VPN connections can be found [here](https://go.microsoft.com/fwlink/?LinkId=325539).  
  
-   [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] and supporting services \(SQL Server and Active Directory\) deployed in Windows Azure, with virtual network connectivity between the Operations Manager Management Server and Linux virtual machines.  
  
> [!NOTE]  
> [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] monitoring of Linux virtual machines in Windows Azure over the public Internet without a VPN connection is not a supported configuration.  
  
## Supported Linux Operating Systems  
All Linux operating systems and versions supported both by [!INCLUDE[omblue_1](../../om/manage/includes/omblue_1_md.md)] and Windows Azure are supported for monitoring in the [Supported Topologies](../../om/manage/Monitoring-Linux-Computers-in-Windows-Azure-by-Using-Operations-Manager.md#bkmk_topologies) section above.  
  
For more information about supported Linux operating systems, see the following:  
  
-   [System Center 2012 R2 - Operations Manager supported Linux operating systems](https://go.microsoft.com/fwlink/?LinkID=325541)  
  
-   [Windows Azure supported Linux operating systems](https://go.microsoft.com/fwlink/?LinkID=325542)  
  
## Certificate and Name Resolution Requirements  
Whether Linux computers are running on\-premises or in Windows Azure, the following requirements for [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] monitoring of Linux computers apply:  
  
-   The Management Server can resolve the fully\-qualified domain name and IP address of the managed Linux computer with forward and reverse DNS lookups.  
  
-   The agent certificate on the Linux computer is created with the fully\-qualified domain name \(for the Linux computer\) that the Management Server uses to identify the Linux computer.  
  
For Linux virtual machines deployed in Windows Azure, additional configuration may be required to meet the certificate configuration requirements, as the fully\-qualified domain name known locally to the Linux computer may not be the FQDN used to reach the Linux computer. The following options can be used to ensure that the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)]agent is able to generate a certificate with the correct FQDN during agent installation.  
  
#### Option 1: Edit \/etc\/hosts  
  
1.  Confirm that `/etc/nsswitch.conf` \(on the Linux VM\) is configured to prioritize **files** before DNS.  
  
2.  Edit `/etc/hosts` so that an entry for the host exists with the following format:  
  
    <*IP Address*> <*hostname*> <*fully\-qualified domain name*>  
  
    For example, reference the entry in the following hosts file for the linuxvm1.contoso.com host.  
  
    ```  
    # IP-Address  Full-Qualified-Hostname  Short-Hostname  
  
    127.0.0.1       localhost  
    192.168.1.124   linuxvm1        linuxvm1.contoso.com  
    ::1             localhost ipv6-localhost ipv6-loopback  
    ```  
  
#### Option 2: Configure DNS and DNS Search Suffixes  
  
1.  Configure the Windows Azure virtual network with your DNS server addresses.  More information can be found [here](https://go.microsoft.com/fwlink/?LinkID=325543).  
  
2.  Configure the appropriate DHCP client settings on the Linux virtual machines so that the correct search suffix is configured \(in `/etc/resolv.conf`\).  The following steps demonstrate this configuration on CentOS, SUSE Linux Enterprise Server, and Ubuntu Server.  
  
    **CentOS**  
  
    1.  Edit the interface configuration script for eth0 \(`/etc/sysconfig/network-scripts/ifcfg-eth0`\).  Add a **SEARCH** entry to the `ifcfg-eth0 script`.  For example, if your domain name is contoso.com, the SEARCH entry to add is:  
  
        ```  
        SEARCH="contoso.com"  
        ```  
  
    2.  Restart the network service:  
  
        ```  
        service network restart  
        ```  
  
    **SUSE Linux Enterprise Server**  
  
    1.  Edit the netconfig file:  
  
        ```  
        /etc/sysconfig/network/config  
        ```  
  
    2.  Set the following property values in the file:  
  
        ```  
        NETCONFIG_DNS_POLICY="STATIC"  
        NETCONFIG_DNS_STATIC_SEARCHLIST="<your DNS search suffixes>"  
        NETCONFIG_DNS_STATIC_SERVERS="<your DNS server addresses>"  
        ```  
  
        For example:  
  
        ```  
        ## Type:        string  
        ## Default:     "auto"  
        #  
        # Defines the DNS merge policy as documented in netconfig(8) manual page.  
        # Set to "" to disable DNS configuration.  
        #  
        NETCONFIG_DNS_POLICY="STATIC"  
  
        ## Type:        string  
        ## Default:     "resolver"  
        #  
        # Defines the name of the DNS forwarder that has to be configured.  
        #  
        NETCONFIG_DNS_FORWARDER="resolver"  
  
        ## Type:        string  
        ## Default:     ""  
        #  
        # List of DNS domain names used for host-name lookup.  
        #  
        NETCONFIG_DNS_STATIC_SEARCHLIST="contoso.com"  
  
        ## Type:        string  
        ## Default:     ""  
        #  
        # List of DNS nameserver IP addresses to use for host-name lookup.  
        #  
        NETCONFIG_DNS_STATIC_SERVERS="192.168.1.8"  
  
        ```  
  
    3.  Restart the network service:  
  
        ```  
        service network restart  
        ```  
  
    **Ubuntu Server**  
  
    1.  Edit the interface configuration file \(`/etc/network/interfaces`\).  
  
    2.  Add a **dns\-search** entry to the configuration for **eth0** to define the DNS search suffixes.  For example:  
  
        ```  
        # The primary network interface  
        auto eth0  
        iface eth0 inet dhcp  
        dns-search contoso.com  
        ```  
  
    3.  Restart the network service:  
  
        ```  
        /etc/init.d/networking restart  
        ```  
  
### Correcting Certificate Issues  
If the agent certificate was created with an incorrect fully\-qualified domain name for the Linux virtual machine, the **scxsslconfig** utility can be used to regenerate the certificate.  More information and troubleshooting steps can be found [here](https://go.microsoft.com/fwlink/?LinkID=325544).  
  
## Additional Configuration  
The following additional configuration steps may be necessary when managing Linux virtual machines in Windows Azure with [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)].  
  
### Create a Group for Linux Computers hosted in Windows Azure  
To simplify override configuration of rules and monitors, it is recommended to create a Group in [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] that contains the Linux computer instances that are hosted in Windows Azure.  
  
1.  In the **Operations Console**, navigate to the **Authoring** pane.  
  
2.  Click **Groups**, and click **New Group**. This group will be used to identify Linux virtual machines in Windows Azure.  
  
3.  Provide a name and description for the group, and select a destination management pack.  
  
4.  Either add each discovered Linux computer that is hosted in Windows Azure as an **Explicit Member** to the group, or create **Dynamic Inclusion** rules that populate the group with Linux computers, based on a name or IP address pattern.  
  
5.  Complete the Group Creation Wizard.  
  
### Disable Available Swap Space monitors  
Linux virtual machines created from Gallery images do not have swap space configured by default. This will cause the Available Swap Space monitors to generate alerts for the Linux virtual machines. It is recommended to disable these monitors with an override for Linux virtual machines in Windows Azure.  
  
1.  In the **Operations Console**, navigate to the **Authoring** pane.  
  
2.  Expand **Management Pack Objects** and click **Monitors**.  
  
3.  Search for the string: "Available Megabytes Swap" in the top search bar.  
  
    There will be one monitor with the name: **Operating System Available Megabytes Swap Space** for each Linux operating system and version. For each of these that apply to the Linux virtual machines hosted in Windows Azure, right\-click the monitor, and then select **Overrides \-> Override the Monitor \-> For a Group**.  
  
4.  Select the group created in the previous exercise that identifies Linux computers in Windows Azure.  
  
5.  Check the box next to the **Enabled** parameter, and set the **Override Value** to **False**.  
  
6.  Select the destination management pack, and click **OK**.  
  
### Disable the ACPI Daemon Monitor for SUSE Linux Enterprise Server Computers  
The SUSE Linux Enterprise Server management packs include a default monitor for the acpi daemon \(acpid\). This daemon is not enabled by default in the SUSE Linux Enterprise Server images in the Windows Azure Gallery.  This monitor should be disabled for any SUSE Linux Enterprise Server computer hosted in Windows Azure.  
  
1.  In the **Operations Console**, navigate to the **Authoring** pane.  
  
2.  Expand **Management Pack Objects** and click **Monitors**.  
  
3.  Search for the string: "Process Acpi" in the top search bar.  
  
    There will be one monitor with the name: **Process Acpi Service Health** for each SUSE Linux Enterprise Server version. For each of these that apply to the Linux virtual machines hosted in Windows Azure, right click the monitor, and then select **Overrides \-> Override the Monitor \-> For a Group**.  
  
4.  Select the group created in the previous exercise that identifies Linux computers in Windows Azure.  
  
5.  Check the box next to the **Enabled** parameter, and set the **Override Value** to **False**.  
  
6.  Select the destination management pack, and click **OK**.  
  
## Additional Resources  
  
-   [Monitoring UNIX and Linux Computers by Using Operations Manager](https://go.microsoft.com/fwlink/?LinkID=325545)  
  
-   [Install Agent on UNIX and Linux Using the Discovery Wizard](https://go.microsoft.com/fwlink/?LinkID=325546)  
  
-   [Accessing UNIX and Linux Computers in Operations Manager](https://go.microsoft.com/fwlink/?LinkID=325547)  
  
-   [Troubleshooting UNIX\/Linux Agent Discovery in System Center 2012 \- Operations Manager](https://go.microsoft.com/fwlink/?LinkID=325548)  
  
-   [Configuring sudo Elevation for UNIX and Linux Monitoring with System Center 2012 - Operations Manager](https://go.microsoft.com/fwlink/?LinkID=325549)  
  
-   [Introduction to Linux on Windows Azure](https://go.microsoft.com/fwlink/?LinkID=325550)  
  
-   [Create a Virtual Machine Running Linux](https://go.microsoft.com/fwlink/?LinkID=325551)  
  
-   [Windows Azure Name Resolution](https://go.microsoft.com/fwlink/?LinkID=325552)  
  
