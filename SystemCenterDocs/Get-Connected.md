---
title: Get Connected
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99bd7ac1-9beb-438d-900e-426da41898b8
---
# Get Connected
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Information about roles and features in Windows Server is available on the web. You can use one or more of the following methods to access information on the web:</para>
    <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
      <thead>
        <tr>
          <TD>
            <para>Method</para>
          </TD>
          <TD>
            <para>Description</para>
          </TD>
          <TD>
            <para>More Information</para>
          </TD>
        </tr>
      </thead>
      <tbody>
        <tr>
          <TD>
            <para>Install Remote Server Administration Tools (RSAT)</para>
          </TD>
          <TD>
            <para>Remote management of servers from an Internet-connected client computer is the preferred method to access information on the web when you are administering Windows Server. To use this method, install RSAT on a client computer that has an Internet connection. The computer running RSAT must also have a network connection to the servers you want to manage. </para>
            <para>RSAT enables you to manage roles and features that are running on Windows Server from a compatible remote computer. The remote computer must be running an operating system that is compatible with the version of RSAT that is installed.</para>
            <para>With RSAT, you can use Server Manager and Microsoft Management Console snap-ins in an environment that is connected to information on the web without the need to connect remote servers to the Internet. For more information, see http://go.microsoft.com/fwlink/?linkid=404281.</para>
          </TD>
          <TD>
            <para>
              <externalLink>
                <linkText>Remote Server Administration Tools</linkText>
                <linkUri>http://go.microsoft.com/fwlink/?linkid=404281</linkUri>
              </externalLink>
            </para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>Connect the computer to the Internet</para>
          </TD>
          <TD>
            <para>Depending on the network environment in your organization, security policies might limit the type of network connections that are available to computers and devices.</para>
            <para>If permitted by security policies in your environment, you can connect a computer running Windows Server to the Internet. Details to help you get connected are provided in this topic.</para>
          </TD>
          <TD>
            <para>
              <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#connecting_local">Connecting to the Internet</link>
            </para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>Use another computer to view information on the web</para>
          </TD>
          <TD>
            <para>You can use a different computer or a mobile device to view information on the web. You might connect this computer to the computer running Windows Server by using a remote access method such as Remote Desktop Services. In this scenario, the computer you use to view information on the web does not have RSAT installed, and you must manually type the web addresses into a web browser.</para>
            <para>For more information about the roles and services that are available in this version of Windows Server, see the following resources on the Microsoft TechNet website at http://go.microsoft.com/fwlink/?linkid=306430.</para>
            <para>More information about Remote Desktop Services is available at http://go.microsoft.com/fwlink/?linkid=306532.</para>
          </TD>
          <TD>
            <para>
              <externalLink>
                <linkText>Windows Server</linkText>
                <linkUri>http://go.microsoft.com/fwlink/?linkid=306430</linkUri>
              </externalLink>
            </para>
            <para>
              <externalLink>
                <linkText>Remote Desktop Services Overview</linkText>
                <linkUri>http://go.microsoft.com/fwlink/?linkid=306532</linkUri>
              </externalLink>
            </para>
          </TD>
        </tr>
      </tbody>
    </table>
  </introduction>
  <section address="connecting_local">
    <title>Connecting to the Internet</title>
    <content>
      <para>If you want to connect a computer running Windows Server to the Internet, you’ll need to check your adapters and settings (including virtual network settings, if applicable). See the following sections for more information:</para>
      <list class="nobullet">
        <listItem>
          <para>
            <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#netadapter">Verify and repair network adapters</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#virtual">Review and verify virtual network settings</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#local_network">Review and verify local network settings</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#remote_network">Review remote network settings</link>
          </para>
        </listItem>
      </list>
    </content>
    <sections>
      <section address="netadapter">
        <title>Verify and repair network adapters</title>
        <content>
          <para>Verify that the computer has at least one network adapter installed and enabled. If the network connection is wired, verify that the network cable is connected and the network link is active. If there are problems with a network adapter, you can attempt to repair them manually, or you can use the network troubleshooter to automatically detect and repair basic configuration problems.</para>
          <para>Use the following procedure to verify the status of network adapters.</para>
          <procedure>
            <title>To verify the status of network adapters</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open a Windows PowerShell prompt, type <userInput>Get-NetAdapter</userInput>, and press ENTER. See the following example:</para>
                  <code>PS C:\&gt; Get-NetAdapter

