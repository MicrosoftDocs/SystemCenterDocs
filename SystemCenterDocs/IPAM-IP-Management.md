---
title: IPAM IP Management
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1737e23-2ade-4f3e-acf1-45740b853d55
---
# IPAM IP Management
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The IPAM address space management (ASM) feature provides the ability to efficiently view, monitor, and manage IP address space on the network. The ASM feature supports IPv4 public and private address space, and IPv6 address space. You can manage dynamic IP addresses and static IP addresses on the network using IPAM ASM. </para>
    <para>The ASM feature addresses IP address space management problems in a growing distributed environment by ensuring better planning and control. IPAM also enables you to easily perform several essential administrative actions, including: detect overlapping IP address ranges that are defined on different DHCP servers, find available IP addresses within a range, create DHCP reservations, and create DNS records. IPAM ASM enables IPv4 and IPv6 address space planning, allocation, and inventory management.</para>
    <para>Features of IPAM ASM include:</para>
    <list class="bullet">
      <listItem>
        <para>IP address space utilization statistics and trend monitoring</para>
      </listItem>
      <listItem>
        <para>Support for import and export of IP address space in comma-separated-value format</para>
      </listItem>
      <listItem>
        <para>Organizing and visualizing of address space data into custom-defined hierarchical logical groups</para>
      </listItem>
      <listItem>
        <para>Identification and reservation of available IP addresses</para>
      </listItem>
      <listItem>
        <para>Expiry assignment and notification for IP addresses</para>
      </listItem>
      <listItem>
        <para>Advanced search and filter functions</para>
      </listItem>
    </list>
  </introduction>
  <section>
    <title>Organizing IP address space</title>
    <content>
      <para>IPAM helps to organize IP address space on your network by providing a highly customizable, hierarchical display. A network administrator can also display utilization trends, track IP address utilization and view threshold-crossing status for specific IP address ranges.</para>
      <para>By default, IPAM allocates IP address space into IP address blocks, IP address ranges, and individual IP addresses.</para>
      <para>IP address blocks are large chunks of IP addresses that are used to organize address space at a high level. IP address ranges are smaller chunks of IP addresses that typically correspond to a DHCP scope. Individual IP addresses correspond to hosts or devices on the network.</para>
      <para>IPAM displays IP address blocks in a multilevel hierarchy of superblocks and sub-blocks, if applicable. When you add an IP address range to IPAM, it is automatically mapped to the appropriate IP address block. Similarly, individual IP addresses are mapped to IP address ranges. If duplicate IP addresses or ranges exist, these can be identified using unique service and service instance fields.</para>
    </content>
    <sections>
      <section>
        <title>Customizing IP address space display</title>
        <content>
          <para>IPAM enables highly customizable sorting and display of IP address space. The display can be based on custom fields, such as region, Regional Internet Registries (RIR), device type, or customer name. IPAM enables you to add new free-format or multivalued custom fields or to extend built-in multivalued custom fields. Custom fields can be used to tag IPAM objects, and enables real-world logical groups to be defined using a multilevel hierarchy of custom fields. With IPAM, you can organize and visualize IP address space using logical groups, depending on your business need. For example, you might organize and view IP address ranges based on geographical location or business unit. To achieve this, you can create a logical group based on country or business unit, and then apply the country or business unit field to the IP address ranges. This enables you to view the IP address ranges that are used by a particular business unit or are in a country by simply clicking the appropriate logical group. </para>
          <para>You can also track utilization data that is rolled up at the logical group level, based on IP address ranges. Multiple IP range groups can be created simultaneously. IPAM also contains a built-in logical range group, which is called the Managed By group. This group is organized by Managed by Service and Service Instance values of the range.</para>
          <para>IPAM enables organizing of IP address space using a built-in logical group that is organized by default using device type and called the IP Address Inventory group. IP address inventory data can be imported, exported, and modified to maintain a database of IP addresses.</para>
        </content>
      </section>
      <section>
        <title>Address space operations</title>
        <content>
          <para>IPAM ASM provides the following IP address space operations.</para>
        </content>
        <sections>
          <section>
            <title>Non-contextual operations</title>
            <content>
              <para>The following non-contextual operations are available from the Tasks menu in address space or by right-clicking nodes in left navigation pane.</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Add IP Address Block</embeddedLabel>: Create a new IP address block and add basic configuration information.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Add IP Address Range</embeddedLabel>: Create a new IP address range and add basic and custom configuration information.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Add IP Address</embeddedLabel>: Create a new IP address and add basic, custom, DHCP reservation and DNS record related information associated with the address.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Import IP Address Blocks</embeddedLabel>: Select a file of comma-separated values that contain IP address block records, and then import these records from the file into IPAM. New addresses are added and existing addresses are updated in the IPAM database.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Import IP Address Ranges</embeddedLabel>: Select a file of comma-separated values that contain IP address range records, and then import these records from the file into IPAM. New IP address ranges are added and existing addresses are updated in the IPAM database.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Import IP Addresses</embeddedLabel>: Select a file of comma-separated values that contain IP address records, and then import these records from the file into IPAM. New IP addresses are added and existing addresses are updated in the IPAM database.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Import and Update IP Address Ranges</embeddedLabel>: Select a file of comma-separated values that contain IP address records, and then import these records from the file into IPAM. New IP address ranges are added and existing addresses are updated in the IPAM database. If a record exists in IPAM with the same Managed By Service and Service Instance values, but the record is not present in the file, it will be deleted.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>IP Address Expiry Log Settings</embeddedLabel>: Set the number of days before expiry that an IP address should be transitioned to a state of Expiry Due. You can also select whether to generate period expiry events or generate expiry events only on state transitions.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Retrieve Address Space Data</embeddedLabel>: Trigger background tasks to retrieve and update address space information such as utilization and expiry.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Export</embeddedLabel>: Export records from the current IPAM view into a file of comma-separated values. If you have applied any filters in the view, only filtered records will be exported.</para>
                </listItem>
              </list>
            </content>
          </section>
          <section>
            <title>IP address block operations</title>
            <content>
              <para>The following are the right-click contextual operations that are available on IP address blocks:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Add IP Address Block</embeddedLabel>: Provides a dialog with the properties of the currently selected IP address block, enabling allocation of a new sub-block under the existing parent IP address block.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Edit IP Address Block</embeddedLabel>: Edit the selected IP address block and update basic information that is associated with the block.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete</embeddedLabel>: Delete the selected IP address block, and prompt for confirmation if the selected blocks have sub-blocks that also must to be deleted.</para>
                </listItem>
              </list>
            </content>
          </section>
          <section>
            <title>IP address range operations</title>
            <content>
              <para>The following are the right-click contextual operations that are available for IP address ranges:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Edit IP Address Range</embeddedLabel>: Edit the selected IP address range to update basic and custom information for the range.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Import and Update IP Addresses</embeddedLabel>: Select a file of comma-separated values that contain a snapshot of all the IP addresses in the selected IP address range, and then import the records into IPAM. New addresses are added, existing address are modified, and missing addresses are deleted from IPAM to synchronize the existing database with the new data that is being imported.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Find and Allocate Available IP Address</embeddedLabel>: Find an available IP address from the selected range, confirm the availability status of the IP address using ping and DNS, and create new IP address record in IPAM.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Map to IP Address Block</embeddedLabel>: Map an IP address range by exchanging an existing overlapping range.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Reclaim IP Addresses</embeddedLabel>: Reclaim IP address records that have expired.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Retrieve Address Space Data</embeddedLabel>: Trigger background tasks to update address space information, such as utilization data.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete</embeddedLabel>: Delete the selected IP address range and prompt for confirmation if the selected range has IP addresses that also must be deleted.</para>
                </listItem>
              </list>
            </content>
          </section>
          <section>
            <title>IP address operations</title>
            <content>
              <para>The following are right-click contextual operations on IP addresses:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Edit IP Address</embeddedLabel>: Edit the selected IP address record to update basic, custom, DHCP reservation and DNS record related information.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Create DHCP Reservation</embeddedLabel>: Create a DHCP reservation for the selected IP address record. You must edit the IP address record and provide DHCP reservation information before you attempt this operation.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Create DNS Host Record</embeddedLabel>: Creates a DNS host (A/AAAA) record for the selected IP address record. You must edit the IP address record and provide DNS record information before you attempt this operation.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Create DNS PTR Record</embeddedLabel>: Create a DNS PTR record for the selected IP address record. You must edit the IP address record and provide DNS record information before you attempt this operation.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete DHCP Reservation</embeddedLabel>: Delete an existing DHCP reservation for the selected IP address.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete DNS Host Record</embeddedLabel>: Delete an existing DNS host (A/AAAA) record for the selected IP address.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete DNS PTR Record</embeddedLabel>: Delete an existing DNS PTR record for the selected IP address.</para>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Delete</embeddedLabel>: Delete the selected IP address record from IPAM.</para>
                </listItem>
              </list>
            </content>
          </section>
        </sections>
      </section>
    </sections>
  </section>
  <section>
    <title>See also</title>
    <content>
      <para>
        <legacyLink xlink:href="0944b8c9-09b6-47a6-9a67-87c4e816a3fc">Managing IP Address Space [ops]</legacyLink>
      </para>
      <para>
        <legacyLink xlink:href="9035778c-7ab3-42d0-8540-45a163c1d46b">IP Address Management Overview</legacyLink>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

