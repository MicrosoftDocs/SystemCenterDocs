---
title: IPAM Role Based Access Control
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64a64cb8-2f51-44b2-8ad2-589127463cbf
---
# IPAM Role Based Access Control
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic provides a summary of role based access control for IP Address Management (IPAM), a new feature available in <token>winblue_server_./Token>. </para>
    <para>For examples and information about how role based access control works, see <legacyLink xlink:href="be6071c5-0c8d-4362-93bc-cf715a128cc3">Walkthrough: Demonstrate IPAM in Windows Server 2012 R2</legacyLink>.</para>
  </introduction>
  <section address="RBAC">
    <title>Role based access control</title>
    <content>
      <para>Role based access control provides you with the ability to customize roles, access scopes, and access policies. Thus, you have the ability to define and establish fine-grained control for users and groups, enabling them to perform a specific set of administrative operations on specific objects managed by IPAM.</para>
      <para>
        <embeddedLabel>Roles</embeddedLabel>: A role is a collection of IPAM operations. You can associate a role with a user or group in Windows using an access policy. Eight built-in administrator roles are provided for convenience, but you can also create customized roles to meet your business requirements. </para>
      <para>
        <embeddedLabel>Access scopes</embeddedLabel>: An access scope determines the objects that a user has access to. You can use access scopes to define administrative domains in IPAM. For example, you might create access scopes based on geographical location. By default, IPAM includes an access scope of Global. All other access scopes are subsets of the Global access scope. Users or groups that are assigned to the Global access scope have access to all objects in IPAM that are permitted by their assigned role. </para>
      <para>
        <embeddedLabel>Access Policies</embeddedLabel>: An access policy combines a role with an access scope to assign permission to a user or group. For example, you might define an access policy for a user with a role of IP Block Admin and an access scope of Global\Asia. Therefore, this user will have permission to edit and delete IP address blocks that are associated to the Asia access scope. This user will not have permission to edit or delete any other IP address blocks in IPAM.</para>
      <para>The following default access scope and roles are provided:</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Type</para>
            </TD>
            <TD>
              <para>Name</para>
            </TD>
            <TD>
              <para>Description</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>DNS record administrator</para>
            </TD>
            <TD>
              <para>Manages DNS resource records</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IP address record administrator</para>
            </TD>
            <TD>
              <para>Manages IP addresses but not IP address spaces, ranges, blocks, or subnets.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM administrator</para>
            </TD>
            <TD>
              <para>Manages all settings and objects in IPAM</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM ASM administrator</para>
            </TD>
            <TD>
              <para>Completely manages IP addresses</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM DHCP administrator</para>
            </TD>
            <TD>
              <para>Completely manages DHCP servers</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM DHCP reservations administrator</para>
            </TD>
            <TD>
              <para>Manages DHCP reservations</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM DHCP scope administrator</para>
            </TD>
            <TD>
              <para>Manages DHCP scopes</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Role</para>
            </TD>
            <TD>
              <para>IPAM MSM administrator</para>
            </TD>
            <TD>
              <para>Completely manages DHCP and DNS servers</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Access scope</para>
            </TD>
            <TD>
              <para>Global</para>
            </TD>
            <TD>
              <para>By default, all objects in IPAM are included in the global access scope. All additional scopes that are configured are subsets of the global access scope.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <para>
        <legacyLink xlink:href="0e27c024-36f7-4a36-8987-5590f13a45e2">IP Address Management (IPAM) Overview</legacyLink>
      </para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

