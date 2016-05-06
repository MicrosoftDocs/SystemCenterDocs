---
title: IPAM Multi-Server Management
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 937c6d67-1a0b-4e45-bdff-180a4f0c49dc
---
# IPAM Multi-Server Management
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>IPAM enables you to monitor and manage multiple DHCP servers and monitor multiple DNS servers that are distributed across different regions from a centralized console. </para>
  </introduction>
  <section>
    <title>Multiserver management and display</title>
    <content>
      <para>Administrative tasks are frequently repetitive across multiple servers, and the ability to run these tasks uniformly across servers reduces the effort involved and the probability of error. The IPAM multiserver management (MSM) feature enables you to easily edit and configure key properties of multiple DHCP servers and scopes across the organization. IPAM also enables tagging servers with built-in and user-defined custom field values to visualize these servers and group them into logical groups and subgroups.</para>
    </content>
  </section>
  <section>
    <title>Service and zone monitoring</title>
    <content>
      <para>IPAM facilitates monitoring and tracking of DHCP and DNS service status on the network. With IPAM, you can monitor hundreds of DNS and DHCP servers allocated across multiple regions from a centralized console.</para>
      <para>IPAM service monitoring includes regular verification that the DNS or DHCP service is running, stopped, or paused on a managed server, and that there is proper network connectivity. Along with DHCP and DNS service status, IPAM allows monitoring of all DHCP scopes from a central console. The status of a scope as active or inactive is displayed. Utilization percentage for a scope is displayed with a current utilization status of: Over, Under, or Optimal.</para>
      <para>You can also monitor the “health” of a DNS zone on multiple DNS servers by viewing the zone status per server, and by displaying the aggregated status of a zone across all authoritative DNS servers.</para>
      <para>DNS zone monitoring includes the following:</para>
      <list class="bullet">
        <listItem>
          <para>Forward lookup zones: IPAM displays a list of all forward lookup zones that are hosted by managed DNS servers. The overall status of each zone is provided, based on the status of the zone on each authoritative server, and the state of the authoritative server.</para>
        </listItem>
        <listItem>
          <para>IPv4 reverse lookup zones: IPAM displays all IPv4 reverse lookup zones that are hosted by managed DNS servers. A list of all authoritative servers that are hosting the selected reverse lookup zone is displayed.</para>
        </listItem>
        <listItem>
          <para>IPv6 reverse lookup zones: IPAM displays all IPv6 reverse lookup zones that are hosted by managed DNS servers. A list of all authoritative servers that are hosting the selected reverse lookup zone is displayed.</para>
        </listItem>
      </list>
      <para>IPAM displays a list of all authoritative servers for a zone in the preview pane along with zone type, zone health status, and duration of the current status. </para>
      <para>Some of the key attributes that are monitored include:</para>
      <list class="bullet">
        <listItem>
          <para>Server availability state: State of the DNS service on a server.</para>
        </listItem>
        <listItem>
          <para>Zone status: State of the zone on a server.</para>
        </listItem>
        <listItem>
          <para>Zone status for all servers: Aggregate status of the zone across all authoritative servers.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section>
    <title>Configuration monitoring</title>
    <content>
      <para>IPAM displays server operational events for managed DHCP servers, DNS servers, and for the IPAM server. IPAM enables you to view event logs, perform searches based on multiple fields, and export information to a file. You can also save queries and modify or reuse them later. Configuration change events include the following details:</para>
      <list class="ordered">
        <listItem>
          <para>Event ID</para>
        </listItem>
        <listItem>
          <para>Event description</para>
        </listItem>
        <listItem>
          <para>Event time</para>
        </listItem>
        <listItem>
          <para>Server name</para>
        </listItem>
        <listItem>
          <para>Domain and user name for the user who is running the configuration event</para>
        </listItem>
      </list>
      <para>Additional fields are available for IPAM server configuration events, including task category, opcode, and keywords. IPAM also provides advanced query constructs within the event description field, which enables you to filter for other information such as Network ID, IP address, group name, or custom field name.</para>
    </content>
  </section>
  <section>
    <title>Server and scope management</title>
    <content>
      <para>The IPAM MSM feature enables you to view and easily configure the key properties of multiple DHCP servers across the organization. Tasks that are frequently repetitive, such as altering a scope option setting on multiple DHCP scopes, can be performed uniformly across multiple servers. This reduces the effort required and the probability of error.</para>
      <para>The following noncontextual are available from the Tasks menu:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Retrieve Server Data</embeddedLabel>: Trigger background tasks to retrieve and update information such as service status, DHCP server and scope configuration, and DNS zone status.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Export</embeddedLabel>: Export records from the current IPAM view into a file of comma-separated values. If you have applied any filters in the view, only filtered records will be exported.</para>
        </listItem>
      </list>
    </content>
    <sections>
      <section>
        <title>DHCP server management actions</title>
        <content>
          <para>The following actions are available for DHCP servers:</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Edit DHCP Server Properties</embeddedLabel>: Configure the server properties of a DHCP server.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Edit DHCP Server Options</embeddedLabel>: Enables adding, deleting, editing, and find-and-replace operations on options at the server level. This action can be performed on multiple DHCP servers simultaneously.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Create DHCP Scope</embeddedLabel>: Create a scope on a DHCP server, and configure multiple scope properties.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Configure Predefined DHCP Options</embeddedLabel>: Add, edit, or delete predefined options. This action can be performed on multiple DHCP servers simultaneously.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Configure User Class</embeddedLabel>: Create, overwrite, or delete User Classes. This action can be performed on multiple DHCP servers simultaneously.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Configure Vendor Class</embeddedLabel>: Create, overwrite, or delete Vendor Classes. This action can be performed on multiple DHCP servers simultaneously.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Launch MMC</embeddedLabel>: Open a DHCP console window for the selected DHCP server.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Retrieve Server Data</embeddedLabel>: Retrieve current data on-demand from the DHCP server. This action can be performed on multiple DHCP servers simultaneously.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>DNS server management actions</title>
        <content>
          <para>The following actions are available for DNS servers:</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Launch MMC</embeddedLabel>: Open a DNS Manager window for the selected DHCP server.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Retrieve Server Data</embeddedLabel>: Retrieve current data on-demand from the DNS server. This action can be performed on multiple DNS servers simultaneously.</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>DHCP scope management actions</title>
        <content>
          <para>The following actions are available for DHCP scopes:</para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Edit DHCP Scopes</embeddedLabel>: Edit lease duration, exclusion ranges, DNS dynamic updates, and scope options. Scope editing includes adding, deleting, editing, and find-and-replace operations. Actions can be performed on one scope or on multiple scopes simultaneously.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Duplicate DHCP Scope</embeddedLabel>: Create a new scope, and configure it with the same properties as the selected scope.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Activate DHCP Scope</embeddedLabel>: Activate one or more scopes.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Deactivate DHCP Scope</embeddedLabel>: Deactivate one or more scopes.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>Delete</embeddedLabel>: Delete one or more scopes.</para>
            </listItem>
          </list>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>See also</title>
    <content>
      <para>
        <legacyLink xlink:href="9035778c-7ab3-42d0-8540-45a163c1d46b">IP Address Management Overview</legacyLink>
      </para>
      <para>
        <legacyLink xlink:href="70586e67-3d2c-48f7-a196-92f76f2e77f9">Multi-server Management</legacyLink>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>