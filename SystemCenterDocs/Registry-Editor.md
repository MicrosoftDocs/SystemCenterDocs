---
title: Registry Editor
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3165c505-893b-4c3f-852a-848d070dd6ad
---
# Registry Editor
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>System configuration information is stored centrally in a hierarchical database called the registry. You can use Registry Editor to add and edit registry keys and values, restore the registry from a backup or to default values, and to import or export keys for reference or backup. You can also print the registry and control which accounts have permission to edit the registry.</para>
    <alert class="note">
      <para>Over time, the registry may contain many entries for devices that will never be used again. To remove this information from the registry, download <externalLink><linkText>Microsoft DevNodeClean</linkText><linkUri>http://www.microsoft.com/download/details.aspx?id=42286</linkUri></externalLink>. For more information, see <externalLink><linkText>How to remove registry information for devices that will never be used again on a computer that's running Windows Server 2003 or a later version</linkText><linkUri>http://support.microsoft.com/kb/934234</linkUri></externalLink>.</para>
    </alert>
    <alert class="caution">
      <para>Incorrectly editing the registry may severely damage your system. Before making changes to the registry, you should back up any valued data on your computer and export the existing registry so that you can restore it if you make a mistake that results in your computer not starting properly.</para>
    </alert>
    <para>This topic explains how to import and export registry files. <token>whymshelpnotonbox</token> Much more information about the registry and using Registry Editor is available. <token>helpnotonbox</token></para>
    <para>
      <externalLink>
        <linkText>http://go.microsoft.com/fwlink/p/?linkid=221024</linkText> 
<linkUri>http://go.microsoft.com/fwlink/p/?linkid=221024</linkUri></externalLink>
    </para>
    <para />
  </introduction>
  <section>
    <title>Exporting registry files</title>
    <content>
      <para>To export all or part of the registry remotely, use Registry Editor. Once you have opened Registry Editor, you can export the registry to a text file or to a hive file.</para>
      <para>You can save registry files in the Windows format as registration files, as binary hive files, or as text files. Registry files are saved with .reg extensions, and text files are saved with .txt extensions.</para>
      <procedure>
        <title>Export all or part of the registry</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Registry Editor. If you want to save only a particular branch, select it.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>File</ui> menu, click <ui>Export…</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In <ui>File name</ui>, enter a name for the registry file.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In <ui>Save as type</ui>, select the file type you wish to use for the saved file (registration file, registry hive file, text file, Windows 98/NT4.0 registration file).</para>
            </content>
          </step>
          <step>
            <content>
              <para>In <ui>Export Range</ui>, use the radio buttons to select whether you want to export the entire registry or only the selected branch.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Click <ui>Save</ui>.</para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="note">
        <para>Certain parts of the registry are reserved and are not accessible to Regedit.exe. The option to export or import “all” of the registry applies to all of the registry that is accessible to Regedit.exe.</para>
      </alert>
    </content>
  </section>
  <section>
    <title>Importing registry files</title>
    <content>
      <para>The <ui>Import…</ui> command in Registry Editor can import registry files of all types, including text files and hive files.</para>
      <procedure>
        <title>Import some or all of the registry</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Registry Editor.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>File</ui> menu, click <ui>Import…</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Find the file you want to import, click the file to select it, and then click <ui>Open</ui>.</para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="note">
        <para>Certain parts of the registry are reserved and are not accessible to Regedit.exe. The option to export or import “all” of the registry applies to all of the registry that is accessible to Regedit.exe.</para>
      </alert>
      <alert class="note">
        <para>In File Explorer, double-clicking a file with the .reg extension imports the file into the computer's registry.</para>
      </alert>
      <alert class="caution">
        <para>A restored hive overwrites an existing registry key and becomes a permanent part of your configuration. For example, to perform maintenance on part of your system, you can use <ui>Export…</ui> to save a hive to a disk. When you are ready, you can then use <ui>Import…</ui> on the <ui>File</ui> menu to restore the saved key to your system</para>
      </alert>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>