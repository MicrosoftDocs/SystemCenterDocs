---
title: Next steps for completing your AD FS installation
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c66c7f4b-6b8f-4e44-8331-63fa85f858c2
---
# Next steps for completing your AD FS installation
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic covers additional steps to configure AD FS after you install the first federation server, including:</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="c66c7f4b-6b8f-4e44-8331-63fa85f858c2#BKMK_ADFSSnapin">Opening the ADFS Management Snap-in</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="c66c7f4b-6b8f-4e44-8331-63fa85f858c2#BKMK_ConfigureDNS">Configuring Name Resolution for AD FS Services</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="c66c7f4b-6b8f-4e44-8331-63fa85f858c2#BKMK_AddNodesToFarm">Adding nodes to the farm</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="c66c7f4b-6b8f-4e44-8331-63fa85f858c2#BKMK_AddWebAppProxy">Adding a Web Application Proxy</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="c66c7f4b-6b8f-4e44-8331-63fa85f858c2#BKMK_InstallDRS">Installing Device Registration Service</link>
        </para>
      </listItem>
    </list>
    <para>For more information about how to deploy AD FS, see <legacyLink xlink:href="dccc483a-4df5-49bd-bc7a-39b6d42cee4c">How to deploy AD FS in Windows Server 2012 R2</legacyLink>. </para>
  </introduction>
  <section address="BKMK_ADFSSnapin">
    <title>Opening the ADFS Management Snap-in</title>
    <content>
      <para>The ADFS Management Snap-in is used to configure AD FS settings, including Relying Party Trusts, Multifactor authentication, and multifactor access control. To open AD FS Management, in <ui>Server Manager</ui>, click <ui>Tools</ui>, and then click <ui>AD FS Management</ui>.  </para>
    </content>
  </section>
  <section address="BKMK_ConfigureDNS">
    <title>Configuring Name Resolution for AD FS Services</title>
    <content>
      <para>In order for AD FS to function, clients must be able to resolve the federation service name, such as fs.contoso.com, to the correct IP address: either the IP address of a federation server or farm (for clients on the internal corporate network), or to the IP address of a web application proxy or proxy farm (for external clients).</para>
      <para>The steps in this section describe how to configure DNS to resolve the federation service name and how to validate name resolution. </para>
    </content>
    <sections>
      <section>
        <title>Create A or AAAA (Host) records for the Federation Service Name</title>
        <content>
          <para>After you install a federation server or farm, and after you install a Web Application Proxy server or farm, create A Host records so DNS clients can locate the servers by their friendly names.</para>
          <para>If you deploy only one AD FS server, create a record that points to the IP address of the federation server. If you deploy a federation server farm, create a record that points to the IP address of a load balancer for the federation server farm.</para>
          <para>If you deploy only one AD FS server, create an A record that points to the name of the federation server. If you deploy a federation server farm, create an A record that points to the IP address of a load balancer for the federation server farm. The same holds true if you deploy a Web Application Proxy server or farm – create an A record that points to the IP address of the Web Application Proxy server or to the external IP address of the load balancer for the Web Application Proxy server farm.  </para>
          <procedure>
            <title>To create an A or AAAA (Host) record for the AD FS federation service name</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Log on to a DNS server using an account that has permission to create resource records in the DNS zone, such as DNS administrator or if you have deployed Active Directory-integrated DNS, a Domain Admin.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Server Manager</ui>, click <ui>Tools</ui>, and then click <ui>DNS</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Expand the name of the DNS server, expand <ui>Forward Lookup Zones</ui>, right-click the name of the zone (for example, contoso.com) where you want to create the record, and click <ui>New Host (A or AAAA)</ui>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Name</ui>, type the single-label name of the AD FS services. For example, if the service is named FS.contoso.com, type <userInputLocalizable>FS1</userInputLocalizable>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>IP address</ui>, type the IP address for the federation server or load balancer, for example, 192.168.1.4.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Click <ui>Add Host</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
