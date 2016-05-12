---
title: Desktop Experience
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36c98a41-36fe-4c1d-8582-3d7709be0882
---
# Desktop Experience
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The Desktop Experience feature allows you to install a variety of applications and features that are not normally installed on a server. . If you are running <token>win8_server_Token>, the following <token>win8_client_Token> features are installed when you install Desktop Experience:</para>
    <list class="bullet">
      <listItem>
        <para>Windows Media Player</para>
      </listItem>
      <listItem>
        <para>Video for Windows (AVI support)</para>
      </listItem>
      <listItem>
        <para>Windows SideShow</para>
      </listItem>
      <listItem>
        <para>Disk Cleanup</para>
      </listItem>
      <listItem>
        <para>Sync Center</para>
      </listItem>
      <listItem>
        <para>Sound Recorder</para>
      </listItem>
      <listItem>
        <para>Character Map</para>
      </listItem>
      <listItem>
        <para>Snipping Tool</para>
      </listItem>
      <listItem>
        <para>Support for desktop apps</para>
      </listItem>
      <listItem>
        <para>Windows Store</para>
      </listItem>
    </list>
    <para>If you are running <token>winblue_server_Token>, the following <token>winblue_client_Token> features are installed when you install Desktop Experience:</para>
    <list class="bullet">
      <listItem>
        <para>Windows Media Player</para>
      </listItem>
      <listItem>
        <para>Video for Windows (AVI support)</para>
      </listItem>
      <listItem>
        <para>Windows SideShow</para>
      </listItem>
      <listItem>
        <para>Disk Cleanup</para>
      </listItem>
      <listItem>
        <para>Sync Center</para>
      </listItem>
      <listItem>
        <para>Sound Recorder</para>
      </listItem>
      <listItem>
        <para>Character Map</para>
      </listItem>
      <listItem>
        <para>Snipping Tool</para>
      </listItem>
      <listItem>
        <para>Support for desktop apps</para>
      </listItem>
      <listItem>
        <para>Windows Store</para>
      </listItem>
      <listItem>
        <para>PC settings (adds <ui>Change PC settings</ui> to the Settings charm)</para>
      </listItem>
      <listItem>
        <para>The ability to play a slide show on your lock screen</para>
      </listItem>
      <listItem>
        <para>Integrated search (searches through the Search charm integrate results from the local computer and the Internet through Bing)</para>
      </listItem>
    </list>
    <alert class="important">
      <para>When you install Desktop Experience in <token>winblue_server_Token>, the integrated search is on by default. This feature sends information to Microsoft. You can turn off the integrated search feature with the following steps:</para>
    </alert>
    <procedure>
      <title>To turn off integrated search</title>
      <steps class="ordered">
        <step>
          <content>
            <para>Open the Windows charm bar (WINDOWS+C)</para>
          </content>
        </step>
        <step>
          <content>
            <para>Click <ui>Settings</ui>, click <ui>Change PC Settings</ui>, and then click <ui>Search &amp; Apps</ui>.</para>
          </content>
        </step>
        <step>
          <content>
            <para>In the <ui>Use Bing to search online</ui> section, move the slider to <ui>Off</ui>. Alternately, in the <ui>Your Search Experience</ui> section, select <ui>Don’t get personalized results from Bing</ui>.</para>
          </content>
        </step>
      </steps>
    </procedure>
    <alert class="note">
      <para>The Desktop Experience feature requires that you also install the Graphical Management Tools and Infrastructure and Server Graphical Shell features.</para>
    </alert>
    <para>Media Foundation, which includes Windows Media Foundation, the Windows Media Format SDK, and a server subset of DirectShow, provides the infrastructure required for applications and services to transcode, analyze, and generate thumbnails for media files. You can install Media Foundation separately with Server Manager—but if you install the Desktop Experience feature, you must install the Media Foundation feature as well.</para>
  </introduction>
  <relatedTopics />
</developerConceptualDocument>

