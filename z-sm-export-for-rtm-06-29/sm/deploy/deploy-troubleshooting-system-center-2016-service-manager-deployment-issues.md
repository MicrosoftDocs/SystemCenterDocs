---
title: Troubleshooting System Center 2012 - Service Manager Deployment Issues
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4aee1627-a7c4-4299-847a-a5bfb87a4133
 

















---
# Troubleshooting System Center 2012 - Service Manager Deployment Issues
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>An installation log file is captured during the installation of <token>smlong12</token>. After <token>smshort</token> is running, various events are captured in the Windows Event Log. In addition, there are some Windows&nbsp;PowerShell commands that you can use to help troubleshoot data warehouse jobs. For more information, see "Troubleshoot Data Warehouse Jobs" in the <externalLink><linkText>Administrator's Guide for System Center 2012 - Service Manager</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=209669</linkUri></externalLink>.</para>
  </introduction>
  <section>
    <title>Installation Log Files</title>
    <content>
      <para>A log file, SCSMInstall.log, captures the progress of the installation. <?Comment TN: This paragraph has two subjects: &quot;Garret&quot; and &quot;you&quot;. Can you either make all the sentences refer to Garret, or make all the sentences refer to &quot;you&quot;?&lt;JDOWING&gt; Made it all about You. :) 2012-03-13T22:33:00Z  Id='1?>You can use this log file to troubleshoot a failed installation. You can find this log file in the %temp% folder. To troubleshoot installation problems, you can open the log files and search for a line that reads <ui>Return Value 3</ui>. If you find such a line in the log file, look above this line for any indication that a particular step failed.<?CommentEnd Id='1'
    ?></para>
    </content>
  </section>
  <section>
    <title>Event Logs</title>
    <content>
      <para>
        <token>smshort</token> event logs are located in Event Viewer, in the <ui>Application and Service Logs</ui> folder, in the <ui>Microsoft</ui> folder, and then listed as <ui>Operations Manager</ui>.</para>
    </content>
  </section>
  <section>
    <title>
      <?Comment j: 226610 2012-03-13T22:34:00Z  Id='2?>Create Database error<?CommentEnd Id='2'
    ?></title>
    <content>
      <para>During setup, when you were configuring Service Manager or data warehouse databases, you were given the opportunity to specify how much disk space to allocate for each database. The default setting is 2,000 megabytes (MB) (2&nbsp;gigabytes (GB)). In addition to the disk space that is required for the database,  <token>smshort</token> sets aside additional space for file groups and log files. The additional space that is required for the file groups and log files can be equal to the space that is required for the database. </para>
      <para>If there is insufficient disk space available, a message appears, indicating that an error occurred during execution of a custom action: _CreateDatabase. The installation stops before permanent changes are made. If you examine the <token>smshort</token> setup log, you find the following string:</para>
      <code>Additional Error Description : MODIFY FILE encountered operating system error 112(There is not enough space on the disk.) while attempting to expand the physical file</code>
      <para>You have to either increase the amount of free disk space that is available or reduce the amount of space that <token>smshort</token> allocates for the database, and then attempt the installation again. If you are installing <token>smshort</token> in a nonproduction environment, you can specify as little as 500&nbsp;MB for the database.</para>
    </content>
  </section>
  <section>
    <title>Troubleshooting deployment topics</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <link xlink:href="56b7f6c9-7960-4a6c-b933-0fe8ca0475d6">How to Troubleshoot a Data Warehouse Job</link>
          </para>
          <para>Describes how to troubleshoot data warehouse jobs.</para>
        </listItem>
      </list>
    </content>
  </section>
  <?Comment TN: DO NOT USE the related topics tag in this sort of parent node topic. Reserve itsuse only for topics that do not provide any navigation function. 2011-06-28T12:36:00Z  Id='3?>
  <relatedTopics>
    <?CommentEnd Id='3'
    ?>
  </relatedTopics>
</developerConceptualDocument>