---
title: Object picker UI
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 084c5529-77c8-466a-ab4e-2466391b459f
---
# Object picker UI
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>
      <token>client_redir</token>
    </para>
    <para>This topic contains examples of object types that you can select when configuring access to various types of computer objects (for example, ownership and permissions).</para>
  </introduction>
  <section>
    <content>
      <para>Use the Object Picker control to type the object names that you want to find on the network or the local computer. You can search for multiple objects by separating each name with a semicolon. For information about Active Directory objects that you can specify in this dialog box when your computer is part of a domain, see <link xlink:href="084c5529-77c8-466a-ab4e-2466391b459f#BKMK_ADobjcts">Active Directory Domain Services objects</link> later in this topic.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Object Type</para>
            </TD>
            <TD>
              <para>Details</para>
            </TD>
            <TD>
              <para>Examples</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Built-in security principal</para>
            </TD>
            <TD>
              <para>Represents default built-in groups and security principals. </para>
              <para>To view built-in principals, type <userInput>Users</userInput> on the Start screen, click <ui>Edit local users and groups</ui>, and then double-click <ui>Groups</ui> or <ui>Users</ui>.</para>
            </TD>
            <TD>
              <para>
                <embeddedLabel>Users:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrator</para>
                </listItem>
                <listItem>
                  <para>Guest</para>
                </listItem>
              </list>
              <para>
                <embeddedLabel>Groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Power Users</para>
                </listItem>
                <listItem>
                  <para>Everyone</para>
                </listItem>
                <listItem>
                  <para>Authenticated Users</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Computer</para>
            </TD>
            <TD>
              <para>Represents a computer's access to network resources.</para>
              <para>The computer name was established when the operating system was installed. The computer name is recorded on the computer information page in <token>winblue_client_2</token>. To view it, type <userInput>System</userInput> on the Start screen.</para>
            </TD>
            <TD>
              <para>
                <?Comment DR: Is this an approved fictitious name? I sent an email to our rep to find out, but thought you might know. 2014-06-23T12:42:00Z  Id='1?>CarrollB<?CommentEnd Id='1'
    ?>-HomeComputer</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Group</para>
            </TD>
            <TD>
              <para>Can contain users, computers, and other groups as members.</para>
              <para>To view these security principals, type <userInput> Groups</userInput> on the Start screen, click <ui>Edit local users and groups</ui>, and then double-click <ui>Groups</ui>. </para>
            </TD>
            <TD>
              <para>
                <embeddedLabel>Client operating system groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Power Users</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
              </list>
              <para>
                <embeddedLabel>Server operating system groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>System Operators</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Power Users</para>
                </listItem>
                <listItem>
                  <para>Everyone</para>
                </listItem>
                <listItem>
                  <para>Authenticated Users</para>
                </listItem>
                <listItem>
                  <para>Anonymous Logon</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
                <listItem>
                  <para>System</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Users</para>
            </TD>
            <TD>
              <para>Allows people to access network resources.</para>
              <para>To view users who currently have accounts on this local computer, type <userInput> Users</userInput> on the Start screen, click <ui>Edit local users and groups</ui>, and then double-click <ui>Users</ui>.</para>
            </TD>
            <TD>
              <para>CarrollB</para>
              <para>HomeServer\CarrollB</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Contact</para>
            </TD>
            <TD>
              <para>Locates information about people. Contact objects cannot be assigned permissions, and therefore, they do not have access to network resources.</para>
              <para>Local Contact objects can be found in the following directory path on your computer: &lt;drive&gt;\Users\&lt;user name&gt;\Contacts.</para>
            </TD>
            <TD>
              <para>Carroll Blythe</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Other</para>
            </TD>
            <TD>
              <para>Can be created by applications.</para>
            </TD>
            <TD>
              <para>Specific for each instance</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_ADobjcts">
    <title>Active Directory Domain Services objects</title>
    <content>
      <para>Real-world objects such as users and computers are represented as objects in Active Directory. And these objects can be contained in other objects called container objects. Active Directory Domain Services supports numerous object types, and each is represented by a unique global identifier.</para>
      <para>Each object has a set of attributes that best describe it. For example, consider a user object. Each user can have attributes such as Name, Address, and Telephone number. The objects that can be authenticated and to which permissions can be assigned are called security principals. Each security principal object has a security identifier (SID) associated with it, in addition to the global identifier (GUID). </para>
      <para />
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Object Type</para>
            </TD>
            <TD>
              <para>Details</para>
            </TD>
            <TD>
              <para>Examples</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Built-in security principal</para>
            </TD>
            <TD>
              <para>Represents default built-in groups and security principals. </para>
            </TD>
            <TD>
              <para>
                <embeddedLabel>Users:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrator</para>
                </listItem>
                <listItem>
                  <para>Cert Publishers</para>
                </listItem>
                <listItem>
                  <para>Domain Guests</para>
                </listItem>
                <listItem>
                  <para>Guest</para>
                </listItem>
              </list>
              <para>
                <embeddedLabel>Groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>Server Operators</para>
                </listItem>
                <listItem>
                  <para>Print Operators</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Hyper-V Administrators</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Computer</para>
            </TD>
            <TD>
              <para>Represents a work station or a server in a network. A computer account helps in authenticating and authorizing its access to network resources.</para>
            </TD>
            <TD>
              <para>CarrollB </para>
              <para>CARROLLB.sales.contoso.com</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Group</para>
            </TD>
            <TD>
              <para>Represents a collection of user accounts, computer accounts, contacts, and other groups that can be managed as a single unit. Groups facilitate role-based access to network resources. There are two types of groups:</para>
              <list class="bullet">
                <listItem>
                  <para>Security groups are mainly used for the purpose of providing access to network resources.</para>
                </listItem>
                <listItem>
                  <para>Distribution groups are not security-enabled and can be used only for communication purposes. Groups can vary in scope, limiting their membership and scope of operation.</para>
                </listItem>
              </list>
            </TD>
            <TD>
              <para>
                <embeddedLabel>Client operating system groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Power Users</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
              </list>
              <para>
                <embeddedLabel>Server operating system groups:</embeddedLabel>
              </para>
              <list class="bullet">
                <listItem>
                  <para>Administrators</para>
                </listItem>
                <listItem>
                  <para>System Operators</para>
                </listItem>
                <listItem>
                  <para>Users</para>
                </listItem>
                <listItem>
                  <para>Power Users</para>
                </listItem>
                <listItem>
                  <para>Everyone</para>
                </listItem>
                <listItem>
                  <para>Authenticated Users</para>
                </listItem>
                <listItem>
                  <para>Anonymous Logon</para>
                </listItem>
                <listItem>
                  <para>Guests</para>
                </listItem>
                <listItem>
                  <para>System</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>User</para>
            </TD>
            <TD>
              <para>Represents individuals who need access to the resources in a network. Each user account has a user name and a password. The purpose behind creating user accounts is to authenticate the identity of the user and authorize the user's access to network resources. Active Directory supports two types of built-in user accounts: Administrator and Guest.</para>
            </TD>
            <TD>
              <para>CarrollB</para>
              <para>Contoso\CarrollB</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Contact</para>
            </TD>
            <TD>
              <para>Contains the contact information about people who are associated with the organization but are not part of it, for example, contractors or suppliers. A contact object does not have a SID associated with it, which prevents it from having access to network resources.</para>
            </TD>
            <TD>
              <para>Carroll Blythe</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Shared folder</para>
            </TD>
            <TD>
              <para>Used to share files across the network. It is mapped to a file share on a server.</para>
              <para>In Active Directory, published shared folders are located in an organizational unit. </para>
            </TD>
            <TD>
              <para>&lt;drive&gt;:\Users\CarrollB\Public</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Printer</para>
            </TD>
            <TD>
              <para>Corresponds to a printer resource in a network. Printer objects are listed under the Domain Controllers container in Active Directory Users and Computers.</para>
            </TD>
            <TD>
              <para>Printer object naming is organization-specific, for example: 2012-ColorTone 200 Driver, which is a driver associated with Type of Printer.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section>
    <title>See also</title>
    <content>
      <list class="bullet">
        <listItem>
          <para>
            <legacyLink xlink:href="90050086-fd7a-41c7-801e-9136a898a65a">Security Principals Technical Overview</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="f48ac289-ebe0-4988-a927-68180b633207">Security Identifiers Technical Overview</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="88d00616-2b16-4186-b5f6-7e07287c5952">Active Directory Accounts</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="473eff45-2b15-4f68-964f-df49f24fa3f6">Active Directory Security Groups</legacyLink>
          </para>
        </listItem>
        <listItem>
          <para>
            <legacyLink xlink:href="ac11b502-deb1-4738-9f01-1bee20045c89">Local Accounts</legacyLink>
          </para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>