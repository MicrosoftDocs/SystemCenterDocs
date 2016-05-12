---
title: Copy a Clustered Role to Another Cluster
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34e052dd-ec68-4759-a861-325d29395300
---
# Copy a Clustered Role to Another Cluster
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can use the Copy Cluster Roles Wizard to copy clustered roles from a failover cluster that is running <token>winblue_server_Token>, <token>win8_server_Token>, or <token>nextref_server_Token>.</para>
    <para>To copy clustered roles, you must be a local administrator on both the cluster node from which you want to copy clustered roles, and the node in the other cluster to which you want to copy the roles.</para>
    <para>Realize that although role settings are copied, cluster settings, network settings, and data files that are used by the role are not copied. Also, for virtual machines, it assumes that storage is reused.</para>
  </introduction>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <externalLink>
              <linkText>Migrate Clustered Roles to Windows Server 2012 R2</linkText>
              <linkUri>http://go.microsoft.com/fwlink/?LinkId=329936</linkUri>
            </externalLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

