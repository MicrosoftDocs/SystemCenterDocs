---
title: AppLocker
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40da294b-501b-4357-a047-a8ff391e0ca1
---
# AppLocker
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic describes the controls on the AppLocker user interface to help you create and maintain application control policies by using AppLocker in <token>winblue_server_Token> and <token>winblue_client_Token>.</para>
  </introduction>
  <section>
    <title>About AppLocker</title>
    <content>
      <para>You can use AppLocker as part of your overall security strategy for the following scenarios:</para>
      <list class="bullet">
        <listItem>
          <para>Help prevent malicious software (malware) and unsupported applications from affecting computers in your environment.</para>
        </listItem>
        <listItem>
          <para>Prevent users from installing and using unauthorized applications. </para>
        </listItem>
        <listItem>
          <para>Implement application control policies to satisfy portions of your security policy or compliance requirements in your organization.</para>
        </listItem>
      </list>
      <para>For more information, see <legacyLink xlink:href="358610e4-88b2-40d0-b34d-dfd7ddee0ed9">AppLocker Overview [Server]</legacyLink>.</para>
    </content>
    <sections>
      <section>
        <title>In this topic</title>
        <content>
          <para>
            <link xlink:href="#BKMK_Enforcement">Enforcement modes</link>
          </para>
          <para>
            <link xlink:href="#BKMK_RuleCollections">Rule collections</link>
          </para>
          <para>
            <link xlink:href="#BKMK_RuleConditions">Rule conditions</link>
          </para>
          <para>
            <link xlink:href="#BKMK_DefaultRules">Default rules</link>
          </para>
          <para>
            <link xlink:href="#BKMK_Behavior">AppLocker rule behavior</link>
          </para>
          <para>
            <link xlink:href="#BKMK_RuleExceptions">Rule exceptions</link>
          </para>
          <para>
            <link xlink:href="#BKMK_DLLRules">DLL rule collection</link>
          </para>
          <para>
            <link xlink:href="#BKMK_Wizards">AppLocker wizards</link>
          </para>
          <para>
            <link xlink:href="#BKMK_AddConsiderations">Additional considerations</link>
          </para>
          <para>
            <link xlink:href="#BKMK_AddResources">Additional resources</link>
          </para>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_Enforcement">
    <title>Enforcement modes</title>
    <content>
      <para>The three AppLocker enforcement modes are described in the following table. The enforcement mode settings that are defined here can be overwritten by a setting that is derived from a linked Group Policy Object (GPO) with a higher precedence.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Enforcement mode</para>
            </TD>
            <TD>
              <para>Description</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>
                <ui>Not configured</ui>
              </para>
            </TD>
            <TD>
              <para>This is the default setting, which means that the rules defined here will be enforced unless a linked GPO with a higher precedence has a different value for this setting.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>Enforce rules</ui>
              </para>
            </TD>
            <TD>
              <para>Rules are enforced.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>
                <ui>Audit only</ui>
              </para>
            </TD>
            <TD>
              <para>Rules are audited but not enforced. When a user runs an application that is affected by an AppLocker rule, the application is allowed to run, and the information about the application is added to the AppLocker event log. The Audit-only enforcement mode helps you determine which applications will be affected by the policy before the policy is enforced. When the AppLocker policy for a rule collection is set to <ui>Audit only</ui>, rules for that rule collection are not enforced.</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>When AppLocker policies from various GPOs are merged, the rules from all the GPOs are merged and the enforcement mode setting of the winning GPO is applied.</para>
      <para>For information about GPOs and Group Policy inheritance, see the <externalLink><linkText>Group Policy Planning and Deployment Guide</linkText><linkUri>http://go.microsoft.com/fwlink/p/?linkid=143138</linkUri></externalLink>.</para>
    </content>
  </section>
  <section address="BKMK_RuleCollections">
    <title>Rule collections</title>
    <content>
      <para>The AppLocker user interface is accessed through the Microsoft Management Console (MMC), and it is organized into rule collections, which are Executable files, Scripts, Windows Installer files, <token>applocker_modernappToken>, <token>applocker_pkgToken> and DLL files. These collections give the administrator an easy way to differentiate the rules for different types of applications. The following table lists the file formats that are included in each rule collection.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Rule collection</para>
            </TD>
            <TD>
              <para>Associated file formats</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Executable files</para>
            </TD>
            <TD>
              <para>.exe</para>
              <para>.com</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Scripts</para>
            </TD>
            <TD>
              <para>.ps1</para>
              <para>.bat</para>
              <para>.cmd</para>
              <para>.vbs</para>
              <para>.js</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Windows Installer files</para>
            </TD>
            <TD>
              <para>.msi</para>
              <para>.msp</para>
              <para>.mst</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Appx (<token>applocker_modernappToken> and <token>applocker_pkgToken>)</para>
            </TD>
            <TD>
              <para>.appx</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>DLL files</para>
            </TD>
            <TD>
              <para>.dll</para>
              <para>.ocx</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para/>
      <alert class="important">
        <para>If you use DLL rules, you need to create an Allow rule for each DLL that is used by all of the allowed applications.</para>
        <para>When DLL rules are used, AppLocker must check each DLL that an application loads. Therefore, users may experience a reduction in performance if DLL rules are used.</para>
        <para>The DLL rule collection is not enabled by default. To learn how to enable the DLL rule collection, see <link xlink:href="#BKMK_DLLRules">DLL rule collection</link>.</para>
      </alert>
    </content>
  </section>
  <section address="BKMK_RuleConditions">
    <title>Rule conditions</title>
    <content>
      <para>Rule conditions are criteria that help AppLocker identify the applications to which the rule applies. The three primary rule conditions are Publisher, Path, and File hash.</para>
      <list class="bullet">
        <listItem>
          <para>
            <link xlink:href="#BKMK_Publisher">Publisher</link>: Identifies an application based on its digital signature</para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_Path">Path</link>: Identifies an application by its location in the file system of the computer or on the network</para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_FileHash">File hash</link>: Represents the system-computed cryptographic hash of the identified file</para>
        </listItem>
      </list>
    </content>
    <sections>
      <section address="BKMK_Publisher">
        <title>Publisher</title>
        <content>
          <para>This condition identifies an application based on its digital signature and extended attributes when available. The digital signature contains information about the company that created the application (the publisher). Executable files, DLLs, Windows installers, <token>applocker_modernappToken>, and <token>applocker_pkgToken> also have extended attributes, which are obtained from the binary resource. Attributes for executable files, DLLs, and Windows installers contain the name of the product that the file is a part of, the original name of the file as supplied by the publisher, and the version number of the file. In <token>applocker_modernappToken> and <token>applocker_pkgToken>, these extended attributes contain the name and the version of the application package.</para>
          <alert class="note">
            <para>Rules that are created in the <token>applocker_modernapToken> and <token>applocker_pkToken> rule collection can only have the Publisher condition because Windows does not support unsigned <token>applocker_modernappToken> or <token>applocker_pkgToken>.</para>
          </alert>
          <para/>
          <alert class="note">
            <para>Use a Publisher rule condition when possible because they can survive application updates in addition to a change in the location of files. </para>
          </alert>
          <para>When you select a reference file for a Publisher condition, the wizard creates a rule that specifies the publisher, product, file name, and version number. You can make the rule more generic by moving the slider up or by using a wildcard character (*) in the product, file name, or version number fields. </para>
          <alert class="note">
            <para>To enter custom values for any of the fields of a Publisher rule condition in the Create Rules Wizard, you must select the <ui>Use custom values</ui> check box. When this check box is selected, you cannot use the slider.</para>
          </alert>
          <para>The <ui>File version</ui> and <ui>Package version</ui> control whether a user can run a specific version, earlier versions, or later versions of the application. You can choose a version number and then configure the following options: </para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>Exactly</embeddedLabel>. The rule applies only to this version of the application.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>And above</embeddedLabel>. The rule applies to this version and all later versions.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>And below</embeddedLabel>. The rule applies to this version and all earlier versions.</para>
            </listItem>
          </list>
          <para>The following table describes how a Publisher condition is applied.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Option</para>
                </TD>
                <TD>
                  <para>The publisher condition allows or denies…</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>
                    <ui>All signed files</ui>
                  </para>
                </TD>
                <TD>
                  <para>All files that are signed by a publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher only</ui>
                  </para>
                </TD>
                <TD>
                  <para>All files that are signed by the named publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher and product name</ui>
                  </para>
                </TD>
                <TD>
                  <para>All files for the specified product that are signed by the named publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher and product name, and file name</ui>
                  </para>
                </TD>
                <TD>
                  <para>Any version of the named file or package for the named product that are signed by the publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher, product name, file name, and file version</ui>
                  </para>
                <para>
                    <ui>Exactly</ui>
                  </para></TD>
               
                <TD>
                  <para>The specified version of the named file or package for the named product that are signed by the publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher, product name, file name, and file version</ui>
                  </para>
                <para>
                    <ui>And above</ui>
                  </para></TD>
              
                <TD>
                  <para>The specified version of the named file or package and any new releases for the product that are signed by the publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Publisher, product name, file name, and file version</ui>
                  </para>
                <para>
                    <ui>And below</ui>
                  </para></TD>
               
                <TD>
                  <para>The specified version of the named file or package and any earlier versions for the product that are signed by the publisher.</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <ui>Custom</ui>
                  </para>
                </TD>
                <TD>
                  <para>You can edit the <ui>Publisher</ui>, <ui>Product name</ui>, <ui>File name</ui>, <ui>Version</ui> <ui>Package name</ui>, and <ui>Package version</ui> fields to create a custom rule.</para>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section address="BKMK_Path">
        <title>Path</title>
        <content>
          <para>This rule condition identifies an application by its location in the file system of the computer or on the network.</para>
          <para>AppLocker uses custom path variables for well-known paths, such as <ui>Program Files</ui> and <ui>Windows</ui>. </para>
          <para>The following table details these path variables.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Windows directory or disk</para>
                </TD>
                <TD>
                  <para>AppLocker path variable</para>
                </TD>
                <TD>
                  <para>Windows environment variable</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Windows</para>
                </TD>
                <TD>
                  <para>%WINDIR%</para>
                </TD>
                <TD>
                  <para>%SystemRoot%</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>System32</para>
                </TD>
                <TD>
                  <para>%SYSTEM32%</para>
                </TD>
                <TD>
                  <para>%SystemDirectory%</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Windows installation directory</para>
                </TD>
                <TD>
                  <para>%OSDRIVE%</para>
                </TD>
                <TD>
                  <para>%SystemDrive%</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Program Files</para>
                </TD>
                <TD>
                  <para>%PROGRAMFILES%</para>
                </TD>
                <TD>
                  <para>%ProgramFiles% and </para>
                  <para>%ProgramFiles(x86)%</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Removable media (for example, a CD or DVD)</para>
                </TD>
                <TD>
                  <para>%REMOVABLE%</para>
                </TD>
                <TD>
                  <para/>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Removable storage device (for example, a USB flash drive)</para>
                </TD>
                <TD>
                  <para>%HOT%</para>
                </TD>
                <TD>
                  <para/>
                </TD>
              </tr>
            </tbody>
          </table>
          <para/>
          <alert class="important">
            <para>Because a Path rule condition can be configured to include a large number of folders and files, Path conditions should be carefully planned. For example, if an Allow rule with a Path condition includes a folder location where non-administrators are allowed to write data, a user can copy unapproved files into that location and run the files. For this reason, it is a best practice to not create path conditions for standard user writable locations, such as a user profile.</para>
          </alert>
        </content>
      </section>
      <section address="BKMK_FileHash">
        <title>File hash</title>
        <content>
          <para>When you choose the File hash rule condition, the system computes a cryptographic hash of the identified file. The advantage of this rule condition is that because each file has a unique hash, a File hash rule condition applies to only one file. The disadvantage is that each time the file is updated (such as a security update or upgrade) the file's hash will change. As a result, you must manually update File hash rules. </para>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_DefaultRules">
    <title>Default rules</title>
    <content>
      <para>AppLocker allows you to generate default rules for each rule collection. </para>
      <para>Executable default rule types include:</para>
      <list class="bullet">
        <listItem>
          <para>Allow members of the local <embeddedLabel>Administrators</embeddedLabel> group to run all applications.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run applications that are located in the <ui>Windows</ui> folder.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run applications that are located in the <ui>Program Files</ui> folder.</para>
        </listItem>
      </list>
      <para>Script default rule types include:</para>
      <list class="bullet">
        <listItem>
          <para>Allow members of the local <embeddedLabel>Administrators</embeddedLabel> group to run all scripts.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run scripts that are located in the <ui>Windows</ui> folder.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run scripts that are located in the <ui>Program Files</ui> folder.</para>
        </listItem>
      </list>
      <para>Windows Installer default rule types include:</para>
      <list class="bullet">
        <listItem>
          <para>Allow members of the local <embeddedLabel>Administrators</embeddedLabel> group to run all Windows Installer files.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run all digitally signed Windows Installer files.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run all Windows Installer files that are located in the Windows\Installer folder.</para>
        </listItem>
      </list>
      <para>DLL default rule types:</para>
      <list class="bullet">
        <listItem>
          <para>Allow members of the local <embeddedLabel>Administrators</embeddedLabel> group to run all DLLs.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run DLLs that are located in the <ui>Windows</ui> folder.</para>
        </listItem>
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to run DLLs that are located in the <ui>Program Files</ui> folder.</para>
        </listItem>
      </list>
      <para>The <token>applocker_modernapToken> default rule types:</para>
      <list class="bullet">
        <listItem>
          <para>Allow members of the <embeddedLabel>Everyone</embeddedLabel> group to install and run all signed <token>applocker_modernappToken> and <token>applocker_pkgToken>.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Behavior">
    <title>AppLocker rule behavior</title>
    <content>
      <para>If no AppLocker rules for a specific rule collection exist, all files with that file format are allowed to run. However, when an AppLocker rule for a specific rule collection is created, only the files explicitly allowed in a rule are permitted to run. For example, if you create an executable rule that allows .exe files in <placeholder>%SystemDrive%\FilePath</placeholder> to run, only executable files located in that path are allowed to run. </para>
      <para>A rule can be configured to use allow or deny actions:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Allow</embeddedLabel>. You can specify which files are allowed to run in your environment, and for which users or groups of users. You can also configure exceptions to identify files that are excluded from the rule.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Deny</embeddedLabel>. You can specify which files are not allowed to run in your environment, and for which users or groups of users. You can also configure exceptions to identify files that are excluded from the rule.</para>
        </listItem>
      </list>
      <alert class="important">
        <para>For a best practice, use Allow actions with exceptions. You can use a combination of Allow and Deny actions, but Deny actions override Allow actions in all cases, and combined actions can be circumvented.</para>
      </alert>
      <para/>
      <alert class="important">
        <para>If you want to allow any <token>applocker_modernappToken> in your environment while continuing to control executables, you should create default rules for <token>applocker_modernappToken> and set the enforcement mode to Audit-only for the <token>applocker_modernapToken> rule collection.</para>
      </alert>
    </content>
  </section>
  <section address="BKMK_RuleExceptions">
    <title>Rule exceptions</title>
    <content>
      <para>You can apply AppLocker rules to individual users or to a group of users. If you apply a rule to a group of users, all users in that group are affected by that rule. If you need to allow a subset of a user group to use an application, you can create a special rule for that subset. For example, the rule "Allow Everyone to run Windows except Registry Editor" allows everyone in the organization to run the Windows operating system, but it does not allow anyone to run Registry Editor. </para>
      <para>The effect of this rule would prevent users such as Help Desk personnel from running a program that is necessary for their support tasks. To resolve this problem, create a second rule that applies to the Help Desk user group: "Allow Help Desk to run Registry Editor." If you create a Deny rule that does not allow any users to run Registry Editor, the Deny rule will override the second rule that allows the Help Desk user group to run Registry Editor.</para>
    </content>
  </section>
  <section address="BKMK_DLLRules">
    <title>DLL rule collection</title>
    <content>
      <para>Because the DLL rule collection is not enabled by default, you must perform the following procedure before you can create and enforce DLL rules.</para>
      <para>
        <token>mingrp_adminToken>
      </para>
      <procedure>
        <title>To enable the DLL rule collection</title>
        <steps class="ordered">
          <step>
            <content>
              <para>
                <token>winblue_starToken> <userInput>secpol.msc</userInput>, and then press ENTER. </para>
            </content>
          </step>
          <step>
            <content>
              <para>
                <token>uac_confirm_actioToken>
              </para>
            </content>
          </step>
          <step>
            <content>
              <para>In the console tree, double-click <ui>Application Control Policies</ui>, right-click <ui>AppLocker</ui>, and then click <ui>Properties</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Click the <ui>Advanced</ui> tab, select the <ui>Enable the DLL rule collection</ui> check box, and then click <ui>OK</ui>.</para>
              <alert class="important">
                <para>Before you enforce DLL rules, make sure that there are Allow rules for each DLL that is used by any of the allowed applications.</para>
              </alert>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <section address="BKMK_Wizards">
    <title>AppLocker wizards</title>
    <content>
      <para>You can create rules by using two AppLocker wizards:</para>
      <list class="ordered">
        <listItem>
          <para>The Create Rules Wizard enables you to create one rule at a time. </para>
        </listItem>
        <listItem>
          <para>The Automatically Generate Rules Wizard allows you to create multiple rules at one time. You can select a folder and let the wizard create rules for the relevant files within that folder, or in case of <token>applocker_modernappToken>, you can let the wizard create rules for all <token>applocker_modernappToken> that are installed on the computer. You can also specify the user or group to which to apply the rules. This wizard automatically generates Allow rules only.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_AddConsiderations">
    <title>Additional considerations</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>By default, AppLocker rules do not allow users to open or run any files that are not specifically allowed. Administrators should maintain an up-to-date list of allowed applications. </para>
        </listItem>
        <listItem>
          <para>There are two types of AppLocker conditions that do not persist following an update of an application: </para>
          <list class="bullet">
            <listItem>
              <para>
                <embeddedLabel>File hash condition</embeddedLabel>. File hash rule conditions can be used with any application because a cryptographic hash value of the application is generated at the time the rule is created. However, the hash value is specific to that exact version of the application. If there are several versions of the application in use within the organization, you need to create file hash conditions for each version in use and for any new versions that are released.</para>
            </listItem>
            <listItem>
              <para>
                <embeddedLabel>A publisher condition with a specific product version set</embeddedLabel>. If you create a publisher rule condition that uses the <embeddedLabel>Exactly</embeddedLabel> version option, the rule cannot persist if a new version of the application is installed. A new publisher condition must be created, or the version must be edited in the rule to be made less specific.</para>
            </listItem>
          </list>
        </listItem>
        <listItem>
          <para>If an application is not digitally signed, you cannot use a Publisher rule condition for that application.</para>
        </listItem>
        <listItem>
          <para>AppLocker rules cannot be used to manage computers running a Windows operating system earlier than <token>nextref_server_Token> or <token>nextref_client_Token>. Software Restriction Policies must be used instead. If AppLocker rules are defined in a Group Policy Object (GPO), only those rules are applied. To ensure interoperability between Software Restriction Policies rules and AppLocker rules, define Software Restriction Policies rules and AppLocker rules in different GPOs.</para>
        </listItem>
        <listItem>
          <para>The <token>applocker_modernapToken> and <token>applocker_pkToken>  rule collection is not available in <token>nextref_server_Token> or <token>nextref_client_Token>.</para>
        </listItem>
        <listItem>
          <para>When the rules for the executable rule  collection are enforced and the <token>applocker_modernapToken> and <token>applocker_pkToken> rule collection does not contain any rules, no <token>applocker_modernappToken> or <token>applocker_pkgToken> are allowed to run. To allow <token>applocker_modernappToken> or <token>applocker_pkgToken>, you must create rules for the <token>applocker_modernapToken> and <token>applocker_pkToken> rule collection.</para>
        </listItem>
        <listItem>
          <para>When an AppLocker rule collection is set to <ui>Audit only</ui>, the rules are not enforced. When a user runs an application that is included in the rule, the application is opened and runs normally, and information about that application is added to the AppLocker event log.</para>
        </listItem>
        <listItem>
          <para>A custom configured URL can be included in the message that is displayed when an application is blocked.</para>
        </listItem>
      </list>
      <alert class="note">
        <para>Expect an increase in the number of Help Desk calls initially because of blocked applications until users understand that they cannot run applications that are not allowed. </para>
      </alert>
    </content>
  </section>
  <section address="BKMK_AddResources">
    <title>Additional resources</title>
    <content>
      <para>The following table lists and describes resources for you to manage security policies using AppLocker.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Resource</para>
            </TD>
            <TD>
              <para>Windows Server 2008 R2 and Windows 7</para>
            </TD>
            <TD>
              <para>
                <token>winblue_server_Token>, <token>win8_server_Token>, <token>winblue_client_Token> and <token>win8_client_Token></para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Product evaluation</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Frequently Asked Questions</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee619725(WS.10).aspx</linkUri>
                </externalLink>
              </para>
              <para>
                <externalLink>
                  <linkText>AppLocker Step-by-Step Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/dd723686(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Frequently Asked Questions</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee619725(WS.10).aspx</linkUri>
                </externalLink>
              </para>
              <para>
                <externalLink>
                  <linkText>AppLocker Step-by-Step Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/dd723686(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Procedures</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Operations Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee791916(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <legacyLink xlink:href="fdf79e90-8318-41cc-8601-8bf83726b93f">Administer AppLocker</legacyLink>
              </para>
              <para>
                <legacyLink xlink:href="30ca862f-74ae-45e2-9918-46e9f9ee05c7">Manage Packaged Apps with AppLocker</legacyLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Scripting</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Using the AppLocker Windows PowerShell Cmdlets</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee791828(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>Using the AppLocker Windows PowerShell Cmdlets</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee791828(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Technical content</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Technical Reference</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee844115(v=WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Technical Reference</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee844115(v=WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Design, planning, and deployment</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Policies Design Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee449480(WS.10).aspx</linkUri>
                </externalLink>
              </para>
              <para>
                <externalLink>
                  <linkText>AppLocker Policies Deployment Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee791890(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Policies Design Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee449480(WS.10).aspx</linkUri>
                </externalLink>
              </para>
              <para>
                <externalLink>
                  <linkText>AppLocker Policies Deployment Guide</linkText>
                  <linkUri>http://technet.microsoft.com/library/ee791890(WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>General information and additional resources</para>
            </TD>
            <TD>
              <para>
                <externalLink>
                  <linkText>AppLocker Documentation for Windows 7 and Windows Server 2008 R2</linkText>
                  <linkUri>http://technet.microsoft.com/library/dd723678(v=WS.10).aspx</linkUri>
                </externalLink>
              </para>
            </TD>
            <TD>
              <para>
                <legacyLink xlink:href="1637ae87-5059-4d95-8c68-96f35cbc88c7">AppLocker Overview [Client]</legacyLink>
              </para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <relatedTopics/>
</developerConceptualDocument>

