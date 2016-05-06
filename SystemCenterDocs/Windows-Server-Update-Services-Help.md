---
title: Windows Server Update Services Help
ms.custom: na
ms.prod: windows-server-2012-r2
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2660fb74-7619-4b8f-b6a2-c674c4ef90d5
---
# Windows Server Update Services Help
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic provides an overview about WSUS, and links to additional information pertaining to WSUS and related technologies.</para>
    <para>The Windows Server Update Service (WSUS) enables information technology administrators to deploy the latest Microsoft product updates. By using WSUS, administrators can fully manage the distribution of updates that are released through Microsoft Update to their network computers.</para>
    <para>Update management is the process of controlling the deployment and maintenance of interim software releases into production environments. It helps you maintain operational efficiency, overcome security vulnerabilities, and maintain the stability of your production environment. If your organization cannot determine and maintain a known level of trust within its operating systems and application software, it might have a number of security vulnerabilities that, if exploited, could lead to a loss of revenue and intellectual property. Minimizing this threat requires you to have properly configured systems, use the latest software, and install the recommended software updates.</para>
    <para>The core scenarios where WSUS adds value to your business are centralized update management, and update management automation.</para>
    <para>A WSUS server can be the update source for other WSUS servers within the organization. The WSUS server that acts as an update source is called an upstream server. In a WSUS implementation, at least one WSUS server in the network must connect to Microsoft Update to get available update information. The administrator can determine, based on network security and configuration, how many other servers connect directly to Microsoft Update.</para>
    <para>Prior to <token>win8_server_./Token>, WSUS was not, by default, part of the server operating system; installation required that you first download the WSUS software from the Microsoft Download Center. Starting in <token>win8_server_./Token>, WSUS is integrated with the server operating system as a server role.</para>
  </introduction>
  <section>
    <title>More information about how to deploy and manage WSUS</title>
    <content>
      <para>For information about how to deploy and manage WSUS, see the following topics:</para>
      <list class="bullet">
        <listItem>
          <para>For detailed information about creating computer groups in WSUS, see section <embeddedLabel>3.3. Configure computer groups</embeddedLabel>, in: <externalLink><linkText>Step 3: Configure WSUS</linkText><linkUri>http://technet.microsoft.com/library/hh852346.aspx</linkUri></externalLink>.</para>
        </listItem>
        <listItem>
          <para>For information about how to assign computers and groups using Group Policy, see section <embeddedLabel>3.4. Configure client updates</embeddedLabel>, in: <externalLink><linkText>Step 3: Configure WSUS</linkText><linkUri>http://technet.microsoft.com/library/hh852346.aspx</linkUri></externalLink>.</para>
        </listItem>
        <listItem>
          <para>For information about using Secure Sockets Layer (SSL) protocol to help protect Windows Server Update Services (WSUS), see section <embeddedLabel>3.5. Secure WSUS with the Secure Sockets Layer Protocol</embeddedLabel>, in: <externalLink><linkText>Step 3: Configure WSUS</linkText><linkUri>http://technet.microsoft.com/library/hh852346.aspx</linkUri></externalLink>.</para>
        </listItem>
        <listItem>
          <para>For information about <embeddedLabel>configuring auto-approval rules</embeddedLabel>, see section <embeddedLabel>4.2. Configure auto-approval rules</embeddedLabel>, in: <externalLink><linkText>Step 4: Approve and Deploy WSUS Updates</linkText><linkUri>http://technet.microsoft.com/library/hh852348.aspx</linkUri></externalLink></para>
        </listItem>
      </list>
      <para>For information about migrating WSUS 3.0 SP2 to <token>winblue_server_./Token> and <token>win8_server_./Token>, see:</para>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Migrate Windows Server Update Services to Windows Server 2012</linkText>
              <linkUri>http://technet.microsoft.com/library/hh852339.aspx</linkUri>
            </externalLink>
          </para>
          <list class="bullet">
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 1: Plan for WSUS Migration</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852352.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 2: Prepare to Migrate WSUS</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852347.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 3: Migrate WSUS</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852349.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 4: Verify the WSUS Migration</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852343.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
          </list>
        </listItem>
      </list>
      <para>For information about deploying WSUS in <token>winblue_server_./Token> and <token>win8_server_./Token>, see:</para>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Deploy Windows Server Update Services in Your Organization</linkText>
              <linkUri>http://technet.microsoft.com/library/hh852340.aspx</linkUri>
            </externalLink>
          </para>
          <list class="bullet">
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 1: Prepare for Your WSUS Deployment</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852344.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 2: Install the WSUS Server Role</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852338.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 3: Configure WSUS</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852346.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
            <listItem>
              <para>
                <externalLink>
                  <linkText>Step 4: Approve and Deploy WSUS Updates</linkText>
                  <linkUri>http://technet.microsoft.com/library/hh852348.aspx</linkUri>
                </externalLink>
              </para>
            </listItem>
          </list>
        </listItem>
      </list>
      <para>Additional resources:</para>
      <list class="bullet">
        <listItem>
          <para>The <externalLink><linkText>Windows Server Update Services</linkText><linkUri>http://technet.microsoft.com/windowsserver/bb332157.aspx</linkUri></externalLink> TechCenter home page, on TechNet.</para>
        </listItem>
        <listItem>
          <para>For overview information about Server Roles, Features, and server technologies, see: <externalLink><linkText>Server Roles and Technologies</linkText><linkUri>http://technet.microsoft.com/library/hh831669.aspx</linkUri></externalLink></para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

