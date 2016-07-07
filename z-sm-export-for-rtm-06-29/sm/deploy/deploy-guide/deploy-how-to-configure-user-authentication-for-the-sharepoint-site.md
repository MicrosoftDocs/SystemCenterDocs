---
title: How to Configure User Authentication for the SharePoint Site
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eaf5b393-1de8-423e-adf1-1a2c3893712b
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
# How to Configure User Authentication for the SharePoint Site
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The option to <ui>Sign in as Different User</ui> has been removed from the Service Manager SharePoint site template file included in <token>smlong12</token>. You should not enable this option in SharePoint site template files because using the option can result in a submitted user request having an incorrect affected user.</para>
    <para>If you want to support multiple users on a computer, you should use the following procedure to configure user authentication in the browser that you use to connect to the <token>smssp</token> SharePoint site in <token>smlong12</token>. Afterward, you should notify your end-users that they should use the <ui>Sign Out</ui> option when they are done using the <token>smssp</token>.</para>
  </introduction>
  <procedure>
    <title>To configure user authentication for the <token>smssp</token> SharePoint site</title>
    <steps class="ordered">
      <step>
        <content>
          <para>Log on to the computer that hosts the SharePoint Web site with the user credentials of an end-user who will submit requests by using the <token>smssp</token>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Open Internet Explorer and then click <ui>Tools</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Select <ui>Internet Options</ui> and then click the <ui>Security</ui> tab.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Click <ui>Trusted Sites</ui> and then <ui>Custom Level</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Under <ui>User Authentication</ui> select <ui>Prompt for user name and password</ui> and then click <ui>OK</ui>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics>
    <link xlink:href="762cd06f-cd61-49ad-a757-8c7d45330125">Self-Service Portal Deployment Scenarios for System Center 2012 - Service Manager</link>
  </relatedTopics>
</developerHowToDocument>