---
title: Scale-Out File Server for Application Data Overview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff59aea7-e0d0-4cad-9c4f-44f6db1c4573
---
# Scale-Out File Server for Application Data Overview
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>When you deploy a highly available file server, you can select either of the following file server types:</para>
    <list class="bullet">
      <listItem>
        <para>
          <embeddedLabel>Scale-Out File Server for application data (Scale-Out File Server)</embeddedLabel>   This type of clustered file server enables you to store server application data, such as Hyper-V virtual machine files, on file shares, and obtain a similar level of reliability, availability, manageability, and high performance that you would expect from a storage area network. All file shares are online on all nodes simultaneously. File shares associated with this type of clustered file server are called scale-out file shares. This is sometimes referred to as active-active.</para>
      </listItem>
      <listItem>
        <para>
          <embeddedLabel>File Server for general use</embeddedLabel>   This is the continuation of the clustered file server that has been supported in Windows Server since the introduction of Failover Clustering. This type of clustered file server, and thus all the shares associated with the clustered file server, is online on one node at a time. This is sometimes referred to as active-passive or dual-active. File shares associated with this type of clustered file server are called clustered file shares.</para>
      </listItem>
    </list>
  </introduction>
  <section>
    <title>When to use Scale-Out File Server</title>
    <content>
      <para>You should use a Scale-Out File Server if you are interested in the scalability and simplicity that it offers and you only require technologies that are supported with Scale-Out File Server. Scale-Out File Servers are ideal for server applications that keep files open for a long amount of time, doing mostly data operations with infrequent metadata operations on the file system. Hyper-V virtual hard disks and SQL Server database files can be stored on a scale-out file share.</para>
      <para>You should not use a Scale-Out File Server if your workload generates a high number of metadata operations, such as opening files, closing files, creating new files, or renaming existing files. A typical information worker would generate a lot of metadata operations. </para>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="0a6029b2-9390-414f-b486-98d31d033ff0">Scale-Out File Server for Application Data Overview [ScaleOut_FS]</legacyLink>
          </para>
        </listItem>
      </list>
      <para />
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>