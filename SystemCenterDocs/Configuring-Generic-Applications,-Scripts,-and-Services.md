---
title: Configuring Generic Applications, Scripts, and Services
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a421f9cd-434a-447b-8734-d2e62c6dc467
---
# Configuring Generic Applications, Scripts, and Services
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can use the Generic Application, Generic Script, and Generic Service options to configure high availability for some services and applications that are not "cluster-aware" (not originally designed to run in a cluster). In general, the failover cluster does not detect the state of a generic application, generic script, or generic service with the same precision that it can monitor a cluster-aware role.</para>
    <para>The following table provides basic information about these generic roles.</para>
    <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
      <thead>
        <tr>
          <TD>
            <para>Role</para>
          </TD>
          <TD>
            <para>Description</para>
          </TD>
        </tr>
      </thead>
      <tbody>
        <tr>
          <TD>
            <para>Generic Application</para>
          </TD>
          <TD>
            <para>The cluster software starts the application, and then periodically queries the operating system to see whether the application appears to be running. If so, it is presumed to be online, and it is not restarted or failed over. You must specify the path for the application and any registry keys that the application requires (so that the registry keys can be replicated to all nodes in the cluster).</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>Generic Script</para>
          </TD>
          <TD>
            <para>You create a script that runs in Windows Script Host, which monitors and controls an application. The ability of the cluster software to respond to the state of the application is determined by the script. As needed, the cluster software restarts or fails over the script (and through it, the application).</para>
          </TD>
        </tr>
        <tr>
          <TD>
            <para>Generic Service</para>
          </TD>
          <TD>
            <para>The cluster software starts the service, and then periodically queries the Service Controller to determine whether the service appears to be running. If so, it is presumed to be online, and it is not restarted or failed over.</para>
          </TD>
        </tr>
      </tbody>
    </table>
  </introduction>
  <relatedTopics />
</developerConceptualDocument>