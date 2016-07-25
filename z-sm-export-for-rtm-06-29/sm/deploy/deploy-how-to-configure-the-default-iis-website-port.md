---
title: How to Configure the Default IIS Website Port
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e48fb208-3c9a-478b-b9dc-be18df10da63
author: cfreemanwa
robots: noindex,nofollow


















---
# How to Configure the Default IIS Website Port
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>When you installed Internet Information Services (IIS), the default website was configured to use port 80. The SharePoint Web Parts is the home page for the <token>smssp</token>. If you want to install the SharePoint Web Parts on port 80, you must first move the default website in IIS to a different port-for example, port 8080-and then install the SharePoint Web Parts on port 80.</para>
    <para>Use the following procedure to move the IIS default website to port 8080 so that you can install the SharePoint website on port 80.</para>
  </introduction>
  <procedure>
    <title>To configure the default IIS website to use port 8080</title>
    <steps class="ordered">
      <step>
        <content>
          <para>On the Windows desktop, click <ui>Start</ui>, click <ui>Administrative Tools</ui>, and then click <ui>Internet Information Services (IIS) Manager</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In <ui>Internet Information Services (IIS) Manager</ui>, in the <ui>Connections</ui> pane, expand the computer name, expand <ui>Sites</ui>, and then click <ui>Default Web Site</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Actions</ui> pane, under <ui>Edit Site</ui>, click <ui>Bindings</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Site Bindings</ui> dialog box, click the <ui>http</ui> entry, and then click <ui>Edit</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Edit Site Binding</ui> dialog box, in <ui>Port</ui>, type <userInput>8080</userInput>, and then click <ui>OK</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Site Bindings</ui> dialog box, click <ui>Close</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>In the <ui>Actions</ui> pane, under <ui>Manage Web Site</ui>, click <ui>Stop</ui>, and then click <ui>Start</ui>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics />
</developerHowToDocument>