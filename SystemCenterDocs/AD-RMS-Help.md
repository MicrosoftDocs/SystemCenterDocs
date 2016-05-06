---
title: AD RMS Help
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec6d4613-f517-4bac-9a46-a74f8c824a30
---
# AD RMS Help
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Active Directory Rights Management Services (AD RMS) is information protection technology that works with AD RMS-enabled applications to help safeguard digital information from unauthorized use, both online and offline, and inside and outside of a firewall. AD RMS is designed for organizations that need to protect sensitive and proprietary information such as financial reports, product specifications, customer data, and confidential e-mail messages. AD RMS augments an organization's security strategy by providing protection of information through persistent usage policies (also known as usage rights and conditions), which remain with the information no matter where it is moved. AD RMS persistently protects any binary format of data, so the usage rights remain with the information rather than in an organization's network. This also enables usage rights to be enforced after the information is accessed by an authorized recipient, both online and offline, and inside and outside of the organization. AD RMS helps protect information through persistent usage policies by establishing the following essential elements:</para>
    <list class="bullet">
      <listItem>
        <para>
          <embeddedLabel>Trusted entities.</embeddedLabel> Organizations can specify the entities, such as individuals, groups of users, computers, and applications that are trusted participants in an AD RMS system. By establishing trusted entities, AD RMS can help protect information by enabling access only to properly trusted participants.</para>
      </listItem>
      <listItem>
        <para>
          <embeddedLabel>Usage rights and conditions.</embeddedLabel> Organizations and individuals can assign usage rights and conditions that define how a specific trusted entity can use rights-protected content. Examples of usage rights are permission to read, copy, print, save, forward, and edit. Usage rights can be accompanied by conditions, such as when those rights expire. Organizations can exclude applications and entities from accessing the rights-protected content.</para>
      </listItem>
      <listItem>
        <para>
          <embeddedLabel>Encryption.</embeddedLabel> Encryption is the process by which data is locked by using electronic keys. AD RMS encrypts information. This makes access conditional on the successful validation of the trusted entities. Once information is locked, only trusted entities that were granted usage rights under the specified conditions (if any) can unlock or decrypt the information in an AD RMS-enabled application or browser. The defined usage rights and conditions will then be enforced by the application.</para>
      </listItem>
    </list>
    <para>The following topics provide information to assist you in accomplishing administrative tasks by using the Active Directory Rights Management Services console. Review the following topics to learn more about how to work with your AD RMS cluster.</para>
    <list class="bullet">
      <listItem>
        <para>
          <externalLink>
            <linkText>Active Directory Rights Management Services Overview</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771627.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Pre-installation Information for Active Directory Rights Management Services</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771789.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying a Single-Server Installation</linkText>
            <linkUri>http://technet.microsoft.com/library/cc730598.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying AD RMS in an Extranet</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771691.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying AD RMS in an Organization with Users in Multiple Forests</linkText>
            <linkUri>http://technet.microsoft.com/library/cc753483.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying an AD RMS Licensing-only Cluster</linkText>
            <linkUri>http://technet.microsoft.com/library/cc772087.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying AD RMS with AD FS</linkText>
            <linkUri>http://technet.microsoft.com/library/cc752998.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Checklist: Deploying AD RMS with Microsoft Federation Gateway Support</linkText>
            <linkUri>http://technet.microsoft.com/library/gg638818.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Installing an AD RMS Cluster</linkText>
            <linkUri>http://technet.microsoft.com/library/cc726041.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Installing Microsoft Federation Gateway Support</linkText>
            <linkUri>http://technet.microsoft.com/library/gg610492.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Configuring an AD RMS Cluster</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771603.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Removing an AD RMS Cluster</linkText>
            <linkUri>http://technet.microsoft.com/library/cc731877.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Working with the AD RMS Client</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771050.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>Resources for AD RMS</linkText>
            <linkUri>http://technet.microsoft.com/library/cc771334.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
      <listItem>
        <para>
          <externalLink>
            <linkText>User Interface: AD RMS</linkText>
            <linkUri>http://technet.microsoft.com/library/cc772004.aspx</linkUri>
          </externalLink>
        </para>
      </listItem>
    </list>
    <para>You can configure and manage AD RMS by using either the Windows interface or Windows PowerShell. The topics listed here describe methods for using the Windows interface. For more information about how to use Windows PowerShell for AD RMS, see <externalLink><linkText>Using Windows PowerShell with AD RMS</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=136806</linkUri></externalLink>.</para>
    <para>For more information about how to plan, deploy, and troubleshoot AD RMS, see the <externalLink><linkText>Active Directory Rights Management Services TechCenter</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=80907</linkUri></externalLink>.</para>
  </introduction>
  <relatedTopics />
</developerConceptualDocument>


