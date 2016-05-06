---
title: Configure File Management Tasks
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d4a6ef1-61bf-49aa-9339-44a56d2781ca
---
# Configure File Management Tasks
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>The following procedure guides you through the process of creating a file management task for expiring files, often referred to as a file expiration task. File expiration tasks are used to automatically move all files that match certain criteria to a specified expiration directory. An administrator can then back those files up and delete them. You can also use the procedure to create a file management task that applies Rights Management Services (RMS) encryption or performs a custom action.</para>
    <para>When a file expiration task is run, a new directory is created within the expiration directory. The directory is grouped by the server name on which the task was run. The new directory name is based on the name of the file management task and the time it was run. When an expired file is found it is moved into the new directory, while preserving its original directory structure.</para>
  </introduction>
  <section>
    <content>
      <procedure>
        <title>To create a file management task</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Click the <ui>File Management Tasks</ui> node.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Right-click <ui>File Management Tasks</ui>, and then click <ui>Create File Management Task</ui>. This opens the <ui>Create File Management Task</ui> dialog box.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>General</ui> tab, enter the following information:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <ui>Name</ui>. Enter a name for the new task.</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Description</ui>. Enter an optional descriptive label for this task.</para>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Scope</ui> tab, specify what folders you want to classify by entering the following information:</para>
              <list class="bullet">
                <listItem>
                  <para>Optionally, click <ui>Set Folder Management Properties</ui> to assign Folder Usage property values to folders and then click <ui>Close</ui> when you are finished. The Folder Usage property specifies the purpose of a folder and the kind of files that are stored in it. File management tasks and classification rules can use the value of the Folder Usage property that is assigned to a folder to determine whether to include the folder in a file management task or classification rule.</para>
                </listItem>
                <listItem>
                  <para>In the first box, specify the folders to include based on the Folder Usage property values that are assigned to the folders. When you select a Folder Usage property, all folders with that property assigned are listed as part of the scope.</para>
                </listItem>
                <listItem>
                  <para>Click <ui>Add</ui> to manually specify folders to include—independent of their assigned Folder Usage values.</para>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Action</ui> tab, enter the following information:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <ui>Type</ui>. Select <ui>File Expiration</ui> from the drop-down list (unless you want to apply RMS Encryption or perform a custom action instead).</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Expiration Directory</ui>. Select a directory or file share where the files will expire to. To use a file share, the computer account of the file server must have <ui>Modify</ui> permissions on the folder and <ui>Full Control</ui> share permissions.</para>
                  <alert class="warning">
                    <para>Do not select a directory that is within the scope of the task, as specified on the <ui>Scope</ui> tab. Doing so could cause an iterative loop that could lead to system instability and data loss.</para>
                  </alert>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>Optionally, on the <ui>Notification</ui> tab, click <ui>Add</ui> to send email notifications, to log an event, or to run a command or script a specified number of days in advance of when the task performs an action on a file.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Optionally, use the <ui>Report</ui> tab to generate one or more logs or storage reports.</para>
              <alert class="note">
                <para>The report is saved in the default location for incident reports, which you can modify in the <ui>File Server Resource Manager Options</ui> dialog box.</para>
              </alert>
            </content>
          </step>
          <step>
            <content>
              <para>Optionally, use the <ui>Condition</ui> tab to run this task only on files that match a defined set of conditions. </para>
              <para>Use the <ui>Property conditions</ui> section to add, edit, or remove conditions based on the file’s classification. Use the remaining fields on the tab to specify time-related conditions and file name pattern conditions.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Schedule</ui> tab, specify when the task should run, and then click <ui>OK</ui>.</para>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>