</content>
      </section>
      <section>
        <title>Create CNAME record for the Device Registration Service</title>
        <content>
          <para />
          <para>A CNAME record is required in order to enable name resolution for the Device Registration Service (DRS). A CNAME record is used as an alias for another type of record in DNS. The CNAME record helps DNS clients query for a service by its friendly name rather than by the fully qualified domain name of the host. The CNAME record for the DRS should use enterpriseregistration for the alias name and point to the name of the Host A or AAAA record created above for the federation service.</para>
          <procedure>
            <title>To create a CNAME record for DRS</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Log on to a DNS server using an account that has permission to create resource records in the DNS zone, such as DNS administrator or if you have deployed Active Directory-integrated DNS, a Domain Admin.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Server Manager</ui>, click <ui>Tools</ui>, and then click <ui>DNS</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Expand the name of the DNS server, expand <ui>Forward Lookup Zones</ui>, right-click the name of the zone (for example, contoso.com) where you want to create the record, and click <ui>New Alias (CNAME)</ui>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>Under <ui>Alias name:</ui>, type <userInputLocalizable>enterpriseregistration</userInputLocalizable>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Under <ui>Fully qualified domain name (FQDN) for target host:</ui>, type the FQDN of the Host A or AAAA record that you created for the federation server or service. For example, type <userInputLocalizable>fs.contoso.com</userInputLocalizable>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
      <section>
        <title>Verify federation service name resolution</title>
        <content>
          <para>After you create the DNS records, at a standard command line, type <embeddedLabel>ipconfig /flushdns</embeddedLabel> to clear the DNS cache on each server and client. Then validate name resolution for the federation service and the IP address by using the following procedure. </para>
          <procedure>
            <title>To verify federation service name resolution</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open a browser window and in the address bar, type the federation service name, and then append it with <userInputLocalizable>federationmetadata/2007-06/federationmetadata.xml</userInputLocalizable> to browse to the federation service metadata endpoint. For example:</para>
                  <code>https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</code>
                  <para>You should see the federation server metadata.  If you have not imported the root CA certificate of your SSL certificate into the local computer trusted root certificates store on your client computer, you may see an SSL error or warning.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>You can also browse to the AD FS sign-in page (your federation service name appended with <userInputLocalizable>adfs/ls/idpinitiatedsignon.htm</userInputLocalizable>. For example: </para>
                  <code>https://fs.contoso.com/adfs/ls/idpinitiatedsignon.htm</code>
                  <para>This displays the AD FS sign-in page where you can sign in with domain administrator credentials.</para>
                  <alert class="important">
                    <para>Make sure to configure your browser settings to trust the federation server role by adding your federation service name (for example, <userInputLocalizable>https://fs.contoso.com</userInputLocalizable>) to the browser’s local intranet zone.  This will enable seamless sign-in using Windows Integrated Authentication.</para>
                  </alert>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_AddNodesToFarm">
    <title>Adding nodes to the farm</title>
    <content>
      <para>You can add nodes to the AD FS farm by installing AD FS on additional servers in the domain. Adding nodes to the farm provides redundancy and fault tolerance to the AD FS deployment, and allows for load balancing client service requests. </para>
      <para>To add nodes to an existing farm, choose Add a federation server to a federation server farm on the Welcome page of the Active Directory Federation Services Configuration Wizard, or use the Add-AdfsFarmNode Windows PowerShell cmdlet.  </para>
      <para>After you add nodes to a farm, you should install a load balancer such as Network Load Balancing in Windows Server and create a Host record that maps the name of the load balancer to its IP address. </para>
      <para>For more information about adding nodes to the farm, see <legacyLink xlink:href="dccc483a-4df5-49bd-bc7a-39b6d42cee4c">How to deploy AD FS in Windows Server 2012 R2</legacyLink>.</para>
    </content>
  </section>
  <section address="BKMK_AddWebAppProxy">
    <title>Adding a Web Application Proxy</title>
    <content>
      <para>The Web Application Proxy can provide access to web applications from extranet clients using AD FS claims-based authentication or Windows Integrated Authentication. The Web Application Proxy can be used in conjunction with Active Directory workplace join, multifactor authentication, or multifactor access control in order to enable more flexible and manageable resource access by users and devices outside of a company firewall. </para>
      <para>For more information about adding a Web Application Proxy, see <legacyLink xlink:href="dccc483a-4df5-49bd-bc7a-39b6d42cee4c">How to deploy AD FS in Windows Server 2012 R2</legacyLink>.</para>
      <para>For a feature overview and more information about installing and configuring Web Application proxy, see the following topic:</para>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="9c9c4e8f-6635-4774-b6e1-f144b5d7ded8">Connect to Applications and Services from Anywhere with Web Application Proxy</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_InstallDRS">
    <title>Enabling Device Registration Service</title>
    <content>
      <para>To enable the Device Registration Service in the local forest, the following prerequisites must be met:</para>
      <list class="bullet">
        <listItem>
          <para>The Active Directory schema must be at <token>winblue_server_1</token> level. </para>
        </listItem>
        <listItem>
          <para>You need to run Windows PowerShell cmdlets as a member of the Enterprise Admins group in order to enable DRS.</para>
        </listItem>
        <listItem>
          <para>The group managed service account that was specified for the AD FS configuration must be specified for the value of the <embeddedLabel>–ServiceAccountName</embeddedLabel> parameter in the format <placeholder>domain</placeholder>\<placeholder>account_name</placeholder>. </para>
        </listItem>
      </list>
      <para>For specific information about how to enable DRS after deploying AD FS in a forest, see <legacyLink xlink:href="dccc483a-4df5-49bd-bc7a-39b6d42cee4c">How to deploy AD FS in Windows Server 2012 R2</legacyLink>.</para>
      <para>For a feature overview and more information about installing and configuring DRS, see the following topic:</para>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="b86471af-4f72-4927-bdfa-b32fa3b9f826">Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>