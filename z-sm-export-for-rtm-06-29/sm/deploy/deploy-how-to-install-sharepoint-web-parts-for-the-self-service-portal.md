---
title: How to Install SharePoint Web Parts for the Self-Service Portal
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55ed8428-80ea-4f78-a664-99ba573a8aac
author: cfreemanwa
robots: noindex,nofollow


















---
# How to Install SharePoint Web Parts for the Self-Service Portal
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The home page for the <token>smssp</token> in <token>smlong12</token> is on the SharePoint Web Parts server. We recommend that you use Secure Sockets Layer (SSL) and install the SharePoint Web Parts using port 443.</para>
    <para>When you installed Internet Information Services (IIS), the default website was configured to use port 80. If you want to install the SharePoint Web Parts on port 80, you must first move the default website in IIS to a different port—for example, port 8080—and then install the SharePoint Web Parts on port 80.</para>
    <para>You can use this information to share Excel workbooks using SharePoint. For an example, see <externalLink><linkText>Configure Excel Services for a BI test environment</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkId=232429</linkUri></externalLink>.</para>
    <para>Use the following procedure to install the SharePoint Web Parts server.</para>
  </introduction>
  <procedure>
    <title>To install the SharePoint Web Parts server</title>
    <steps class="ordered">
      <step>
        <content>
          <para>Using the Operational Database Account, log on to the computer that will host the <token>smssp</token>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <token>smlong12</token> installation media, double-click the <ui>Setup.exe</ui> file. </para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Service Manager Setup Wizard</ui> page, click <ui>Service Manager web portal</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Portal Parts</ui> page, click <ui>SharePoint Web Parts</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Product registration</ui> page, read the Microsoft Software License Terms, and, if applicable, click <ui>I have read, understood, and agree with the terms of the license terms</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>System check results</ui> page, make sure that the prerequisite check passed or at least passed with warnings, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure the Service Manager SharePoint site</ui> page, complete these steps:</para>
          <list class="ordered">
            <listItem>
              <para>In the <ui>SSL certificate</ui> list, select the Secure Sockets Layer (SSL) certificate that you want to use with the <token>smssp</token>, and then click <ui>Next</ui>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Port</ui> text box, accept the default port, or type a new port. For example, type <userInput>443</userInput>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>URL</ui> text box, type the URL for the web content server in the form of http://&lt;computername&gt;:&lt;port&gt; or https://&lt;computername&gt;:&lt;port&gt;.</para>
            </listItem>
            <listItem>
              <para>Click in any of the other text boxes, and then click <ui>Next</ui>.</para>
            </listItem>
          </list>
          <alert class="note">
            <para>We strongly recommend the use of SSL. If you are using a self-signed certificate, make sure that the certification authority (CA) that issues the certificate has been added to the Trusted Root Certification Authorities store. You must use the same HTTP protocol (HTTP or HTTPS) with both portal parts.</para>
          </alert>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure the account for the Service Manager SharePoint app pool</ui> page, type a domain user and password, and then click <ui>Test Credentials</ui>. After you verify that you received a “The credentials were accepted” message, click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Help improve System Center Service Manager</ui> page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click <ui>Tell me more about the program</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Use Microsoft Update to help keep your computer secure and up-to-date</ui> page, indicate your preference for using Microsoft Update to check for <token>smshort</token> updates. If you want Windows Update to check for updates, select <ui>Initiate machine wide Automatic update</ui>. Click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Installation summary</ui> page, click <ui>Install</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Setup completed successfully</ui> page, click <ui>Close</ui>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics>
    <link xlink:href="54a505d1-f84b-4ac8-92f5-76c73cd2e5c9">How to Grant Permissions on the SharePoint Site</link>
  </relatedTopics>
</developerHowToDocument>