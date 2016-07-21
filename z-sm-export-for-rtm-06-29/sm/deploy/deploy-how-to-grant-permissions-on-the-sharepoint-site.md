---
title: How to Grant Permissions on the SharePoint Site
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54a505d1-f84b-4ac8-92f5-76c73cd2e5c9
author: cfreemanwa
robots: noindex,nofollow


















---
# How to Grant Permissions on the SharePoint Site
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Use the following procedure to grant permissions to the <token>smssp</token> SharePoint site in <token>smlong12</token>.</para>
  </introduction>
  <procedure>
    <title>To grant permissions on the Self-Service Portal SharePoint site</title>
    <steps class="ordered">
      <step>
        <content>
          <para>Log on to the computer that hosts the SharePoint Web site with administrative credentials.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Open a browser and connect to the SharePoint site at http://localhost:&lt;port&gt;/_layouts/settings.aspx.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the upper left area of the web page, click <ui>Site Actions</ui>, and then click <ui>Site Permissions</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the SharePoint ribbon, click <ui>Grant Permissions</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Grant Permissions</ui> box, in the <ui>Users/Groups</ui> box, type the Active&nbsp;Directory name for the users or user groups to whom you want to grant access.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Grant Permissions</ui> area, click <ui>Read - Can view pages and list items and download documents</ui>, and then click <ui>OK</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Close the browser.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics>
    <link xlink:href="0b8aa677-1b20-49bc-941f-d225bd2852e0">How to Verify the Installation of the Self-Service Portal</link>
  </relatedTopics>
</developerHowToDocument>