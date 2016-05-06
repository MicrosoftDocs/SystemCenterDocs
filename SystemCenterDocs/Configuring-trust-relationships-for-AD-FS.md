---
title: Configuring trust relationships for AD FS
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c0857cb-52eb-4139-8b08-9487c53c9496
---
# Configuring trust relationships for AD FS
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para />
    <para>After you deploy the first federation server in the account partner organization, <?Comment SE(L: Would &quot;open&quot; be a better word than &quot;use&quot;? 2013-11-08T15:07:00Z  Id='0?>use <?CommentEnd Id='0'
    ?>the AD FS Management snap-in to create a relying party trust relationship. You can create a relying party trust by entering data about a resource partner manually or by using a federation metadata URL that the administrator of the resource partner organization provides to you. You can use the federation metadata to retrieve the data for the resource partner automatically.</para>
    <alert class="note">
      <para>If the resource partner publishes its federation metadata or can provide a file copy of it for you to use, we recommend that you retrieve the data automatically because it can save time.</para>
    </alert>
    <para>Membership in <embeddedLabel>Administrators</embeddedLabel>, or equivalent, on the local computer is the minimum requirement to complete these procedures. <token>review_details</token></para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="3c0857cb-52eb-4139-8b08-9487c53c9496#BKMK_Metadata">Create a claims provider trust by using federation metadata</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="3c0857cb-52eb-4139-8b08-9487c53c9496#BKMK_Manual">Create a claims provider trust manually</link>
        </para>
      </listItem>
    </list>

</introduction>
  <section address="BKMK_Metadata">
    <title>Create a claims provider trust by using federation metadata</title>
    <content>
      <para>To add a new claims provider trust, use the AD FS Management snap-in. The snap-in automatically imports configuration data about the partner from federation metadata that the partner has published to a local network or to the Internet. Perform the following procedure on a federation server in the resource partner organization.</para>
      <alert class="note">
        <para>To query federation metadata, you should only use a fully qualified domain name, such as https://myserver.contoso.com.</para>
      </alert>
      <procedure>
        <title>To create a claims provider trust by using federation metadata</title>
        <steps class="ordered">
          <step>
            <content>
              <para>
                <token>winblue_start</token> <userInput>AD FS Management</userInput>, and then press Enter.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Under <ui>AD FS\Trust Relationships</ui>, right-click <ui>Claims Provider Trusts</ui>, and then click <ui>Add Claims Provider Trust</ui> to open the Add Claims Provider Trust Wizard.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Welcome</ui> page, click <ui>Start</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Select Data Source</ui> page, click <ui>Import data about the claims provider published online or on a local network</ui>. In <ui>Federation metadata address (host name or URL)</ui>, type the federation metadata URL or host name for the partner, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Specify Display Name</ui> page, type a <ui>Display name</ui>, under <ui>Notes</ui>, type a description for this claims provider trust, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Ready to Add Trust</ui> page, click <ui>Next</ui> to save your claims provider trust information.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Finish</ui> page, click <ui>Close</ui>. This action automatically displays the <ui>Edit Claim Rules</ui> dialog box. For more information about how to proceed with adding claim rules for this claims provider trust, see the "Additional references" section <?Comment SE(L: Per MSTP:Use instead ofbelowin cross-references. For example, say &quot;later in this topic.There is no &quot;Additional references section&quot; in this topic. Is it to be added, or do you link to another section in a different topic?This reference occurs here and in the last line of this topic. 2013-11-08T15:07:00Z  Id='71?>later in this topic<?CommentEnd Id='71'
    ?>.</para>
              <alert class="important">
                <para>If trusted certificate stores have been modified previously on this computer, verify that the service account that is assigned to this Federation Service trusts the <?Comment SE(L: In topic &quot;Prerequisites for installing AD FS&quot; , it was calledSSL server authentication certificate. Is the normally used name &quot;SSL certificate&quot;, or should you add &quot;also named SSL server authentication certificate&quot;? 2013-11-08T15:07:00Z  Id='76?>SSL certificate <?CommentEnd Id='76'
    ?>that is used to secure the federation metadata retrieval. If the service account does not trust the SSL certificate of this claims provider, monitoring of the trust fails. To prevent this failure, ensure that the issuer of the claims provider’s SSL certificate is in the Local Computer Trusted Root Certification Authorities certificate store on each federation server in the farm.</para>
              </alert>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <section address="BKMK_Manual">
    <title>Create a claims provider trust manually</title>
    <content>
      <para>To add a new claims provider trust, use the AD FS Management snap-in and manually configure the settings. Perform the following procedure on a resource partner federation server in the resource partner organization.</para>
      <procedure>
        <title>To create a claims provider trust manually</title>
        <steps class="ordered">
          <step>
            <content>
              <para>
                <token>winblue_start</token> <userInput>AD FS Management</userInput>, and then press Enter.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Under the <ui>AD FS\Trust Relationships</ui>, right-click <ui>Claims Provider Trusts</ui>, and then click <ui>Add Claims Provider Trust</ui> to open the Add Claims Provider Trust Wizard.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Welcome</ui> page, click <ui>Start</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Select Data Source</ui> page, click <ui>Enter claims provider trust data manually</ui>, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Specify Display Name</ui> page, type a <ui>Display name</ui>, under <ui>Notes</ui>, type a description for this claims provider trust, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Choose Profile</ui> page, do one of the following:</para>
              <list class="bullet">
                <listItem>
                  <para>Click <ui>AD FS Profile</ui>, click <ui>Next</ui>, and then go to step 7.</para>
                </listItem>
                <listItem>
                  <para>Click <ui>AD FS 1.0 and 1.1 profile</ui>, click <ui>Next</ui>, and then move to step 8.</para>
                </listItem>
              </list>
              <para>If you know that you require interoperability between this claims provider trust and other, older Active Directory Federation Services (AD FS) claims provider trusts, click <ui>AD FS 1.0 and 1.1 profile</ui>. Otherwise, use the default <ui>AD FS profile</ui> option.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Configure URL</ui> page, do one or both of the following, click <ui>Next</ui>, and then go to step 9:</para>
              <list class="bullet">
                <listItem>
                  <para>Select the <ui>Enable support for the WS-Federation Passive protocol</ui> check box. Under <ui>Claims provider WS-Federation Passive protocol URL</ui>, type the URL for this claims provider trust, and then click <ui>Next</ui>.</para>
                </listItem>
                <listItem>
                  <para>Select the <ui>Enable support for the SAML 2.0 WebSSO protocol</ui> check box. Under <ui>Claims provider SAML 2.0 SSO service URL</ui>, type the Security Assertion Markup Language (SAML) service endpoint URL for this claims provider trust, and then click <ui>Next</ui>.</para>
                </listItem>
              </list>
              <para>Click the <ui>Help</ui> button on this page for more information about which of these options apply to the requirements of your organization.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Configure URL</ui> page, under <ui>WS-Federation Passive URL</ui>, type the URL for this claims provider trust, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Configure Identifier</ui> page, under <ui>Claims provider trust identifier</ui>, type the appropriate identifier, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Configure Certificates</ui> page, click <ui>Add</ui> to locate a certificate file and add it to the list of certificates, and then click <ui>Next</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Ready to Add Trust</ui> page, click <ui>Next</ui> to save your claims provider trust information.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Finish</ui> page, click <ui>Close</ui>. This action automatically displays the <ui>Edit Claim Rules</ui> dialog box. For more information about how to proceed with adding claim rules for this claims provider trust, see the "<?Comment SE(L: Please see the commentabove. 2013-11-08T15:07:00Z  Id='109?>Additional references" section<?CommentEnd Id='109'
    ?>.</para>
            </content>
          </step>
        </steps>
      </procedure>

</content>
  </section>
  <relatedTopics />
</developerConceptualDocument>