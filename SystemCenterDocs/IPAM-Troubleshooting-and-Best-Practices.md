---
title: IPAM Troubleshooting and Best Practices
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3288f3a8-3b3a-4baa-a9b0-41c8d58d6131
---
# IPAM Troubleshooting and Best Practices
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic provides general troubleshooting guidance for IPAM server. For more information, see <externalLink><linkText>Troubleshooting and Best Practices</linkText><linkUri>http://go.microsoft.com/fwlink/p/?linkid=244445</linkUri></externalLink> in the Windows Server Technical Library.</para>
  </introduction>
  <section>
    <title>Troubleshooting tools</title>
    <content>
      <para>IPAM event logs are available in Event Viewer using the following path: Application and Services Logs &gt; Microsoft &gt; Windows &gt; IPAM. The following log channels are available:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Admin</embeddedLabel>: This channel captures events that are related to IPAM user actions and IPAM periodic tasks.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>ConfigurationChange</embeddedLabel>: This channel captures events that are related to configuration changes made to the IPAM server.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Operational</embeddedLabel>: This channel captures informational events that are related to IPAM periodic tasks. Event logging on this channel is disabled by default.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Analytic and Debug</embeddedLabel>: These channels are hidden and disabled by default. Use these channels for debugging purposes. To show them, click <ui>View</ui> and then click <ui>Show Analytic and Debug Logs</ui>.</para>
        </listItem>
      </list>
      <para>Events in the Admin and Operational channels can also be viewed from the IPAM tile in the Server Manager Dashboard.</para>
    </content>
  </section>
  <section>
    <title>Common problems and solutions</title>
    <content>
      <para>The following section lists common problems and solutions for IPAM.</para>
    </content>
    <sections>
      <section>
        <title>Connecting to the IPAM server</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Problem: You are not able to connect to the IPAM server.</para>
            </listItem>
            <listItem>
              <para>Solution: View the <ui>Description</ui> field on Task Manager’s <ui>Services</ui> tab, and verify that the following services are running on the IPAM server:</para>
              <list class="bullet">
                <listItem>
                  <para>Windows Process Activation Service</para>
                </listItem>
                <listItem>
                  <para>Windows Internal Database</para>
                </listItem>
              </list>
              <para>If they are not running, start these services. Also verify that you are a signed in as a domain user and that you are a member of either the local Administrators security group on the IPAM server, or a member of the appropriate IPAM security group on the IPAM server.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Server access</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Problem: The access status of a managed server does not change to Unblocked after completing IPAM provisioning.</para>
            </listItem>
            <listItem>
              <para>Solution: Review the details pane in Server Inventory view to identify the types of access status that are blocked. If you are using the manual IPAM provisioning method, verify that the access settings that correspond to this status are enabled. For Group Policy-based provisioning, verify that the required GPOs have been created and linked, and that the managed server is a member of the security filter list of appropriate GPOs. This issue can also occur if Group Policy has not been updated on the target servers. Open an elevated command prompt on the managed server and type <userInput>gpupdate /force</userInput> to force the application of Group Policy. </para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to add a managed server to an IPAM GPO.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that you are signed in as a member of the Domain Admins security group, or higher, or that you have been delegated privileges to edit the GPO. GPO delegation for users or groups can be enabled from the IPAM <system>Invoke-IpamGpoProvisioning</system> cmdlet at the time the GPO is created, or from the Group Policy Management Console if the GPO is already created.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Server discovery</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to configure server discovery.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that you are signed in as a domain user and not as a local user on the IPAM server.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: A DNS server is not discovered.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that the DNS server configured on the IPAM server’s network interface can query name server (NS) records for the domain zone, and that an NS record exists for the DNS server. All NS records for the domain zone and NS records for allowed DNS suffixes are queried during the DNS server discovery operation.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: A DHCP server is not discovered.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that the DHCP server role is not installed on the IPAM server. Verify that at least one IPv4 scope is configured on a DHCP server, and that the IPAM server has a TCP/IP connection to the DHCP server. Also verify that DHCP INFORM request messages sent by IPAM server are not filtered on the network.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to manually add a server to IPAM.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify DNS resolution of the IP address of the server. Also verify that the server name is present in the Active Directory Global Catalog.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>IP address space management</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to find an available IP address from a Microsoft DHCP-managed IP address range.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that DHCP RPC firewall ports are enabled on the target DHCP server, and that your user account is a member of the DHCP Users group on the DHCP server.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to import a comma-separated value file with IP address records into IPAM.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that all the header field names in the file match the existing built-in and custom field names in IPAM. Create new custom field names in IPAM if required.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: Importing records from a comma-separated value file is successful, but some of the records are not displayed in IPAM.</para>
            </listItem>
            <listItem>
              <para>Solution: Review the error log for the import operation. By default, this log is created in the Documents folder, and it contains details of any records that failed to import. Use the error information provided to fix each failed record instance, and then repeat the import operation.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to select DHCP servers or DNS zones in the IP address add or edit dialog box.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that the DHCP and DNS servers that are hosting the scope or zone are managed by IPAM. Also verify that you have administrative privileges on the target DHCP or DNS server.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Monitoring and management</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Problem: A managed server availability state is not reachable.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify TCP/IP connectivity between the IPAM server and the target server. Verify that the DNS Server service or DHCP Server service is running on the target server, and that the IPAM server has been successfully provisioned with Read access on the service ACLs. Also verify that remote service management ports are open on the target server.</para>
            </listItem>
          </list>
          <list class="bullet">
            <listItem>
              <para>Problem: You are unable to make configuration changes on a DHCP server or scope.</para>
            </listItem>
            <listItem>
              <para>Solution: Verify that DHCP RPC firewall ports are enabled on the target DHCP server, and that you are signed in with an account that has DHCP Administrators privileges on the target DHCP server.</para>
            </listItem>
          </list>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>Best practices</title>
    <content>
      <para>The following are some best practices for deploying and operating IPAM.</para>
    </content>
    <sections>
      <section>
        <title>General</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>The IPAM server should be installed as a standalone feature. For optimal performance, do not locate IPAM with other server roles or features.</para>
            </listItem>
            <listItem>
              <para>The recommended hardware configuration for an IPAM server is: A dual-core 2 GHz CPU, RAM in excess of 4 GB, and disk space of 120 GB or greater.</para>
            </listItem>
            <listItem>
              <para>IPAM users and administrators must be added to the appropriate IPAM security groups based on their roles and administrative privileges.</para>
            </listItem>
            <listItem>
              <para>User-defined custom fields that are required to be used for a logical grouping must be added as multivalue fields.</para>
            </listItem>
            <listItem>
              <para>Refresh the IPAM user interface periodically to ensure that the view is up-to-date with any changes in the database. Changes can occur due to periodic data collection tasks and concurrent user sessions.</para>
            </listItem>
            <listItem>
              <para>Leverage advanced features like logical grouping, saving and loading filter queries, group by, and viewing customizations to visualize and track entities and fields of interest.</para>
            </listItem>
            <listItem>
              <para>The IPAM database should be backed up periodically using Windows Server Backup.</para>
            </listItem>
            <listItem>
              <para>Tasks that require a long time to complete, and operations such as database purging, should be scheduled during nonbusiness hours when the load on the network is low.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Provisioning</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>The Group Policy-based provisioning method is recommended over the manual provisioning method due to the number of security settings that need to be enabled for each server role that is managed by IPAM. Using Group Policy also ensures that settings are regularly updated.</para>
            </listItem>
            <listItem>
              <para>A domain-wide group named <system>IpamGpoAdmins</system> should be created, and IPAM GPO administration should be delegated to this group at the time of GPO creation. Any user who needs to mark servers as managed or unmanaged can be added to this group.</para>
            </listItem>
            <listItem>
              <para>Ensure that there are no conflicting Group Policies in your environment for the settings that are required by IPAM. IPAM access can be disabled if a firewall port that is required by IPAM is blocked by another Group Policy, or if membership in a security group that is required by IPAM is overwritten.</para>
            </listItem>
            <listItem>
              <para>When multiple servers are being selected for management, such as during initial IPAM provisioning, select all servers simultaneously to set their manageability status. This ensures that incremental edits to IPAM GPOs are minimal.</para>
            </listItem>
            <listItem>
              <para>For large deployments, linking the GPO to the root of the domain may not be ideal. Administrators should use organizational units to deploy Group Policy for infrastructure servers.</para>
            </listItem>
            <listItem>
              <para>Rollback of IPAM access settings is recommended from the servers that are being marked as unmanaged. However, updating the domain-wide DNS ACL will enable DNS RPC access for the IPAM server on all domain controllers that are co-located with DNS servers in the domain. This setting is not updated on a per-server basis.</para>
            </listItem>
            <listItem>
              <para>For standalone DNS servers that are not co-located on domain controller, the computer for the IPAM server must be added to the local Administrators group because the domain-wide DNS ACL will not be applicable on these servers.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Discovery</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Do not install the IPAM feature on a server that is running the on a DHCP Server role service because it affects IPAM’s discovery of DHCP servers in the network.</para>
            </listItem>
            <listItem>
              <para>Do not add servers individually (for roles other than NPS), to avoid having to manually maintain the server inventory. Leverage the automated discovery mechanism as much as possible.</para>
            </listItem>
            <listItem>
              <para>Avoid keeping the server manageability status as Unspecified except when the server is temporarily out of service. Ideally the server should be marked as Managed or Unmanaged.</para>
            </listItem>
            <listItem>
              <para>If only a subset of the roles that are discovered on a physical server need to be managed, make sure that only the roles that are actively managed are selected on the server. Other roles should be cleared. IPAM periodic data collection tasks will collect data from all roles that are selected.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>IP address management</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Configure utilization thresholds appropriately to select the most effective checkpoints to identify under and over utilized address space.</para>
            </listItem>
            <listItem>
              <para>Over utilization threshold crossing events that are logged by IPAM should be monitored for timely detection of potential address space exhaustion.</para>
            </listItem>
            <listItem>
              <para>Overutilized and underutilized address space must be identified and effectively redistributed to achieve optimal utilization across the entire address space. Utilization trends can be used as effective tools to predict the short and long term address space requirements.</para>
            </listItem>
            <listItem>
              <para>If exclusion ranges are being used within DHCP scopes to make static allocations or reservations, then IPAM recommends explicitly creating a static IP address range that corresponds to the exclusion range to track the utilization statistics for the entire subnet.</para>
            </listItem>
            <listItem>
              <para>For a homogenous and consistent rollout of address space allocations, arrange IPv4 address ranges in size units of between /22 and /24 and IPv6 ranges of /64. Use IPv4 address blocks of size /16, and IPv6 address blocks of /48.</para>
            </listItem>
            <listItem>
              <para>Create static IP addresses with a finite expiry date to ensure that stale addresses can be reclaimed from address ranges at the correct intervals. When an IP address transitions to the expiry due state, administrators must try to ensure that the address is alive in the network and extend the address life or reclaim the address.</para>
            </listItem>
            <listItem>
              <para>Leverage IPAM’s overlap and duplicate detection feature to identify and track intentional and unintentional IP address ranges on your network.</para>
            </listItem>
            <listItem>
              <para>If you have multiple instances of overlapping address space configured in your environment, then using logical groups will be more effective to track overall utilization. Address blocks only map one overlapping range for utilization roll-up.</para>
            </listItem>
            <listItem>
              <para>For tracking IP address leases in the network, the IP address tracking feature in the Event Catalog view can be more efficient than pulling all dynamic DHCP lease records into IPAM.</para>
            </listItem>
            <listItem>
              <para>Leverage IPAM’s Find an Available IP Address feature with in-line DHCP reservation and DNS record updates to simplify static IP address allocations.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Monitor and manage</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Create and save queries to quickly identify services and zones that are not in a healthy state.</para>
            </listItem>
            <listItem>
              <para>Leverage advanced constructs in multiedit scenarios to add, overwrite, delete, or find-and-replace to cater to the exact scenario requirement when you edit options across multiple DHCP scopes and servers.</para>
            </listItem>
            <listItem>
              <para>Leverage advanced constructs in multiedit scenarios to add, overwrite, or delete to cater to the exact scenario requirement when you configure vendor and user classes across multiple DHCP servers.</para>
            </listItem>
            <listItem>
              <para>Use the duplicate scope functionality to create new scopes with similar settings. The typical scenarios where this can be leveraged are migrating scopes from one server to another and configuring split scopes.</para>
            </listItem>
            <listItem>
              <para>Use the overall forward lookup zone view to identify potential issues and to identify servers that might have a problem. Isolate whether the issue is due to a zone event or server availability state.</para>
            </listItem>
            <listItem>
              <para>Monitor DHCP scope utilization percentage and utilization status to identify overutilized and underutilized scopes. Take necessary actions to align scope utilization to an optimal state, keeping utilization trend history in mind.</para>
            </listItem>
            <listItem>
              <para>For settings that are not supported by IPAM, launch the DHCP or DNS MMC from within the IPAM console to complete the configuration scenario.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Event catalog</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>For best performance and disk space management, an IPAM event catalog data purge should be performed periodically, to maintain a six-month old database.</para>
            </listItem>
            <listItem>
              <para>Auditing of account logon events should be enabled on domain controllers and NPS servers, and the security event log size should be large enough to allow the periodic audit task to complete data collection before it is rolled over.</para>
            </listItem>
            <listItem>
              <para>The DHCP audit log file size must be large enough to hold the audit events for one day, to ensure that no lease events are lost because of size overruns.</para>
            </listItem>
            <listItem>
              <para>The audit log file location for both DHCP IPv4 and IPv6 leases must be configured in a common folder. The IPAM audit task selects the log files from one network share per server.</para>
            </listItem>
            <listItem>
              <para>The time period that is selected for a query should be optimal. Typically, a query interval between 3 days to 15 days is optimal.</para>
            </listItem>
          </list>
        </content>
      </section>
    </sections>
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