Name                      InterfaceDescription                    ifIndex Status       MacAddress             LinkSpeed
----                      --------------------                    ------- ------       ----------             ---------
Ethernet 2                Microsoft Hyper-V Network Adapter #4         24 Disconnected 00-15-5D-9F-DF-06        10 Gbps
Ethernet                  Microsoft Hyper-V Network Adapter #3         20 Up           00-15-5D-9F-DF-05        10 Gbps</code>
                  <alert class="tip">
                    <list class="bullet">
                      <listItem>
                        <para>To display only network adapters that are not <ui>Up</ui>, type <userInput>Get-NetAdapter | ? Status –ne Up</userInput>. </para>
                      </listItem>
                      <listItem>
                        <para>To display a detailed list of network interface parameters for the <ui>Ethernet 2</ui> adapter, type <userInput>Get-NetAdapter –Name “Ethernet 2” | fl *</userInput>.</para>
                      </listItem>
                      <listItem>
                        <para>To see a list of network status related Windows PowerShell commands, type <userInput>Get-Command Get-Net*</userInput>. </para>
                      </listItem>
                      <listItem>
                        <para>To view the syntax for a command, use the <embeddedLabel>Get-Help</embeddedLabel> cmdlet, for example: <userInput>Get-Help Get-NetAdapterStatistics</userInput>.</para>
                      </listItem>
                    </list>
                  </alert>
                </content>
              </step>
              <step>
                <content>
                  <para>Verify that <ui>Up</ui> is displayed under <ui>Status</ui> for all network adapters that are currently in use.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>If the status of a network adapter is not <ui>Up</ui>, verify that the adapter is required to connect to the Internet and repair the connection. </para>
                  <para>The actions required to repair a network adapter depend on its status. For example, a status of <ui>Disconnected</ui> can indicate a problem with the network cable or another network device, such as a switch or hub. If the computer is a virtual machine, a <ui>Disconnected</ui> status can indicate a problem with the virtual network that is associated with a network adapter. More information is provided later in this topic to help you troubleshoot virtual networks.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Type <userInput>ncpa.cpl</userInput> at a command prompt, and press ENTER to open the <ui>Network Connections</ui> control panel.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click inside the <ui>Network Connections</ui> window, point to <ui>View</ui>, and click <ui>Details</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Review the <ui>Connectivity</ui> column for each network adapter. At least one adapter must display <ui>Internet access</ui> in this column for the computer to successfully connect to the Internet.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <para>
            <embeddedLabel>Use the network troubleshooter</embeddedLabel>
          </para>
          <para>If you cannot repair network adapters manually, you can use the network troubleshooter to attempt repairs. The network troubleshooter analyzes your network configuration and performs basic tests, including a default gateway test, DNS test, firewall test, and Internet connectivity test. The network troubleshooter also saves network diagnostic information that you can use later to review network settings.</para>
          <alert class="caution">
            <para>During the troubleshooting process, the network troubleshooter might reset some or all network connections on the local computer.</para>
          </alert>
          <para>Use the following procedure to run the network troubleshooter.</para>
          <procedure address="Tx">
            <title>To run the network troubleshooter</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Type <userInput>ncpa.cpl</userInput> at a command prompt, and press ENTER to open the <ui>Network Connections</ui> control panel.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click the network connection you want to repair, and click <ui>Diagnose</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>The network troubleshooter attempts to repair network problems automatically. If it is unable to repair the problem, it provides information about the type of problem found. Click <ui>View detailed information</ui>, and record the results that are listed under <ui>Windows Network Diagnostics</ui> and <ui>Issues found</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>To save detailed results from the network troubleshooter, click <ui>Detection details</ui>, and then under <ui>Other Networking Configuration and Logs</ui>, click <ui>NetworkConfiguration.cab</ui>. Right-click the <system>ipconfig.all.txt</system> file, click <ui>Copy</ui>, right-click the desktop, and then click <ui>Paste</ui>. Also copy and paste the <system>route.print.txt</system> file. </para>
                </content>
              </step>
            </steps>
            <conclusion>
              <content>
                <para>Information that you save from the network troubleshooter is helpful when you review local network settings, which is explained in the <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#local_network">Review and verify local network settings</link> section later in this topic.</para>
              </content>
            </conclusion>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="virtual">
    <title>Review and verify virtual network settings</title>
    <content>
      <para>Use the following procedures to verify virtual network settings. If the computer is not a virtual machine, you can skip this section.</para>
      <para>To connect a Hyper-V virtual machine to the Internet, the server running Hyper-V (also known as a host) must have a connection to the Internet, and Hyper-V must be configured with an external virtual switch that provides access to the host’s Internet connection. At least one network adapter on the virtual machine must be connected to this external virtual switch directly or through a virtual network. For more information about Hyper-V virtual switch functionality in Windows Server, see <externalLink><linkText>Hyper-V Virtual Switch Overview</linkText><linkUri>http://go.microsoft.com/fwlink/?linkid=306536</linkUri></externalLink> (http://go.microsoft.com/fwlink/?linkid=306536).</para>
      <para>The following procedures use Windows PowerShell to review virtual network settings on a virtual machine that is intended to connect to the Internet by using an external virtual switch that is configured on the Hyper-V host. To use these commands, the Hyper-V Module for Windows PowerShell must be installed. You can also use Hyper-V Manager to perform these procedures. For more information about configuring virtual networks with Hyper-V Manager, see <externalLink><linkText>Configure Virtual Networks</linkText><linkUri>http://go.microsoft.com/fwlink/?linkid=306679</linkUri></externalLink> (http://go.microsoft.com/fwlink/?linkid=306679).</para>
      <alert class="tip">
        <list class="nobullet">
          <listItem>
            <para>To see a list of Hyper-V status-related Windows PowerShell commands, type <userInput>Get-Command Get-VM*</userInput>. </para>
          </listItem>
          <listItem>
            <para>To see a list of all commands that are available in the Hyper-V module, type <userInput>Get-Command –Module Hyper-V</userInput>.</para>
          </listItem>
        </list>
      </alert>
      <procedure>
        <title>To verify virtual network settings</title>
        <steps class="ordered">
          <step>
            <content>
              <para>To verify that an external virtual switch is available on a virtual Hyper-V host, type <userInput>Get-VMSwitch –SwitchType External</userInput>, and press ENTER. See the following example:</para>
              <code>PS C:\&gt; Get-VMSwitch -SwitchType External

