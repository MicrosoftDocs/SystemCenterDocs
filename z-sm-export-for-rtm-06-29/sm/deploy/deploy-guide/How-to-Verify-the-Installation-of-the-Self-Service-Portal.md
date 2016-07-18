---
title: How to Verify the Installation of the Self-Service Portal
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0b8aa677-1b20-49bc-941f-d225bd2852e0
author: cfreemanwa
robots: noindex,nofollow
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Verify the Installation of the Self-Service Portal
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The default portal name for the <token>smssp</token> in <token>smlong12</token> is SMPortal. Use the following procedure to verify the installation of the <token>smssp</token>.</para>
  </introduction>
  <procedure>
    <title>To verify the installation of the Self-Service Portal</title>
    <steps class="ordered">
      <step>
        <content>
          <para>On the computer hosting the SharePoint Web site, open Internet Explorer.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the address line, type one of the following:</para>
          <list class="ordered">
            <listItem>
              <para>http://localhost:&lt;port&gt;/SMPortal (if you are not using Secure Sockets Layer (SSL))</para>
            </listItem>
            <listItem>
              <para>https://localhost:&lt;port&gt;/SMPortal (if you are using SSL)</para>
            </listItem>
          </list>
          <para>Where &lt;port&gt; is the port number that is defined when the SharePoint Parts server is installed.</para>
        </content>
      </step>
      <step>
        <content>
          <para>The default home page for the <token>smssp</token> should appear as shown <?Comment jhb: I don’t know if we have control over this. But a message appears in this UI that uses the expression “canned requests”. “Canned” is jargon, with a negative connotation. “Pre-prepared” or “prepared in advance” might be better alternatives.Can we get this UI text modified? 2011-10-18T11:35:00Z  Id='1?>in the following illustration.<?CommentEnd Id='1'
    ?></para>
          <mediaLink>
            <image xlink:href="1de60bb6-1cc5-467d-8377-db70b4cd6006" />
          </mediaLink>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics />
</developerHowToDocument>