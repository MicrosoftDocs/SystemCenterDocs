---
title: Prerequisites for installing AD FS
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf7f9cf4-6170-40e8-83dd-e636cb4f9ecb
---
# Prerequisites for installing AD FS
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic summarizes AD FS installation permission requirements and other prerequisites, including options to extend the Active Directory schema to create objects and containers that are required to support Device Registration Service (DRS) for Active Directory Workplace Join. For more detailed information about deploying AD FS, see <legacyLink xlink:href="dccc483a-4df5-49bd-bc7a-39b6d42cee4c">How to deploy AD FS in Windows Server 2012 R2</legacyLink>. </para>
  </introduction>
  <section address="BKMK_InstallPermissions">
    <title>Installation permission requirements</title>
    <content>
      <para>This section covers permissions that are required to install Active Directory Federation Services (AD FS).  </para>
      <list class="bullet">
        <listItem>
          <para>To install any server role or feature, including the AD FS server role or the Web Application Proxy role service (part of the Remote Access server role), you must be a member of the local Administrators group on the target server. </para>
        </listItem>
        <listItem>
          <para>To configure AD FS, whether you create a new federation server farm or add nodes to an existing federation server farm, you must be a member of the Domain Admins group in the domain to which the federation server is joined. </para>
        </listItem>
        <listItem>
          <para>To configure Web Application Proxy, you must be a member of the local Administrators group on the target server, and you must have the credentials of a local administrator on the AD FS server.</para>
        </listItem>
        <listItem>
          <para>To enable the Device Registration Service (DRS), you need to be a member of the Enterprise Admins group or the Domain Admins group in the root domain of the forest in order to create the DRS configuration and registered device containers and objects in Active Directory. </para>
          <para>DRS also requires the <token>winblue_server_./Token> Active Directory schema. To extend the schema, you must run <embeddedLabel>adprep /forestprep</embeddedLabel>, which requires Schema Admins, Enterprise Admins, and Domain Admins credentials. For more information about how to run <embeddedLabel>adprep /forestprep</embeddedLabel>, see <externalLink><linkText>Running Adprep.exe</linkText><linkUri>http://technet.microsoft.com/library/dd464018(v=ws.10).aspx</linkUri></externalLink>. </para>
        </listItem>
      </list>
    </content>
  </section>
  <section>
    <title>Hardware and software prerequisites</title>
    <content>
      <para>The following table lists hardware and software prerequisites.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <tbody>
          <tr>
            <TD>
              <para>
                <?Comment JTH: Per Mitica,By default the expectation is to not require different hw requirements than the previous version, so please use the 2.1 ones 2013-05-30T13:09:00Z  Id='0?>Hardwar<?CommentEnd Id='0'
    ?>e</para>
            </TD>
            <TD>
              <para>Minimum requirement</para>
              <list class="bullet">
                <listItem>
                  <para>CPU: <?Comment JTH: Changed to match min listed by Jaime for WS 2012 athttp://technet.microsoft.com/en-us/library/jj134246.aspx 2013-05-30T13:09:00Z  Id='1?>Single-core, 1.4 gigahertz (GHz) 64-bit processor<?CommentEnd Id='1'
    ?></para>
                </listItem>
                <listItem>
                  <para>RAM: 1 GB</para>
                </listItem>
                <listItem>
                  <para>Disk space: 50 MB</para>
                </listItem>
              </list>
              <para>Recommended configuration:</para>
              <list class="bullet">
                <listItem>
                  <para>CPU: Quad-core, 2 GHz</para>
                </listItem>
                <listItem>
                  <para>RAM: 4 GB</para>
                </listItem>
                <listItem>
                  <para>Disk space: 100 MB</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Certificates</para>
            </TD>
            <TD>
              <list class="bullet">
                <listItem>
                  <para>SSL Server Authentication Certificate: This certificate must be trusted publicly (chained to a public root certification authority) or explicitly trusted by all computers that require access to the federation service. </para>
                  <para>You must have both the certificate and its private key available. For example, if you have the certificate and its private key in a .pfx file, you can import the file directly into the Active Directory Federation Services Configuration Wizard. This SSL certificate must contain the following:</para>
                  <list class="ordered">
                    <listItem>
                      <para>Subject name or subject alternative name must contain the exact name of your federation service such as <embeddedLabel>fs.contoso.com</embeddedLabel> or a matching wildcard expression such as <embeddedLabel>*.contoso.com</embeddedLabel></para>
                    </listItem>
                    <listItem>
                      <para>If you plan to use DRS for Active Directory Workplace Join, the subject name or subject alternative name must contain the value <embeddedLabel>enterpriseregistration</embeddedLabel> followed by the UPN suffix of your organization. For example, <embeddedLabel>enterpriseregistration.corp.contoso.com</embeddedLabel>.</para>
                      <para>If your organization uses multiple UPN suffixes, the SSL certificate must contain a subject alternative name entry for each suffix.</para>
                    </listItem>
                  </list>
                </listItem>
                <listItem>
                  <para>Token signing and token decryption certificate: By default, a token-signing certificate and a token decryption certificate are created automatically during the AD FS installation and do not have to be provided by the administrator.</para>
                  <para>Optionally, certificates that are issued by your corporate certification authority (CA) or a third-party CA can be used for token signing and token encryption certificates, but this configuration option requires that you use Windows PowerShell and not the AD FS Configuration Wizard to create the farm or to add farm nodes. If you choose to use this option, the certificates do not need to be trusted publicly. However, relying party federation servers and applications that consume tokens issued by the federation service will need to trust this certificate as part of their claims provider trust configuration.</para>
                </listItem>
                <listItem>
                  <para>Service Communications Certificate: This certificate is used for scenarios that require message security. This certificate is distinct from the SSL certificate of the federation server. By default, the initial AD FS configuration assigns the certificate that the administrator provides as the SSL certificate to the service communications certificate role. This can be changed after initial AD FS configuration by using the AD FS Management snap-in. To manage the Service Communications Certificate, use the AD FS Management snap-in. For more information, see <externalLink><linkText>Set a Service Communications Certificate</linkText><linkUri>http://technet.microsoft.com/library/dd807075.aspx</linkUri></externalLink>. </para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Browser</para>
            </TD>
            <TD>
              <para>Any web browser with JavaScript capability can work as an AD FS client. JavaScript must be enabled, and cookies must be enabled for browser-based sign-in and sign-out. Support for Transport Layer Security/Secure Sockets Layer (TLS/SSL) is also required.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Device Registration Service (DRS)</para>
            </TD>
            <TD>
              <para>To install the DRS, the Active Directory schema must be <token>winblue_server_./Token>. For more information about how to extend the schema, see <externalLink><linkText>Running Adprep.exe</linkText><linkUri>http://technet.microsoft.com/library/dd464018(v=WS.10).aspx</linkUri></externalLink>.</para>
            </TD>
          </tr>
        </tbody>
      </table>