Name                                                           SwitchType NetAdapterInterfaceDescription
----                                                           ---------- ------------------------------
Intel(R) 82567LM-3 Gigabit Network Connection - Virtual Switch External   Intel(R) 82567LM-3 Gigabit Network Connection</code>
            </content>
          </step>
          <step>
            <content>
              <para>Verify that <ui>External</ui> is displayed under <ui>SwitchType</ui> for at least one virtual switch.</para>
            </content>
          </step>
          <step>
            <content>
              <para>To verify that a virtual machine is connected to ports on the external virtual switch shown in the previous step, type <userInput>Get-VMNetworkAdapter –VMName &lt;vmname&gt; | ft Name,SwitchName</userInput>, and press ENTER. See the following example:</para>
              <code>PS C:\&gt; Get-VMNetworkAdapter -VMName VM02.contoso.com | ft Name,SwitchName,IPAddresses -Autosize

Name            SwitchName                                                     IPAddresses
----            ----------                                                     -----------
Network Adapter Intel(R) 82567LM-3 Gigabit Network Connection - Virtual Switch {10.123.182.243, fe80::1106:7d3f:d7ac:d1f9, 2001:4898:2a:4:1106:7d3f:d7ac:d1f9}
Network Adapter Private network                                                {192.168.0.1, fe80::29c6:3513:2570:eeeb}</code>
            </content>
          </step>
          <step>
            <content>
              <para>Verify that the <ui>SwitchName</ui> that is displayed is the same as the <ui>Name</ui> of an external virtual switch displayed in the previous command output.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Virtual local area network (VLAN) settings can cause network connectivity issues. To display a list of virtual switch ports and associated VLANs, type <userInput>Get-VMNetworkAdapterVlan</userInput>, and press ENTER. See the following example:</para>
              <code>PS C:\&gt; Get-VMNetworkAdapterVlan

