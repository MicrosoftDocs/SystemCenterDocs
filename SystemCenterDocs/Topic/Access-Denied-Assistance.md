---
title: Access-Denied Assistance
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ef9ff28-ff5a-4fd1-a56a-a7de0520be88
---
# Access-Denied Assistance
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Access-denied assistance provides users who are denied access to a file or file share with additional information about the issue, and optionally, it suggests a way to request assistance from the designated owner or owners of the file share.</para>
  </introduction>
  <section>
    <title>Security considerations</title>
    <content>
      <para>Enabling access-denied assistance adds the Access-Denied Assistance Users group to the Remote Management Users group, which by default contains the Authenticated Users group. This allows all authenticated users to obtain assistance.</para>
      <para>The inbound Windows Firewall rule, Windows Remote Management (HTTP-In), must be enabled for access-denied assistance to work. This rule is enabled by default.</para>
    </content>
  </section>
  <section>
    <title>Message formatting considerations</title>
    <content>
      <para>The access-denied assistance messages can contain only plain text and hyperlinks that are enclosed in valid HTML &lt;a&gt; tags. For example, &lt;a href="http://support.microsoft.com"&gt;Microsoft Support&lt;/a&gt;.</para>
    </content>
  </section>
  <section DoNotNumber="false">
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Scenario: Access-Denied Assistance</linkText>
              <linkUri>http://technet.microsoft.com/library/hh831788.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>