---
title: File Server Resource Manager Overview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dffba8a6-f9a8-4692-b043-63effb043ea3
---
# File Server Resource Manager Overview
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction address="BKMK_INTRO">
    <para>This topic describes the File Server Resource Manager features that are included with the File and Storage Services server role.</para>
  </introduction>
  <section address="BKMK_OVER">
    <title>Feature descriptions</title>
    <content>
      <para>File Server Resource Manager is a set of features that enables you to manage and classify data that is stored on file servers. File Server Resource Manager includes the following features:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>File Classification Infrastructure</embeddedLabel>   File Classification Infrastructure provides insight into your data by automating classification processes so that you can manage your data more effectively. You can classify files and apply policies based on this classification. Example policies include dynamic access control for restricting access to files, file encryption, and file expiration. Files can be classified automatically by using file classification rules or manually by modifying the properties of a selected file or folder.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>File Management Tasks</embeddedLabel>   File Management Tasks enables you to apply a conditional policy or action to files based on their classification. The conditions of a file management task include the file location, the classification properties, the date the file was created, the last modified date of the file, or the last time the file was accessed. The actions that a file management task can take include the ability to expire files, encrypt files, or run a custom command.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Quota management</embeddedLabel>   Quotas allow you to limit the space that is allowed for a volume or folder, and they can be automatically applied to new folders that are created on a volume. You can also define quota templates that can be applied to new volumes or folders.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>File screening management</embeddedLabel>   File screens help you control the types of files that user can store on a file server. You can limit the extension that can be stored on your shared files. For example, you can create a file screen that does not allow files with an MP3 extension to be stored in personal shared folders on a file server. </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Storage reports</embeddedLabel>   Storage reports are used to help you identify trends in disk usage and how your data is classified. You can also monitor a selected group of users for attempts to save unauthorized files.</para>
        </listItem>
      </list>
      <para>The features included with File Server Resource Manager can be configured and managed by using the File Server Resource Manager Microsoft Management Console (MMC) or by using Windows PowerShell.</para>
      <alert class="important">
        <para>File Server Resource Manager supports volumes formatted with the NTFS file system only. The Resilient File System is not supported.</para>
      </alert>
    </content>
  </section>
  <section address="BKMK_APP" expanded="true">
    <title>Practical applications</title>
    <content>
      <para>Some practical applications for File Server Resource Manager include:</para>
      <list class="bullet">
        <listItem>
          <para>Use File Classification Infrastructure with the Dynamic Access Control scenario to create a policy that grants access to files and folders based on the way files are classified on the file server.</para>
        </listItem>
        <listItem>
          <para>Create a file classification rule that tags any file that contains at least 10 social security numbers as having personally identifiable information.</para>
        </listItem>
        <listItem>
          <para>Expire any file that has not been modified in the last 10 years.</para>
        </listItem>
        <listItem>
          <para>Create a 200 megabyte quota for each user’s home directory and notify them when they are using 180 megabytes.</para>
        </listItem>
        <listItem>
          <para>Do not allow any music files to be stored in personal shared folders.</para>
        </listItem>
        <listItem>
          <para>Schedule a report that runs every Sunday night at midnight that generates a list of the most recently accessed files from the previous two days. This can help you determine the weekend storage activity and plan your server downtime accordingly.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_LINKS" expanded="true">
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Dynamic Access Control Scenario Overview</linkText>
              <linkUri>http://technet.microsoft.com/library/hh831717.aspx</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