VMName                VMNetworkAdapterName                                           Mode     VlanList
------                --------------------                                           ----     --------
                      Internal network                                               Access   2
                      Intel(R) 82567LM-3 Gigabit Network Connection - Virtual Switch Untagged
VM01.contoso.com      Network Adapter                                                Trunk    10,1-100
VM02.contoso.com      Network Adapter                                                Untagged
VM02.contoso.com      Network Adapter                                                Access   200
VM03.contoso.com      Network Adapter                                                Isolated 10,200</code>
              <para>If a VLAN ID is associated with a Hyper-V host network adapter, or with virtual machines, it is displayed under <ui>VlanList</ui>. In this example, the first two network adapters are connected to the Hyper-V host and the next four network adapters are connected to the virtual machines that are displayed under <ui>VMName</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Verify that the external network adapter on the virtual machine that you want to connect to the Internet is using the same VLAN configuration as the external virtual switch on the host running Hyper-V. For example, if the external virtual switch on the Hyper-V host is untagged, the corresponding network adapter on a virtual machine must also be untagged. Or, if virtual switch ports are configured to use VLAN access mode, both ports must be tagged with the same VLAN ID.</para>
              <para>A virtual switch also provides support for VLAN trunk mode. In trunk mode, a virtual switch port receives traffic from all VLANs that you configure in an allowed VLAN list. In the following example, the virtual machine VM01.contoso.com is configured to send or receive traffic on any VLAN in the range 1-100. If there is no VLAN specified in the packet, the packet is treated as if it is from VLAN 10.</para>
              <code>Set-VMNetworkAdapterVlan –VMName VM01.contoso.com –Trunk –AllowedVlanIdList 1-100 –NativeVlanId 10</code>
              <para>A virtual machine and virtual switch might also be configured with port VLANs (PVLANs). PVLAN is a virtual switch property that enables the use of two VLAN IDs: a primary VLAN ID and a secondary VLAN ID. A PVLAN can be set in one of the following three modes:</para>
              <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>PVLAN Mode</para>
                    </TD>
                    <TD>
                      <para>Description</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>Isolated</para>
                    </TD>
                    <TD>
                      <para>Communicates only with promiscuous ports in the PVLAN</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Promiscuous</para>
                    </TD>
                    <TD>
                      <para>Communicates with all ports in the PVLAN</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Community</para>
                    </TD>
                    <TD>
                      <para>Communicates with ports in the same community and any promiscuous ports in the PVLAN</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
              <para>A PVLAN can be used to create an environment where virtual machines can interact only with the Internet and not have visibility into other virtual machine network traffic. To accomplish this, set the virtual switch ports on all virtual machines to the same PVLAN in isolated mode. In this configuration, all virtual machines are isolated from each other. In the following example, the PVLAN is set in isolated mode with a primary VLAN ID of 10 and a secondary VLAN ID of 200:</para>
              <code>Set-VMNetworkAdapterVlan –VMName VM03.contoso.com –Isolated –PrimaryVlanId 10 –SecondaryVlanId 200</code>
            </content>
          </step>
        </steps>
        <conclusion>
          <content>
            <para>In addition to VLANs and PVLANs, virtual switches can be configured with security policies and settings that can block access to the Internet. Hyper-V Network Virtualization enables you to deploy virtual networks with the same capabilities (and security policies) as a physical network. If a virtual machine is located on a virtual network, review all virtual network settings in the same way that you would review local network settings for a physical host. See information later in this topic for help reviewing local network settings. For more information, see <externalLink><linkText>Hyper-V Network Virtualization Overview</linkText><linkUri>http://go.microsoft.com/fwlink/?linkid=306685</linkUri></externalLink> (http://go.microsoft.com/fwlink/?linkid=306685).</para>
          </content>
        </conclusion>
      </procedure>
    </content>
  </section>
  <section address="local_network">
    <title>Review and verify local network settings</title>
    <content>
      <para>Next, verify and record the local network settings that you are using. These settings determine connectivity to the local area network (LAN), and they provide the local computer with the ability to resolve Domain Name System (DNS) names and to communicate with other computers and networks. If you are not sure these settings are correct, contact your network administrator.</para>
      <para>If the computer that you want to connect to the Internet is a virtual machine, see <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#virtual">Review and verify virtual network settings</link> before you perform these procedures.</para>
      <procedure>
        <title>To review local network settings</title>
        <steps class="ordered">
          <step>
            <content>
              <para>If you saved files from the network troubleshooter in the <link xlink:href="99bd7ac1-9beb-438d-900e-426da41898b8#netadapter">Verify and repair network adapters</link> section of this topic, open the <system>ipconfig.all.txt</system> file to review local network settings.</para>
            </content>
          </step>
          <step>
            <content>
              <para>If you did not run the network troubleshooter or you did not save files from the network troubleshooter, open a command prompt, type <userInput>ipconfig /all</userInput>, and press ENTER.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Review and record the following settings for all network adapters:</para>
              <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>Setting</para>
                    </TD>
                    <TD>
                      <para>Description</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>DHCP enabled</para>
                    </TD>
                    <TD>
                      <para>Dynamic Host Configuration Protocol (DHCP) is enabled by default to dynamically configure network settings. If there are no DHCP servers available, or if installed roles or services require a static IP address, you must manually provide network settings.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>IPv6 address</para>
                    </TD>
                    <TD>
                      <para>DHCP can provide a dynamic IPv6 address, or you can configure a static IPv6 address. By default, the computer will use a link-local IPv6 address if an IPv6 address is not provided by DHCP or is statically configured. A link-local IPv6 address is not sufficient to connect to the Internet.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>IPv4 address</para>
                    </TD>
                    <TD>
                      <para>DHCP can provide a dynamic IPv4 address or you can configure a static IPv4 address. By default, the computer will use Automatic Private IP Addressing (APIPA) if an IPv4 address is not provided by DHCP or is statically configured. An IP address assigned by APIPA will be in the private IP address range of 169.254.0.1 – 169.254.255.254. An IP address assigned by APIPA is not sufficient to connect to the Internet.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Subnet mask</para>
                    </TD>
                    <TD>
                      <para>DHCP can provide a subnet mask or you can configure a subnet mask manually. The subnet mask determines which IP addresses the computer can connect to directly, without the use of routing. A computer uses routing to connect to IP addresses on different subnets, such as IP addresses on the Internet. </para>
                      <para>If you saved files from the network troubleshooter in the previous procedure, all routes that are currently configured on the local computer are recorded in the <system>route.print.txt</system> file. Destinations that are on the same subnet (determined by the subnet mask) will display as <ui>On-link</ui> under <ui>Gateway</ui>. If you did not run the network troubleshooter, or you did not save files from the network troubleshooter, you can display this information by typing <userInput>route print</userInput> at a command prompt and then pressing ENTER. You can also use the Windows PowerShell cmdlet <embeddedLabel>Get-NetRoute</embeddedLabel>.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Default gateway</para>
                    </TD>
                    <TD>
                      <para>DHCP can provide the default gateway or you can configure a default gateway manually. The default gateway is an IP address on the local subnet where a computer sends network traffic by default. A computer will send traffic to the default gateway if it does not have a static route to the destination IP address. Typically, the default gateway is the IP address that the computer uses to send network traffic off the local network and to other networks, such as the Internet. </para>
                      <para>If the computer is not configured with a default gateway, or if it is configured with an incorrect default gateway address, the computer might be unable to connect to other networks, such as the Internet.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>DHCP server</para>
                    </TD>
                    <TD>
                      <para>If the computer is configured to use DHCP and it has successfully acquired an IP address configuration from a DHCP server, the IP address of the DHCP server will be displayed.</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>DNS servers</para>
                    </TD>
                    <TD>
                      <para>DHCP can provide a list of IP addresses for one or more DNS servers or you can configure the DNS server list manually. The computer uses DNS servers to translate host names to IP addresses and vice-versa. At least one DNS server is required to provide DNS name resolution. Additional DNS servers are listed in case the primary DNS server does not respond. To use a DNS server, the computer must be able to connect to the DNS server using the local subnet or by routing through the network.</para>
                      <para>If multiple DNS servers are assigned to a computer, the computer will use the first DNS server that is configured on its network adapter. If the computer has more than one network adapter, the first DNS server configured on the preferred network adapter is used. The preferred network adapter is the adapter that is highest in the binding order.</para>
                      <para>To successfully connect to the Internet, a computer must have a network connection to its assigned DNS server, and that DNS server must be able to provide Internet name resolution by using forwarding or root hints. A computer will not use other DNS servers if the assigned DNS server responds to a query, even if that response is that it failed to resolve a name.</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </content>
          </step>
        </steps>
        <conclusion>
          <content>
            <para>If network settings are not provided by DHCP, you must provide these settings manually.</para>
            <para>Whether settings are provided manually or by DHCP, verify that these settings are correct for the local subnet.</para>
          </content>
        </conclusion>
      </procedure>
    </content>
    <sections>
      <section>
        <title>Verifying local network settings</title>
        <content>
          <para>Following are some useful commands that you can use to test local network settings.</para>
          <para>
            <embeddedLabel>Windows PowerShell commands</embeddedLabel>
          </para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Command</para>
                </TD>
                <TD>
                  <para>Description</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Test-Connection</para>
                </TD>
                <TD>
                  <para>Sends Internet Control Message Protocol (ICMP) echo request packets to one or more computers.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Resolve-DnsName</para>
                </TD>
                <TD>
                  <para>Performs a DNS name query resolution for a specified name.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Test-DnsServer</para>
                </TD>
                <TD>
                  <para>Tests that a specified computer is a functioning DNS server.</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>
            <br />
          </para>
          <para>
            <embeddedLabel>Windows commands</embeddedLabel>
          </para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Command</para>
                </TD>
                <TD>
                  <para>Description</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Ping</para>
                </TD>
                <TD>
                  <para>Sends an ICMP echo request to a destination IP address.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Tracert</para>
                </TD>
                <TD>
                  <para>Displays a list of router interfaces that exist between a source host and a destination.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Pathping</para>
                </TD>
                <TD>
                  <para>Sends ICMP packets to each router on the way to a destination and displays results of the packets returned from each hop.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>NSlookup</para>
                </TD>
                <TD>
                  <para>Displays information that you can use to diagnose the DNS infrastructure.</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>
            <br />
          </para>
          <alert class="note">
            <para>The commands that are used to test connections (<embeddedLabel>Test-Connection</embeddedLabel>, <embeddedLabel>ping</embeddedLabel>, <embeddedLabel>tracert</embeddedLabel>, and <embeddedLabel>pathping</embeddedLabel>) will be blocked if the destination computer or device is configured to deny ICMP echo requests.</para>
          </alert>
          <procedure>
            <title>To verify local network settings</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>When you test network connectivity to the local computer and other computers and devices, begin by verifying that the local computer is responding. Next, test network connectivity to computers and devices on a path from the local computer out to the Internet. </para>
                  <para>Network settings can be verified by testing connectivity to the following devices:</para>
                  <list class="nobullet">
                    <listItem>
                      <para>The loopback address (127.0.0.1)</para>
                    </listItem>
                    <listItem>
                      <para>An IP address assigned to the network adapter that you want to connect to the Internet</para>
                    </listItem>
                    <listItem>
                      <para>The IP address for the default gateway </para>
                    </listItem>
                    <listItem>
                      <para>The IP address for the default DNS server</para>
                    </listItem>
                    <listItem>
                      <para>An IP address on the Internet</para>
                    </listItem>
                    <listItem>
                      <para>A DNS name on the Internet</para>
                    </listItem>
                  </list>
                  <para>
                    <br />
                  </para>
                  <para>You can use the <embeddedLabel>ping</embeddedLabel> command or the <embeddedLabel>Test-Connection</embeddedLabel> Windows PowerShell cmdlet to test connectivity. In the following example, 157.54.10.29 is the preferred DNS server for the host VM02.</para>
                  <code>PS C:\&gt; Test-Connection 157.54.10.29

