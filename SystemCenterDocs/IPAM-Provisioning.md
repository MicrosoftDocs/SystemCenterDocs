---
title: IPAM Provisioning
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24c903c7-37e6-452b-bb3a-72265d932870
---
# IPAM Provisioning
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic provides a summary of IPAM provisioning methods. For more information, see <externalLink><linkText>Choose an IPAM Provisioning Method</linkText><linkUri>http://go.microsoft.com/fwlink/p/?linkid=244438</linkUri></externalLink> in the Windows Server Technical Library.</para>
  </introduction>
  <section>
    <title>What is IPAM provisioning?</title>
    <content>
      <para>To be managed by IPAM, group memberships, file shares, service access settings, and firewall ports on domain controllers, NPS, DNS, and DHCP servers must be configured to allow the IPAM server access to perform required monitoring and configuration functions. Application of these settings to managed servers is referred to as IPAM provisioning.</para>
      <para>When access settings are configured on managed servers, the IPAM server periodically collects configuration and monitoring information by using Windows remote management protocols. The IPAM server collects information by using data collection tasks that run periodically and can be viewed in Task Manager. These periodic data collection tasks run on the IPAM server under the Network Service account, which in turn uses the IPAM server computer account credentials for remote communication. </para>
      <para>The following table describes the settings that are required on managed servers to enable IPAM access.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Managed Server Role</para>
            </TD>
            <TD>
              <para>IPAM Access Status</para>
            </TD>
            <TD>
              <para>Access Settings</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>DHCP</para>
            </TD>
            <TD>
              <para>DHCP RPC</para>
            </TD>
            <TD>
              <para>The computer account for the IPAM server must be a member of the DHCP Users security group.</para>
              <para>The following firewall rules must be enabled:</para>
              <list class="bullet">
                <listItem>
                  <para>DHCP Server (RPC-In)</para>
                </listItem>
                <listItem>
                  <para>DHCP Server (RPCSS-In)</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>DHCP</para>
            </TD>
            <TD>
              <para>DHCP audit share</para>
            </TD>
            <TD>
              <para>A network file share named <system>Dhcpaudit</system> must be created using the DHCP audit file folder, with Read access enabled for the computer account of the IPAM server.</para>
              <para>The following firewall rules must be enabled:</para>
              <list class="bullet">
                <listItem>
                  <para>File and Printer Sharing (NB-Session-In)</para>
                </listItem>
                <listItem>
                  <para>File and Printer Sharing (SMB-In)</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>DNS</para>
            </TD>
            <TD>
              <para>DNS RPC</para>
            </TD>
            <TD>
              <para>Read access for the computer account of the IPAM server must be added to DNS discretionary access control list (DACL).</para>
              <para>The following firewall rules must be enabled:</para>
              <list class="bullet">
                <listItem>
                  <para>DNS Service RPC</para>
                </listItem>
                <listItem>
                  <para>DNS Service RPC Endpoint Mapper</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>DHCP, DNS, domain controller, NPS</para>
            </TD>
            <TD>
              <para>Event log</para>
            </TD>
            <TD>
              <para>The computer account of the IPAM server must be a member of the Event Log Readers security group.</para>
              <para>The computer account for the IPAM server must be granted read access in the ACL that is maintained by the following registry key on the DNS server: MACHINE\System\CurrentControlSet\Services\Eventlog\DNS Server\CustomSD. This only required on DNS servers.</para>
              <para>The following firewall rules must be enabled:</para>
              <list class="bullet">
                <listItem>
                  <para>Remote Event Log Management (RPC)</para>
                </listItem>
                <listItem>
                  <para>Remote Event Log Management (RPC-EPMAP)</para>
                </listItem>
              </list>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>In addition to service management and event monitoring, IPAM performs service status monitoring for DNS and DHCP servers. To enable this service monitoring functionality, the computer account of the IPAM server must be granted read access to the DHCP Server service (for DHCP service monitoring) and to the DNS Server service (for DNS service monitoring). This access is controlled by the Windows service ACL and requires that the following firewall rules are enabled on target servers:</para>
      <list class="bullet">
        <listItem>
          <para>Remote Service Management (RPC)</para>
        </listItem>
        <listItem>
          <para>Remote Service Management (RPC-EPMAP)</para>
        </listItem>
      </list>
      <para>Service access status for DHCP and DNS servers can be viewed in the Server Availability column from the DHCP and DNS Servers view.</para>
    </content>
  </section>
  <section>
    <title>Provisioning methods</title>
    <content>
      <para>Before you can begin using IPAM, you must choose a method to provision access settings on managed servers. The following IPAM provisioning methods are available:</para>
      <list class="nobullet">
        <listItem>
          <para>
            <embeddedLabel>Manual</embeddedLabel>: If you choose the manual method, security group membership, firewall rules, file shares, and service access settings must be configured individually on each managed server. Settings must also be removed manually if the server becomes unmanaged. This method is typically used when the number of managed servers is small.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Group Policy-based</embeddedLabel>: If you choose the Group Policy-based method, IPAM automatically adds managed servers to the appropriate Group Policy Object (GPO) when a server is marked as managed. If the server is marked as unmanaged it is removed from GPO security filtering. However, settings must be removed manually if you change a server from a managed status to unmanaged status. You must provide a Group Policy Object (GPO) prefix in the IPAM provisioning wizard, and the following GPOs must be created in the domains that contain managed servers:</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>&lt;GPO-prefix&gt;_DHCP</embeddedLabel>: This GPO is used to apply policies and settings to allow IPAM to monitor, manage, and collect information from managed DHCP servers on the network. In addition to monitoring functions, several DHCP server and scope properties can be configured using IPAM.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>&lt;GPO-prefix&gt;_DNS</embeddedLabel>: This GPO is used to apply policies and settings to allow IPAM to monitor and collect information from managed DNS servers on the network. Zone status monitoring and a limited set of configuration functions are available for DNS servers.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>&lt;GPO-prefix&gt;_DC_NPS</embeddedLabel>: This GPO is used to apply policies and settings to allow IPAM to collect information from managed domain controllers and network policy servers (NPS) on the network for IP address tracking purposes.</para>
            </listItem>
          </list>
        </listItem>
      </list>
      <alert class="important">
        <para>The managed server provisioning method cannot be changed after you complete the IPAM provisioning wizard.</para>
      </alert>
      <para>If you use the Group Policy-based method, GPOs must be created in the domains that will be managed by IPAM. To configure these GPOs, use the <system>Invoke-IpamGpoProvisioning</system> Windows PowerShell cmdlet. To use the manual provisioning method, you must configure individual security group membership, firewall rules, file shares, and service access settings locally on each managed server.</para>
      <para>When you configure IPAM access settings on managed servers, the IPAM server communicates with these servers using Windows remote management connections. These are required for server management functions and periodic data collection tasks that run on the IPAM server.</para>
      <para>The following are typical steps that are used to initially configure IPAM using the Group Policy-based provisioning method:</para>
      <list class="ordered">
        <listItem>
          <para>Complete the IPAM provisioning wizard, and select the Group Policy-based provisioning method. Provide a GPO prefix that is unique to each IPAM server instance. GPOs are NOT created in this step.</para>
        </listItem>
        <listItem>
          <para>Configure server discovery by selecting the domains that contain infrastructure servers you want to manage and monitor with IPAM.</para>
        </listItem>
        <listItem>
          <para>Create IPAM GPOs in each of the chosen domains by using the Windows PowerShell <system>Invoke-IpamGpoProvisioning</system> cmdlet. Membership in the Domain Admins group, or higher, is required to run this cmdlet. You can delegate subsequent IPAM GPO administration tasks to specified users or groups that are not domain administrators.</para>
        </listItem>
        <listItem>
          <para>After you complete the server discovery task, select the servers to manage by setting their manageability status to Managed or Unmanaged. Credentials for the user that is signed in to the IPAM server are used to add these servers to the GPO filter list. The IPAM administrator who performs this operation must be a member of the Domain Admins or Enterprise Admins security group, or a delegated administrator.</para>
        </listItem>
        <listItem>
          <para>Wait for Group Policy update to apply the settings on the managed servers. Refresh the server access status to ensure that all the required IPAM access settings are allowed on managed servers.</para>
        </listItem>
        <listItem>
          <para>When IPAM access is verified, you can retrieve data from the managed servers.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section>
    <title>Common management actions</title>
    <content>
      <para>IPAM provides the following noncontextual actions from the Manage menu in the Server Manager console:</para>
      <list class="nobullet">
        <listItem>
          <para>
            <embeddedLabel>Connect to IPAM Server</embeddedLabel>: Enables you to select an IPAM server from the list of IPAM servers that are managed by the current instance of Server Manager.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>IPAM Settings</embeddedLabel>: Provides the following configuration options:</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Configure Server Discovery</embeddedLabel>: Select domains in the Active Directory forest to run automatic server discovery for DHCP servers, DNS servers, and domain controllers.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Configure Custom Fields</embeddedLabel>: Create new custom fields and values or extend existing custom fields.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Configure Utilization Threshold</embeddedLabel>: Specify overutilization and underutilization threshold percentages to categorize the utilization status of IP address ranges, IP address blocks, and IP range groups as Over, Under, or Optimal.</para>
            </listItem>
          </list>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Start Discovery</embeddedLabel>: Trigger the ServerDiscovery task on demand to refresh server information.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Retrieve All Server Data</embeddedLabel>: Trigger all data collection tasks on demand to refresh information.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <para>
        <legacyLink xlink:href="9035778c-7ab3-42d0-8540-45a163c1d46b">IP Address Management Overview</legacyLink>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

