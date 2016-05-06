---
title: Configure Classification Rules
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3771cc72-cc54-4f5b-87db-9851038be662
---
# Configure Classification Rules
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Classification properties are used to categorize files. They can be used to restrict access to files and to select files for scheduled file management tasks. The following procedure guides you through the process of creating a classification rule, assuming that the classification properties that you want to set have already been created. Each rule sets the value for a single property.</para>
    <alert class="note">
      <para>The Windows PowerShell classifier requires that the Windows PowerShell execution policy allows the script to run. </para>
    </alert>
  </introduction>
  <section>
    <content>
      <procedure>
        <title>To create a classification rule</title>
        <steps class="ordered">
          <step>
            <content>
              <para>In <ui>Classification Management</ui>, click the <ui>Classification Rules</ui> node.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Right-click <ui>Classification Rules</ui>, and then click <ui>Create Classification Rule</ui>. This opens the <ui>Create Classification Rule</ui> dialog box.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>General</ui> tab, enter the following information:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <ui>Rule name</ui>. Type a name for the rule.</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Enabled</ui>. This rule will only be applied if the <ui>Enabled</ui> box is selected. To disable the rule, clear this box.</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Description</ui>. Type an optional description for this rule.</para>
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
              <para>On the <ui>Classification</ui> tab, enter the following information:</para>
              <list class="bullet">
                <listItem>
                  <para>In the <ui>Classification method</ui> section, choose the classifier module that will assign the property to files.</para>
                </listItem>
                <listItem>
                  <para>In the <ui>Property</ui> section, choose the property to assign to files, and set the value of the property.</para>
                </listItem>
                <listItem>
                  <para>In the <ui>Parameters</ui> section, if present, click <ui>Configure</ui> to specify additional parameters that are recognized by the selected classification method.</para>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Evaluation Type</ui> tab, optionally specify whether this classification rule should overwrite or add to any existing properties that are assigned to the affected files by using the following settings: </para>
              <list class="bullet">
                <listItem>
                  <para>
                    <ui>Re-evaluate existing property values</ui>   Controls whether this classification rule should overwrite or add to any existing properties that are assigned to the affected files. When the check box is cleared, the classification rule only applies if the property that is specified by the rule has not already been assigned to the affected files.</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Overwrite the existing value</ui>   Specifies that the rule should overwrite any existing values for the property that is assigned by the rule.</para>
                </listItem>
                <listItem>
                  <para>
                    <ui>Aggregate the values</ui>   Specifies that the rule should combine the values that are assigned by the rule with any already assigned to the file.</para>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>Click <ui>OK</ui> when you are finished creating the rule.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Optionally, in the <ui>Classification Rules</ui> node, click <ui>Configure Classification Schedule</ui> to schedule the rules to run automatically, or click <ui>Run Classification With All Rules Now</ui> to run the rules immediately.</para>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>