Source        Destination     IPV4Address      IPV6Address                              Bytes    Time(ms)
------        -----------     -----------      -----------                              -----    --------
VM02           157.54.10.29    157.54.10.29     2001:4898:c8:600b:3968:4760:1905:30e1    32       1
VM02           157.54.10.29    157.54.10.29     2001:4898:c8:600b:3968:4760:1905:30e1    32       1
VM02           157.54.10.29    157.54.10.29     2001:4898:c8:600b:3968:4760:1905:30e1    32       1
VM02           157.54.10.29    157.54.10.29     2001:4898:c8:600b:3968:4760:1905:30e1    32       1</code>
                  <para>Remember that these commands can be blocked if the computer or device is configured to deny ICMP echo requests. Devices on the Internet are frequently configured to block ICMP.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Test routing to a remote host. In the following example, the <embeddedLabel>tracert</embeddedLabel> command is used without resolving the host names, and the number of hops is limited to 12. The first hop in this list is the default gateway. ICMP is blocked starting at hop #9.</para>
                  <code>C:\&gt; Tracert -d -h 12 microsoft.com

Tracing route to microsoft.com [64.4.11.37]
over a maximum of 12 hops:

  1    &lt;1 ms    &lt;1 ms    &lt;1 ms  10.123.182.1
  2     1 ms     1 ms    &lt;1 ms  10.37.2.182
  3     1 ms     1 ms     1 ms  10.37.67.61
  4    &lt;1 ms    &lt;1 ms    &lt;1 ms  10.37.44.102
  5    &lt;1 ms    &lt;1 ms     1 ms  10.37.67.222
  6     1 ms     1 ms     1 ms  10.37.45.77
  7     1 ms     1 ms    &lt;1 ms  131.107.202.166
  8     2 ms     2 ms     2 ms  131.107.200.74
  9     *        *        *     Request timed out.
 10     *        *        *     Request timed out.
 11     *        *        *     Request timed out.
 12     *        *        *     Request timed out.

