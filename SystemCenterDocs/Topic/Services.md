---
title: Services
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a032480-38d4-4845-a2ab-fafa13ea7721
---
# Services
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can use the Services Microsoft Management Console (MMC) snap-in to manage services that are running on local or remote computers — for example, to stop or start a service. You can also manage services using the <system>sc config</system> command.</para>
  </introduction>
  <section>
    <title>What is a service?</title>
    <content>
      <para>A service is an application type that runs in the system background without a user interface and is similar to a UNIX daemon process. Services provide core operating system features, such as Web serving, event logging, file serving, printing, cryptography, and error reporting.</para>
    </content>
  </section>
  <section>
    <title>What can I do with the Services snap-in?</title>
    <content>
      <para>You can perform the following actions for services on local and remote computers:</para>
      <list class="bullet">
        <listItem>
          <para>Start, stop, pause, resume, or disable services.</para>
        </listItem>
        <listItem>
          <para>Set up recovery actions to take place if a service fails — for example, restarting the service automatically or restarting the computer.</para>
        </listItem>
        <listItem>
          <para>Run services in the security context of a user account that is different from the logged-on user or the default computer account.</para>
        </listItem>
        <listItem>
          <para>Enable or disable services for a particular hardware profile.</para>
        </listItem>
        <listItem>
          <para>Export and save service information to a .txt or .csv file.</para>
        </listItem>
        <listItem>
          <para>View the status and description of each service.</para>
        </listItem>
        <listItem>
          <para>View the service dependencies.</para>
        </listItem>
      </list>
      <para>For more information about using the Services snap-in, see <externalLink><linkText>Services</linkText><linkUri>http://technet.microsoft.com/library/cc772408.aspx</linkUri></externalLink></para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>