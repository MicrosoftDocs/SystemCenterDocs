---
title: Software Restriction Policies Help
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3595e4ee-3841-43c0-8211-b53470203190
---
# Software Restriction Policies Help
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic for the IT professional contains procedures for administering application control policies by using Software Restriction Policies (SRPs).</para>
  </introduction>
  <section>
    <content>
      <para>Software Restriction Policies is a Group Policy-based feature that identifies software programs running on computers in a domain, and controls the ability of those programs to run. You use software restriction policies to create a highly restricted configuration for computers, in which you allow only specifically identified applications to run. These are integrated with Active Directory Domain Services and Group Policy, but they can also be configured on stand-alone computers. </para>
      <para>This topic contains the following procedures:</para>
      <list class="bullet">
        <listItem>
          <para>
            <link xlink:href="#BKMK_Create_SRP">How to create new software restriction policies</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_Add_Del">How to add or delete a designated file type</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_Prevent_Admin">How to prevent software restriction policies from applying to local administrators</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_Sec_Lvl">How to change the default security level of software restriction policies</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_Apply_SRP_DLLs">How to apply software restriction policies to DLLs</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="#BKMK_WorkingWithRules">How to work with SRPs rules</link>
          </para>
        </listItem>
      </list>
      <para>For information about using SRPs to design a portion of your application security strategy, see <legacyLink xlink:href="0abb73b6-b5d8-4505-8ab1-2f29e4bf0411">Determine Allow/Deny List and Application Inventory for Software Restriction Policies</legacyLink>.</para>
    </content>
  </section>
  <section address="BKMK_Create_SRP">
    <title>How to create new software restriction policies</title>
    <content>
      <para>Follow this procedure if you want to create new SRPs.</para>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>Different administrative credentials are required to perform this procedure, depending on your environment:</para>
            <list class="bullet">
              <listItem>
                <para>If you create new software restriction policies for your local computer: <token>mingrp_adminToken></para>
              </listItem>
              <listItem>
                <para>If you create new software restriction policies for a computer that is joined to a domain, members of the Domain Admins group can perform this procedure. </para>
              </listItem>
            </list>
          </listItem>
        </list>
      </alert>
      <procedure>
        <title>To create a new SRP</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Software Restriction Policies.</para>
            </content>
          </step>
          <step>
            <content>
              <para>On the <ui>Action</ui> menu, click <ui>New Software Restriction Policies</ui>.</para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="warning">
        <list class="bullet">
          <listItem>
            <para>If software restriction policies have already been created for a Group Policy Object (GPO), the <ui>New Software Restriction Policies</ui> command does not appear on the <ui>Action</ui> menu. To delete the software restriction policies that are applied to a GPO, in the console tree, right-click <ui>Software Restriction Policies</ui>, and then click <ui>Delete Software Restriction Policies</ui>. When you delete software restriction policies for a GPO, you also delete all software restriction policy rules for that GPO. After you delete software restriction policies, you can create new software restriction policies for that GPO.</para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section address="BKMK_Add_Del">
    <title>How to add or delete a designated file type</title>
    <content>
      <procedure>
        <title>To add or delete a file type</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Software Restriction Policies.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In the details pane, double-click <ui>Designated File Types</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Do one of the following: </para>
              <list class="bullet">
                <listItem>
                  <para>To add a file type, in <ui>File name extension</ui>, type the file name extension, and then click <ui>Add</ui>.</para>
                </listItem>
                <listItem>
                  <para>To delete a file type, in <ui>Designated file types</ui>, click the file type, and then click <ui>Remove</ui>.</para>
                </listItem>
              </list>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>Different administrative credentials are required to perform this procedure, depending on the environment in which you add or delete a designated file type:  </para>
            <list class="bullet">
              <listItem>
                <para>If you add or delete a designated file type for your local computer: <token>mingrp_adminToken></para>
              </listItem>
              <listItem>
                <para>If you create new software restriction policies for a computer that is joined to a domain, you must be a member of the Domain Admins group. </para>
              </listItem>
            </list>
          </listItem>
          <listItem>
            <para>It may be necessary to create a new software restriction policy setting for the Group Policy Object (GPO) if you have not already done so. </para>
          </listItem>
          <listItem>
            <para>For a GPO, the list of designated file types is shared by all rules for Computer Configuration and for User Configuration.</para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section address="BKMK_Prevent_Admin">
    <title>How to prevent software restriction policies from applying to local administrators</title>
    <content>
      <procedure>
        <title>To exempt local administrators</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Software Restriction Policies.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In the details pane, double-click <ui>Enforcement</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Under <ui>Apply software restriction policies to the following users</ui>, click <ui>All users except local administrators</ui>. </para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="warning">
        <list class="bullet">
          <listItem>
            <para>
              <token>mingrp_adminToken>
            </para>
          </listItem>
          <listItem>
            <para>It may be necessary to create a new software restriction policy setting for the Group Policy Object (GPO) if you have not already done so. </para>
          </listItem>
          <listItem>
            <para>If it is common for users to be members of the local Administrators group on their computers in your organization, you may not want to enable this option.</para>
          </listItem>
          <listItem>
            <para>If you are defining a software restriction policy setting for your local computer, use this procedure to prevent local administrators from having software restriction policies applied to them. If you are defining a software restriction policy setting for your network, filter user policy settings based on membership in security groups using Group Policy.</para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section address="BKMK_Sec_Lvl">
    <title>How to change the default security level of software restriction policies</title>
    <content>
      <procedure>
        <title>To change the default security level</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Software Restriction Policies.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In the details pane, double-click <ui>Security Levels</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Right-click the security level that you want to set as the default, and then click <ui>Set as default</ui>.</para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="caution">
        <para>In certain directories, setting the default security level to <ui>Disallowed</ui> can adversely affect your operating system. </para>
      </alert>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>Different administrative credentials are required to perform this procedure, depending on the environment for which you change the default security level of software restriction policies.  </para>
          </listItem>
          <listItem>
            <para>It may be necessary to create a new software restriction policy setting for this Group Policy Object (GPO) if you have not already done so. </para>
          </listItem>
          <listItem>
            <para>In the details pane, the current default security level is indicated by a black circle with a check mark in it. If you right-click the current default security level, the <ui>Set as default</ui> command does not appear in the menu.</para>
          </listItem>
          <listItem>
            <para>Software restriction policy rules are created to specify exceptions to the default security level. When the default security level is set to <ui>Unrestricted</ui>, rules can specify software that is not allowed to run. When the default security level is set to <ui>Disallowed</ui>, rules can specify software that is allowed to run.</para>
          </listItem>
          <listItem>
            <para>At installation, the default security level of software restriction policies on all files on your system is set to <ui>Unrestricted</ui>.</para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section address="BKMK_Apply_SRP_DLLs">
    <title>How to apply software restriction policies to DLLs</title>
    <content>
      <procedure>
        <title>To apply policies to DLLs</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open Software Restriction Policies.</para>
            </content>
          </step>
          <step>
            <content>
              <para>In the details pane, double-click <ui>Enforcement</ui>.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Under <ui>Apply software restriction policies to the following</ui>, click <ui>All software files</ui>. </para>
            </content>
          </step>
        </steps>
      </procedure>
      <alert class="note">
        <list class="bullet">
          <listItem>
            <para>To perform this procedure, you must be a member of the Administrators group on the local computer, or you must have been delegated the appropriate authority. If the computer is joined to a domain, members of the Domain Admins group can perform this procedure. </para>
          </listItem>
          <listItem>
            <para>By default, software restriction policies do not check dynamic-link libraries (DLLs). Checking DLLs can decrease system performance, because software restriction policies must be evaluated every time a DLL is loaded. However, you may decide to check DLLs if you are concerned about receiving a virus that targets DLLs. If the default security level is set to <ui>Disallowed</ui>, and you enable DLL checking, you must create software restriction policy rules that allow each DLL to run. </para>
          </listItem>
        </list>
      </alert>
    </content>
  </section>
  <section address="BKMK_WorkingWithRules">
    <title>How to work with SRP rules</title>
    <content>
      <para>With software restriction policies, you can protect your computing environment from untrusted software by identifying and specifying which software is allowed to run. You can define a default security level of <ui>Unrestricted</ui> or <ui>Disallowed</ui> for a Group Policy Object (GPO) so that software is allowed or not allowed to run by default. You can make exceptions to this default security level by creating software restriction policy rules for specific software. For example, if the default security level is set to <ui>Disallowed</ui>, you can create rules that allow specific software to run. The types of rules are:</para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Certificate rules</embeddedLabel>
          </para>
          <para>For procedures, see <link xlink:href="#BKMK_Cert_Rules">Working with certificate rules</link>.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Hash rules</embeddedLabel>
          </para>
          <para>For procedures, see <link xlink:href="#BKMK_Hash_Rules">Working with hash rules</link>.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Internet zone rules</embeddedLabel>
          </para>
          <para>For procedures, see <link xlink:href="#BKMK_Internet_Zone_Rules">Working with Internet zone rules</link>.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Path rules</embeddedLabel>
          </para>
          <para>For procedures, see <link xlink:href="#BKMK_Path_Rules">Working with path rules</link>.</para>
        </listItem>
      </list>
    </content>
    <sections>
      <section address="BKMK_Cert_Rules">
        <title>Working with certificate rules</title>
        <content>
          <para>Software restriction policies can identify software by its signing certificate. You can create a certificate rule that identifies software and then allows or does not allow the software to run, depending on the security level. For example, you can use certificate rules to automatically trust software from a trusted source in a domain without prompting the user. You can also use certificate rules to run files in disallowed areas of your operating system. </para>
          <para>Certificate rules are not enabled by default. When rules are created for the domain by using Group Policy, you must have permissions to create or modify a Group Policy Object. If you are creating rules for the local computer, you must have administrative credentials on that computer.</para>
          <procedure>
            <title>To create a certificate rule</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open Software Restriction Policies.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree or the details pane, right-click <ui>Additional Rules</ui>, and then click <ui>New Certificate Rule</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Click <ui>Browse</ui>, and then select a certificate or signed file.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Security level</ui>, click <ui>Disallowed</ui> or <ui>Unrestricted</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Description</ui>, type a description for this rule, and then click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <alert class="note">
            <list class="bullet">
              <listItem>
                <para>It might be necessary to create a new software restriction policy setting for the Group Policy Object (GPO) if you have not already done so. </para>
              </listItem>
              <listItem>
                <para>Certificate rules are not enabled by default. </para>
              </listItem>
              <listItem>
                <para>The only file types that are affected by certificate rules are those that are listed in <ui>Designated file types</ui> in the details pane for Software Restriction Policies. There is one list of designated file types that is shared by all rules. </para>
              </listItem>
              <listItem>
                <para>For software restriction policies to take effect, users must update policy settings by logging off and then logging on to their computers.</para>
              </listItem>
              <listItem>
                <para>When more than one software restriction policy rule is applied to policy settings, there is a precedence of rules for handling conflicts. </para>
              </listItem>
            </list>
          </alert>
        </content>
        <sections>
          <section>
            <title>Enabling certificate rules</title>
            <content>
              <para>There are different procedures for enabling certificate rules depending on your environment:</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <link xlink:href="#BKMK_CertRuleLocal">For your local computer</link>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <link xlink:href="#BKMK_CertRuleDomain">For a Group Policy Object from aserver that is joined to a domain</link>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <link xlink:href="#BKMK_CertRuleRSAT">For a Group Policy Object from a domain controller or workstation that has the RSAT installed</link>
                  </para>
                </listItem>
                <listItem>
                  <para>
                    <link xlink:href="#BKMK_CertRuleRSAT2">For only domain controllers from a domain controller or workstation that has RSAT installed</link>
                  </para>
                </listItem>
              </list>
              <procedure address="BKMK_CertRuleLocal">
                <title>To enable rules for your local computer</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open Local Security Settings.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, click <ui>Security Settings</ui>, click <ui>Local Policies</ui>, and then click <ui>Security Options</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the details pane, double-click <ui>System settings: Use Certificate Rules on Windows Executables for Software Restriction Policies</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Do one of the following, and then click <ui>OK</ui>:</para>
                      <list class="bullet">
                        <listItem>
                          <para>To enable certificate rules, click <ui>Enabled</ui>.</para>
                        </listItem>
                        <listItem>
                          <para>To disable certificate rules, click <ui>Disabled</ui>.</para>
                        </listItem>
                      </list>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure address="BKMK_CertRuleDomain">
                <title>To enable certificate rules for a GPO from a server joined to a domain</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open Microsoft Management Console (MMC).</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>On the <ui>File</ui> menu, click <ui>Add/Remove snap-in</ui>, and then click <ui>Add</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Click <ui>Local Group Policy Object Editor</ui>, and then click <ui>Add</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In <ui>Select Group Policy Object</ui>, click <ui>Browse</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In <ui>Browse for a Group Policy Object</ui>, select a Group Policy Object (GPO) in the appropriate domain, site, or organizational unit (or create a new one), and then click <ui>Finish</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Click <ui>Close</ui>, and then click <ui>OK</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, click <ui>Security Options</ui> located under <placeholder>GroupPolicyObject</placeholder> <placeholder>[ComputerName]</placeholder> Policy/Computer Configuration/Windows Settings/Security Settings/Local Policies/.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the details pane, double-click <ui>System settings: Use Certificate Rules on Windows Executables for Software Restriction Policies</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>If this policy setting has not yet been defined, select the <ui>Define these policy settings</ui> check box.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Do one of the following, and then click <ui>OK</ui>:</para>
                      <list class="bullet">
                        <listItem>
                          <para>To enable certificate rules, click <ui>Enabled</ui>.</para>
                        </listItem>
                        <listItem>
                          <para>To disable certificate rules, click <ui>Disabled</ui>.</para>
                        </listItem>
                      </list>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure address="BKMK_CertRuleRSAT">
                <title>To enable certificate rules for a GPO from a domain controller or workstation that has the RSAT</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open Active Directory Users and Computers.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, right-click the Group Policy Object (GPO) for which you want to enable certificate rules.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Click <ui>Properties</ui>, and then click the <ui>Group Policy</ui> tab.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Click <ui>Edit</ui> to open the GPO that you want to edit. You can also click <ui>New</ui> to create a new GPO, and then click <ui>Edit</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, click <ui>Security Options</ui> located under <placeholder>GroupPolicyObject</placeholder> <placeholder>[ComputerName]</placeholder> Policy/Computer Configuration/Windows Settings/Security Settings/Local Policies.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the details pane, double-click <ui>System settings: Use Certificate Rules on Windows Executables for Software Restriction Policies</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>If this policy setting has not yet been defined, select the <ui>Define these policy settings</ui> check box.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Do one of the following, and then click <ui>OK</ui>:</para>
                      <list class="bullet">
                        <listItem>
                          <para>To enable certificate rules, click <ui>Enabled</ui>.</para>
                        </listItem>
                        <listItem>
                          <para>To disable certificate rules, click <ui>Disabled</ui>.</para>
                        </listItem>
                      </list>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure address="BKMK_CertRuleRSAT2">
                <title>To enable certificate rules for only domain controllers from a domain controller or workstation that has the RSAT installed</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open Domain Controller Security Settings.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, click <legacyBold>Security Options</legacyBold> located under <placeholder>GroupPolicyObject</placeholder> [<placeholder>ComputerName</placeholder>] Policy/Computer Configuration/Windows Settings/Security Settings/Local Policies.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the details pane, double-click <ui>System settings: Use Certificate Rules on Windows Executables for Software Restriction Policies</ui>.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>If this policy setting has not yet been defined, select the <ui>Define these policy settings</ui> check box.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Do one of the following, and then click <ui>OK</ui>:</para>
                      <list class="bullet">
                        <listItem>
                          <para>To enable certificate rules, click <ui>Enabled</ui>.</para>
                        </listItem>
                        <listItem>
                          <para>To disable certificate rules, click <ui>Disabled</ui>.</para>
                        </listItem>
                      </list>
                    </content>
                  </step>
                </steps>
              </procedure>
              <alert class="note">
                <para>You must perform this procedure before certificate rules can take effect.</para>
              </alert>
            </content>
          </section>
          <section>
            <title>Setting trusted publisher options</title>
            <content>
              <para>Software signing is being used by a growing number of software publishers and application developers to verify that their applications come from a trusted source. However, many users do not understand or they pay little attention to the signing certificates that are associated with applications they install.</para>
              <para>The policy settings that are listed on the <ui>Trusted Publishers</ui> tab of the certificate path validation policy allows administrators to control which certificates can be accepted as coming from a trusted publisher.</para>
              <procedure>
                <title>To configure the trusted publishers policy settings for a local computer</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>
                        <token>winblue_starToken> <userInputLocalizable>gpedit.msc</userInputLocalizable> and then press ENTER.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree under <ui>Local Computer Policy\Computer Configuration\Windows Settings\Security Settings</ui>, click <ui>Public Key Policies</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Double-click <ui>Certificate Path Validation Settings</ui>, and then click the <ui>Trusted Publishers</ui> tab.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Select the <ui>Define these policy settings</ui> check box, select the policy settings that you want to apply, and then click <ui>OK</ui> to apply the new settings.</para>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure>
                <title>To configure the trusted publishers policy settings for a domain</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open <ui>Group Policy Management</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, double-click <ui>Group Policy Objects</ui> in the domain that contains the <ui>Default Domain Policy</ui> GPO that you want to edit.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Right-click the <ui>Default Domain Policy</ui> GPO, and then click <ui>Edit</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree under <ui>Computer Configuration\Windows Settings\Security Settings</ui>, click <ui>Public Key Policies</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Double-click <ui>Certificate Path Validation Settings</ui>, and then click the <ui>Trusted Publishers</ui> tab.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Select the <ui>Define these policy settings</ui> check box, select the policy settings that you want to apply, and then click <ui>OK</ui> to apply the new settings.</para>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure>
                <title>To allow only administrators to manage certificates used for code signing for a local computer</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>
                        <token>winblue_starToken> <userInputLocalizable>gpedit.msc</userInputLocalizable>, and then press ENTER.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree under <ui>Default Domain Policy</ui> or <ui>Local Computer Policy</ui>, double-click <ui>Computer Configuration</ui>, click <ui>Windows Settings</ui>, click <ui>Security Settings</ui>, and then click <ui>Public Key Policies</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Double-click <ui>Certificate Path Validation Settings</ui>, and then click the <ui>Trusted Publishers</ui> tab.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Select the <ui>Define these policy settings</ui> check box.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Under <ui>Trusted publisher management</ui>, click <ui>Allow only all administrators to manage Trusted Publishers</ui>, and then click <ui>OK</ui> to apply the new settings.</para>
                    </content>
                  </step>
                </steps>
              </procedure>
              <procedure>
                <title>To allow only administrators to manage certificates used for code signing for a domain</title>
                <steps class="ordered">
                  <step>
                    <content>
                      <para>Open <ui>Group Policy Management</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree, double-click <ui>Group Policy Objects</ui> in the domain that contains the <ui>Default Domain Policy</ui> GPO that you want to edit.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Right-click the <ui>Default Domain Policy</ui> GPO, and then click <ui>Edit</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>In the console tree under <ui>Computer Configuration\Windows Settings\Security Settings</ui>, click <ui>Public Key Policies</ui>. </para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Double-click <ui>Certificate Path Validation Settings</ui>, and then click the <ui>Trusted Publishers</ui> tab.</para>
                    </content>
                  </step>
                  <step>
                    <content>
                      <para>Select the <ui>Define these policy settings</ui> check box, implement the changes you want, and then click <ui>OK</ui> to apply the new settings.</para>
                    </content>
                  </step>
                </steps>
              </procedure>
            </content>
          </section>
        </sections>
      </section>
      <section address="BKMK_Hash_Rules">
        <title>Working with hash rules</title>
        <content>
          <para>A hash is a series of bytes with a fixed length that uniquely identifies a software program or file. The hash is computed by a hash algorithm. When a hash rule is created for a software program, software restriction policies calculate a hash of the program. When a user tries to open a software program, a hash of the program is compared to existing hash rules for software restriction policies. </para>
          <para>The hash of a software program is always the same, regardless of where the program is located on the computer. However, if a software program is altered in any way, its hash also changes, and it no longer matches the hash in the hash rule for software restriction policies.</para>
          <para>For example, you can create a hash rule and set the security level to <ui>Disallowed</ui> to prevent users from running a certain file. A file can be renamed or moved to another folder and still result in the same hash. However, any changes to the file itself also change its hash value and allow the file to bypass restrictions.</para>
          <procedure>
            <title>To create a hash rule</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open Software Restriction Policies.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree or the details pane, right-click <ui>Additional Rules</ui>, and then click <ui>New Hash Rule</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Click <ui>Browse</ui> to find a file, or paste a precalculated hash in <ui>File hash</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Security level</ui>, click <ui>Disallowed</ui> or <ui>Unrestricted</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Description</ui>, type a description for this rule, and then click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <alert class="note">
            <list class="bullet">
              <listItem>
                <para>It may be necessary to create a new software restriction policy setting for the Group Policy Object (GPO) if you have not already done so. </para>
              </listItem>
              <listItem>
                <para>A hash rule can be created for a virus or a Trojan horse to prevent them from running.</para>
              </listItem>
              <listItem>
                <para>If you want other people to use a hash rule so that a virus cannot run, calculate the hash of the virus by using software restriction policies, and then email the hash value to them. Never email the virusitself.</para>
              </listItem>
              <listItem>
                <para>If a virus has been sent through email, you can also create a path rule to prevent the email attachments from running.</para>
              </listItem>
              <listItem>
                <para>A file that is renamed or moved to another folder results in the same hash. Any change to the file results in a different hash.</para>
              </listItem>
              <listItem>
                <para>The only file types that are affected by hash rules are those that are listed in <ui>Designated File Types</ui> in the details pane for Software Restriction Policies. There is one list of designated file types that is shared by all rules.</para>
              </listItem>
              <listItem>
                <para>For software restriction policies to take effect, users must update policy settings by logging off and then logging on to their computers.    </para>
              </listItem>
              <listItem>
                <para>When more than one software restriction policy rule is applied to policy settings, there is a precedence of rules for handling conflicts.</para>
              </listItem>
            </list>
          </alert>
        </content>
      </section>
      <section address="BKMK_Internet_Zone_Rules">
        <title>Working with Internet zone rules</title>
        <content>
          <para>Internet zone rules apply only to Windows Installer packages. A zone rule can identify software from a zone that is specified through Internet Explorer. These zones are Internet, Local intranet, Restricted sites, Trusted sites, and My Computer. An Internet zone rule is designed to prevent users from downloading and installing software.</para>
          <procedure>
            <title>To create an Internet zone rule</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open Software Restriction Policies.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree or the details pane, right-click <ui>Additional Rules</ui>, and then click <ui>New Internet Zone Rule</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Internet zone</ui>, click an Internet zone.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Security level</ui>, click <ui>Disallowed</ui> or <ui>Unrestricted</ui>, and then click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <alert class="note">
            <list class="bullet">
              <listItem>
                <para>It may be necessary to create a new software restriction policy setting for the Group Policy Object (GPO) if you have not already done so. </para>
              </listItem>
              <listItem>
                <para>Zone rules only apply to files with an .msi file type, which are Windows Installer packages.</para>
              </listItem>
              <listItem>
                <para>For software restriction policies to take effect, users must update policy settings by logging off and then logging on to their computers.</para>
              </listItem>
              <listItem>
                <para>When more than one software restriction policy rule is applied to policy settings, there is a precedence of rules for handling conflicts.</para>
              </listItem>
            </list>
          </alert>
        </content>
      </section>
      <section address="BKMK_Path_Rules">
        <title>Working with path rules</title>
        <content>
          <para>A path rule identifies software by its file path. For example, if you have a computer that has a default security level of <ui>Disallowed</ui>, you can still grant unrestricted access to a specific folder for each user. You can create a path rule by using the file path and setting the security level of the path rule to <ui>Unrestricted</ui>. </para>
          <para>Some common paths for this type of rule are %userprofile%, %windir%, %appdata%, %programfiles%, and %temp%. You can also create registry path rules that use the registry key of the software as its path.</para>
          <para>Because these rules are specified by the path, if a software program is moved, the path rule no longer applies.</para>
          <procedure>
            <title>To create a path rule</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open Software Restriction Policies.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree or the details pane, right-click <ui>Additional Rules</ui>, and then click <ui>New Path Rule</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Path</ui>, type a path, or click <ui>Browse</ui> to find a file or folder.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Security level</ui>, click <ui>Disallowed</ui> or <ui>Unrestricted</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Description</ui>, type a description for this rule, and then click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <alert class="caution">
            <list class="bullet">
              <listItem>
                <para>For certain folders (such as the Windows folder), setting the security level to <legacyBold>Disallowed</legacyBold> can adversely affect the operation of your operating system. Make sure that you do not disallow a crucial component of the operating system or one of its dependent programs. </para>
              </listItem>
            </list>
            <para />
          </alert>
          <alert class="note">
            <list class="bullet">
              <listItem>
                <para>It may be necessary to create new software restriction policies for the Group Policy Object (GPO) if you have not already done so. </para>
              </listItem>
              <listItem>
                <para>If you create a path rule for software with a security level of <ui>Disallowed</ui>, users can still run the software by copying it to another location.</para>
              </listItem>
              <listItem>
                <para>The wildcard characters that are supported by the path rule are * and ?.</para>
              </listItem>
              <listItem>
                <para>You can use environment variables, such as %programfiles% or %systemroot%, in the path rule.</para>
              </listItem>
              <listItem>
                <para>If you want to create a path rule for software when you do not know where it is stored on a computer but you have its registry key, you can create a registry path rule. </para>
              </listItem>
              <listItem>
                <para>To prevent users from executing email attachments, you can create a path rule for your email program's attachment directory that prevents users from running email attachments.</para>
              </listItem>
              <listItem>
                <para>The only file types that are affected by path rules are those that are listed in <ui>Designated File Types</ui> in the details pane for Software Restriction Policies. There is one list of designated file types that is shared by all rules. </para>
              </listItem>
              <listItem>
                <para>For software restriction policies to take effect, users must update policy settings by logging off and then logging on to their computers.</para>
              </listItem>
              <listItem>
                <para>When more than one software restriction policy rule is applied to policy settings, there is a precedence of rules for handling conflicts. </para>
              </listItem>
            </list>
          </alert>
          <procedure>
            <title>To create a registry path rule</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>
                    <token>winblue_starToken> <userInput>regedit</userInput>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree, right-click the registry key that you want to create a rule for, and then click <ui>Copy Key Name</ui>. Note the value name in the details pane.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Open Software Restriction Policies.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the console tree or the details pane, right-click <ui>Additional Rules</ui>, and then click <ui>New Path Rule</ui>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Path</ui>, paste the registry key, followed by the value name.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Enclose the registry path in percent signs (%), for example, <environmentVariable>%HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PlatformSDK\Directories\InstallDir%</environmentVariable>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Security level</ui>, click <ui>Disallowed</ui> or <ui>Unrestricted</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <ui>Description</ui>, type a description for this rule, and then click <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>

