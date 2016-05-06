---
title: IPAM IP Address Tracking
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce39b1fa-56db-46ff-8dd0-ea480331ac99
---
# IPAM IP Address Tracking
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The IPAM IP address tracking feature enables you to track IP address activity on the network, and correlate activity with MAC addresses, DUIDs, user names, host names, and other parameters. Information is collected from logs on servers that are managed by IPAM and made available to aid forensics investigations.</para>
  </introduction>
  <section>
    <title>IP address information</title>
    <content>
      <para>Information collected that enables history tracking for IP address leases and user logins includes:</para>
      <list class="bullet">
        <listItem>
          <para>IP addresses, client identifiers, and host names are collected from lease logs on managed DHCP servers</para>
        </listItem>
        <listItem>
          <para>User names and IP addresses are collected from logon events on managed domain controllers.</para>
        </listItem>
        <listItem>
          <para>User names and client identifiers are collected from logon events on managed network policy servers.</para>
        </listItem>
      </list>
      <para>An administrator can search logs and correlate IP address activity based on IP address, client identifier, host name, or user name. DHCP lease logs from DHCP servers and user logon events on domain controllers and network policy servers (NPS) provide information to IPAM that can be used to maintain a historical trail of IP address lease events, and help track users and computers on the network. IPAM administrators can select search criteria and specify a query time interval to correlate user and device activity for the specified time. </para>
      <para>The following are some basic example of queries for using a specified start and end time.</para>
      <list class="bullet">
        <listItem>
          <para>Query 1: Find all DHCP lease events that match a specified IP address, client ID, or host name.</para>
        </listItem>
        <listItem>
          <para>Query 2: Correlate network authentication events with the start and end times for events in query 1.</para>
        </listItem>
        <listItem>
          <para>Query 3: Display all logon events that match a specified user name with correlated DHCP lease events.</para>
        </listItem>
      </list>
      <para>IPAM enables purging IP address tracking data from the IPAM database. You can also trigger an on-demand refresh of IP address tracking information from the Tasks menu when you are using the Event Catalog view.</para>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <para>
        <legacyLink xlink:href="f08b3adc-42e2-439e-9941-e719b9f6ef2e">Understanding IP Address Tracking</legacyLink>
      </para>
      <para>
        <legacyLink xlink:href="9035778c-7ab3-42d0-8540-45a163c1d46b">IP Address Management Overview</legacyLink>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>