Trace complete.</code>
                  <para>Verify that the computer is able to send traffic off the local network.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Test the default DNS server to verify that it is functional. See the following example.</para>
                  <code>PS C:\&gt; Test-DnsServer -IPAddress 157.54.10.29

IPAddress                               Result                                  RoundTripTime                           TcpTried
---------                               ------                                  -------------                           --------
157.54.10.29                            Success                                 00:00:00                                False</code>
                  <para>Verify that <ui>Success</ui> is displayed under <ui>Result</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Test DNS resolution for a name on the Internet. See the following example.</para>
                  <code>PS C:\&gt; Resolve-DnsName microsoft.com

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
microsoft.com                                  A      710   Answer     64.4.11.37
microsoft.com                                  A      710   Answer     65.55.58.201</code>
                  <para>Verify that no errors are displayed.</para>
                </content>
              </step>
            </steps>
            <conclusion>
              <content>
                <para>If one or more of these commands fails, verify that the network settings are correct and use this information to repair the problem. If the local network settings are correct and you are unable to repair the problem, review the remote network settings.</para>
              </content>
            </conclusion>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="remote_network">
    <title>Review remote network settings</title>
    <content>
      <para>Nearly every network today implements policies and protocols to control access to and from the Internet. These remote network settings are in place to protect the local computer, but they can also prevent Internet access. If you are having trouble connecting to the Internet after you have verified the network adapter status and the local or virtual network settings, contact your network administrator to review the settings and verify that the remote network settings are not preventing you from connecting to the Internet.</para>
      <para>Examples of network security and isolation methods that can block Internet access include firewalls, MAC address filters, IP access control lists (ACLs), proxy servers, IP security (IPsec) policies, VLANs, Virtual Extensible LANs (VXLAN), and Network Virtualization for Generic Routing Encapsulation (NVGRE). For example, the local computer can be configured with a correct default gateway, IP address, and subnet mask, but the network troubleshooter reports that the default gateway is not available. This might be due to a network security or isolation policy applied to the local computer. These policies are common in some network environments, such as data centers.</para>
      <para>If one or more network security policies or settings are preventing the local computer from connecting to the Internet, a network administrator must enable this access. You cannot configure remote network settings on the local computer.</para>
      <para>Other remote network problems that can disrupt Internet access include the failure of network infrastructure services, devices, and connections. To determine if the issue is isolated to the local computer, you can attempt a connection to the Internet by using another computer that is located on the same subnet or on an adjacent subnet. If another computer is also affected, it is likely that the issue is not caused by settings on the local computer.</para>
    </content>
  </section>
  <section>
    <title>Related resources</title>
    <content>
      <para>
        <link xlink:href="06e1cb7b-19c9-4c49-9db8-a941f6f593c3">Microsoft Management Console 3.0</link>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

