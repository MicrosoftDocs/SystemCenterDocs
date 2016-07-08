---
title: How to Install Both the Web Content Server and SharePoint Web Parts on One Computer
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54910c9a-b8d5-4413-832d-7bad2262c3a0
author: cfreemanwa
robots: noindex,nofollow


















---
# How to Install Both the Web Content Server and SharePoint Web Parts on One Computer
<?xml version="1.0" encoding="utf-8"?>
<developerHowToDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>
      <?Comment j: 226426 2011-10-07T17:00:00Z  Id='0?>When you are installing the web content server and SharePoint Web Parts on the same computer in <token>smlong12</token>, you must install both components at the same time. After one component has been installed, you will not be able to run Setup again to install the other component.<?CommentEnd Id='0'
    ?></para>
    <para>Use the following procedure to install both the web content server and SharePoint Web Parts for the <token>smssp</token> on the third computer.</para>
  </introduction>
  <procedure>
    <title>To install the Self-Service Portal on one computer</title>
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
          <para>On the <ui>Microsoft System Center Service Manager Setup Wizard</ui> page, click <ui>Service Manager Web portal</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Portal Parts</ui> page, click <ui>Web Content Server</ui>, click <ui>SharePoint Web Parts</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Product registration</ui>  page, read the Microsoft Software License Terms, and, if applicable, click <ui>I have read, understood, and agree with the terms of the license terms</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Installation location</ui> page, verify that sufficient free disk space is available, and then click <ui>Next</ui>. If necessary, click <ui>Browse</ui> to change the installation location of the <token>smshort</token> management server.</para>
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
          <para>On the <ui>Configure the Service Manager Self-Service Portal name and port</ui> page, do the following:</para>
          <list class="ordered">
            <listItem>
              <para>In the <ui>Website name</ui> text box, accept the default name, or type a new name.</para>
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
              <para>In the <ui>SQL Server instance</ui> list, select the instance name for the <token>smshort</token> database. (<ui>Default</ui> is the default SQL Server instance.)</para>
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
          <para>On the <ui>Configure the account for the Service Manager Self-Service Portal</ui> page, click <ui>Domain account</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>Specify the user name, password, and domain <?Comment JD: Per bug 155890 2011-05-26T09:37:00Z  Id='2?>for the <token>smshort</token> services account that you specified during installation of <token>smshort</token><?CommentEnd Id='2'
    ?>. For example, enter the account information for the SM_Acct domain user. </para>
        </content>
      </step>
      <step>
        <content>
          <para>Click <ui>Test Credentials</ui>. After you verify that you received a “The credentials were accepted” message, click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure the Service Manager SharePoint Web site</ui> page, do the following:</para>
          <list class="ordered">
            <listItem>
              <para>In the <ui>Web site name</ui> text box, accept the default name, or type a new name.</para>
            </listItem>
            <listItem>
              <para>In the <ui>SSL certificate</ui> list, select the SSL certificate that you want to use with the <token>smssp</token>.</para>
            </listItem>
            <listItem>
              <para>In the <ui>Port</ui> text box, accept the default port, or type a new port.</para>
              <alert class="note">
                <para>This is the port number that will be used for accessing the <token>smssp</token>.</para>
              </alert>
            </listItem>
            <listItem>
              <para>In the <ui>Database server</ui> text box, type the name of the computer that hosts the SharePoint database, and then press TAB. For example, select the default entry for the computer on which you are installing the SharePoint website.</para>
            </listItem>
            <listItem>
              <para>In the <ui>SQL Server instance</ui> list, select the instance name for the SharePoint database. (<ui>Default</ui> is the default SQL Server instance.)</para>
            </listItem>
            <listItem>
              <para>In the <ui>Database name</ui> text box, accept the default database name, or type a new name</para>
            </listItem>
            <listItem>
              <para>Click <ui>Next</ui>.</para>
            </listItem>
          </list>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Configure the account for Service Manager SharePoint application pool</ui> page, type a domain user and password, and then click <ui>Test Credentials</ui>. After you verify that you received a “The credentials were accepted” message, click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Help improve System Center Service Manager</ui> page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click <ui>Tell me more about the program</ui>, and then click <ui>Next</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Installation summary</ui> page, click <ui>Install</ui>.</para>
        </content>
      </step>
      <step>
        <content>
          <para>On the <ui>Setup completed successfully</ui> page, click the link to test the URL for the <token>smssp</token>. Make a note of this URL, and then click <ui>Close</ui>.</para>
        </content>
      </step>
    </steps>
  </procedure>
  <relatedTopics />
</developerHowToDocument>