</content>
  </section>
  <section>
    <title>Updating the AD DS schema to support Device Registration Service</title>
    <content>
      <para>To create the new containers and objects, the AD DS schema must be extended to the <token>winblue_server_./Token> level. For the permissions that are required to update the AD DS schema, see <link xlink:href="bf7f9cf4-6170-40e8-83dd-e636cb4f9ecb#BKMK_InstallPermissions">Installation permission requirements</link>. There are three ways to extend the schema:</para>
      <list class="bullet">
        <listItem>
          <para>In an existing Active Directory forest, run <embeddedLabel>adprep /forestprep</embeddedLabel> from the \Support\Adprep folder of the <token>winblue_server_./Token> operating system DVD on any 64-bit server that runs Windows Server 2008 or later. In this case, no additional domain controller has to be installed, and no existing domain controllers have to be upgraded. </para>
          <para>To run <embeddedLabel>adprep /forestprep</embeddedLabel>, you must be a member of the Schema Admins group, the Enterprise Admins group, and the Domain Admins group of the domain that hosts the schema master. </para>
        </listItem>
        <listItem>
          <para>In an existing Active Directory forest, install a domain controller that runs <token>winblue_server_./Token>. In this case, <embeddedLabel>adprep /forestprep</embeddedLabel> runs automatically as part of the domain controller installation.</para>
          <para>During the domain controller installation, you must enter additional credentials to run <embeddedLabel>adprep /forestprep</embeddedLabel>. </para>
        </listItem>
        <listItem>
          <para>Create a new Active Directory forest by installing AD DS on a server that runs <token>winblue_server_./Token>. In this case, <embeddedLabel>adprep /forestprep</embeddedLabel> does not need to be run because the schema will be initially created with all the necessary containers and objects to support DRS.</para>
          <para>To create a new forest, you must be a member of the Administrators group on the server where you install AD DS.</para>
        </listItem>
      </list>
      <para>For more information about Adprep.exe, see <externalLink><linkText>Running Adprep.exe</linkText><linkUri>http://technet.microsoft.com/library/dd464018(v=WS.10).aspx</linkUri></externalLink>. For a list of objects and containers that are created when the AD DS schema is extended for <token>winblue_server_./Token>, <?Comment JTH: I should add a list here of what the objects are, not the whole ldf file but just a list of the objects. Then link as planed to the topic about the changes made by adprep.Pad:There are no new forest or domain operations in this release.These ldfs contain DRS schema changes:Sch59Sch61Sch62Sch63Sch64Sch65Sch67Enterprise client sync:Sch66MSODSSch60(There is one more incoming schema change for a MP feature and will be in sch68). 2013-06-13T10:34:00Z  Id='3?>see the SCH.ldf files that are listed for DRS in <?CommentEnd Id='3'
    ?><externalLink><linkText>Changes to Adprep</linkText><linkUri>http://technet.microsoft.com/library/jj916254.aspx</linkUri></externalLink>.</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

