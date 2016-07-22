---
title: How to Install the Web Content Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df14d942-a4fa-4955-8822-0141bf79d271
author: cfreemanwa
robots: noindex,nofollow


















---
# How to Install the Web Content Server
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Use the following procedure to install the <token>smssp</token> web content server in <token>smlong12</token>.</para>
  </introduction>
  <procedure>
    <title>To install the web content server</title>
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
          <para>On the <ui>Portal Parts</ui> page, click <ui>Web Content Server</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Product registration</ui> page, read the Microsoft Software License Terms, and, if applicable, click <ui>I have read, understood, and agree with the terms of the license agreement</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Installation location</ui> page, verify that sufficient free disk space is available, and then click <ui>Next</ui>. If necessary, click <ui>Browse</ui> to change the installation location of the web content server.</para>
          <alert class="note">
            <para>We recommend that you install the <token>smssp</token> in the default location. Installing the <token>smssp</token> in another location will require that you make configuration changes in Internet Information Services (IIS).</para>
          </alert>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>System check results</ui> page, make sure that the prerequisite check passed or at least passed with warnings, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure the Service Manager self-service portal name and port</ui> page, do the following:</para>
          <list class="ordered">
            <listItem>
              <para>In the <ui>Web site name</ui> text box, accept the default name, or type a new name.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Port</ui> text box, accept the default port, or type a new port.</para>
            </listItem>
            <listItem>
              <para>In the <ui>SSL certificate</ui> list, select the Secure Sockets Layer (SSL) certificate that you want to use with the <token>smssp</token>, and then click <ui>Next</ui>.</para>
            </listItem>
          </list>
          <alert class="note">
            <para>We strongly recommend the use of SSL. If you are using a self-signed certificate, make sure that the certification authority (CA) that issues the certificate has been added to the Trusted Root Certification Authorities store. You must use the same HTTP protocol (HTTP or HTTPS) with both portal parts.</para>
          </alert>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Select the Service Manager database</ui> page, do the following:</para>
          <list class="ordered">
            <listItem>
              <para>In the <ui>Database server</ui> text box, type the name of the computer that hosts the <token>smshort</token> database, and then press TAB.</para>
            </listItem>
            <listItem>
              <para>In the <ui>SQL Server instance</ui> list, select the instance name for the <token>smshort</token> database. (<ui>Default</ui> is the default selection.)</para>
            </listItem>
            <listItem>
              <para>In the <ui>Database</ui> list, select the database that hosts the <token>smshort</token> database. (<ui>ServiceManager</ui> is the default database name.)</para>
            </listItem>
            <listItem>
              <para>Click <ui>Next</ui>.</para>
            </listItem>
          </list>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure account for the Service Manager self-service portal</ui> page, click <ui>Domain account</ui>.</para>
          <alert class="note">
            <?Comment j: 223038 2011-08-26T13:41:00Z  Id='6?>
            <para>Make sure that the credentials you enter here are for the sdk_users users role on the SQL&nbsp;Server that is hosting the <token>smshort</token> database.<?CommentEnd Id='6'
    ?></para>
          </alert>
        </content>
      </step>
      <step>
        <content>
          <para>Specify the user name, password, and domain <?Comment JD: Per bug 155890 2011-05-20T10:45:00Z  Id='7?>for the <token>smshort</token> services account that you specified during installation of <token>smshort</token><?CommentEnd Id='7'
    ?>. For example, enter the account information for the SM_Acct domain user. </para>
        </content>
      </step>
      <step>
        <content>
          <para>Click <ui>Test Credentials</ui>. After you verify that you received a "The credentials were accepted message," click <ui>Next</ui>.</para>
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
          <para>On the <ui>Setup completed successfully</ui> page, we recommend that you leave <ui>Open the Encryption Backup or Restore Wizard</ui> selected, and then click <ui>Close</ui>. For more information about backing up the encryption key, see <link xlink:href="dbb276a9-7df5-4cd9-ae75-9099aabcaa93">Completing Deployment by Backing Up the Encryption Key</link>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics>
    <link xlink:href="55ed8428-80ea-4f78-a664-99ba573a8aac">How to Install SharePoint Web Parts for the Service Manager 2012 Self-Service Portal</link>
  </relatedTopics>
</developerHowToDocument>