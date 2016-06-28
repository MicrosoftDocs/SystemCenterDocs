---
title: Installing VMM from a Command Prompt
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84b45ef1-bb8a-48f8-a2d7-5a93157ffc78
---
# Installing VMM from a Command Prompt

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can install <token>vmm12sp1_lonToken> by using a command prompt. Installing <token>vmm12shorToken> features involves saving installation settings in an .ini file and using the <system>setup.exe</system> command with that file.</para>
    <alert class="important">
      <para>For all of these procedures, use the <ui>Run as administrator</ui> option to open an elevated command prompt.</para>
    </alert>
  </introduction>
  <section>
    <title>Installation files</title>
    <content>
      <para>Your installation media contains .ini files for each <token>vmm12shorToken> feature:</para>
      <list class="bullet">
        <listItem>
          <para>
            <system>VMServer.ini</system>
          </para>
          <para>Settings for the <token>vmm12shorToken> management server.</para>
        </listItem>
        <listItem>
          <para>
            <system>VMClient.ini</system>
          </para>
          <para>Settings for the <token>vmm12shorToken> console.</para>
        </listItem>
        <listItem>
          <para>
            <system>VMServerUninstall.ini</system>
          </para>
          <para>Uninstallation settings for the <token>vmm12shorToken> management server.</para>
        </listItem>
      </list>
      <para>The files contain key/value pairs that have default values. These entries are commented out. To edit the file, remove the comment symbol (#) and change the value.</para>
    </content>
    <sections/>
  </section>
  <section>
    <title>Installing a VMM management server by using a command prompt</title>
    <content>
      <para>To install a <token>vmm12shorToken> management server, edit the VMServer.ini file and then run the <system>setup.exe</system> command.</para>
      <alert class="note">
        <para>When you install a <token>vmm12shorToken> management server, the <token>vmm12shorToken> console is automatically installed.</para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Configuring options for a VMM management server in the installation file</title>
        <content>
          <para/>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>
                    Option</para>
                </TD>
                <TD>
                  <para>Values</para>
                </TD>
                <TD>
                  <para>Default</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>ProductKey</para>
                </TD>
                <TD>
                  <para>Product key in the format: xxxxx-xxxxx-xxxxx-xxxxx-xxxxx</para>
                  <para/>
                </TD>
                <TD>
                  <para>
                    <parameterReference>xxxxx-xxxxx-xxxxx-xxxxx-xxxxx</parameterReference>
                  </para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>UserName</para>
                </TD>
                <TD>
                  <para>Optional display name for the user who is installing the features.</para>
                  <alert class="note">
                    <para>This is not the user account for the installation.</para>
                  </alert>
                </TD>
                <TD>
                  <para>Administrator</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>CompanyName</para>
                </TD>
                <TD>
                  <para>Optional display name for the organization that is installing the features. </para>
                </TD>
                <TD>
                  <para>Microsoft Corporation</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>ProgramFiles</para>
                </TD>
                <TD>
                  <para>Location for <token>vmm12shorToken> files.</para>
                </TD>
                <TD>
                  <para>C:Program FilesMicrosoft System Center 2012Virtual Machine Manager</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>CreateNewSqlDatabase</para>
                </TD>
                <TD>
                  <para>0: Use an existing Microsoft SQL Server database.</para>
                  <para>1: Create a new SQL Server database.</para>
                </TD>
                <TD>
                  <para>1</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SqlInstanceName</para>
                </TD>
                <TD>
                  <para>Name of the new or existing instance of SQL Server. </para>
                </TD>
                <TD>
                  <para>MICROSOFT$VMM$</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SqlDatabaseName</para>
                </TD>
                <TD>
                  <para>Name of the new or existing SQL Server database.</para>
                </TD>
                <TD>
                  <para>VirtualManagerDB</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>RemoteDatabaseImpersonation</para>
                </TD>
                <TD>
                  <para>0: Do not impersonate the administrator account for SQL Server.</para>
                  <alert class="important">
                    <para>The user that runs <system>setup.exe</system> must be an administrator for the server that is hosting SQL Server.</para>
                  </alert>
                  <para>1: Impersonate the administrator account for SQL Server by using the provided credentials.</para>
                  <alert class="important">
                    <para>The user who runs <system>setup.exe</system> must provide values for the <system>SqlDBAdminName</system>, <system>SqlDBAdminPassword</system>, and <system>SqlDBAdminDomain</system> parameters.</para>
                  </alert>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SqlMachineName</para>
                </TD>
                <TD>
                  <para>Name of the server that is hosting SQL Server. <?Comment ak: As per bug 451982 2014-09-08T18:01:00Z  Id='1?>Do not specify <userInput>localhost</userInput>. Instead, specify the actual name of the computer.<?CommentEnd Id='1'
    ?></para>
                </TD>
                <TD>
                  <para>
                    <placeholder>&lt;sqlmachinename&gt;</placeholder>
                  </para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>(various ports)</para>
                </TD>
                <TD>
                  <para>For information about ports, see <link xlink:href="6a33f439-9e47-443d-b36c-359986260df9">Ports and Protocols for VMM</link>.</para>
                  <para/>
                  <para/>
                </TD>
                <TD>
                  <para>IndigoTcpPort: 8100</para>
                  <para>IndigoHTTPSPort: 8101</para>
                  <para>IndigoNETTCPPort: 8102</para>
                  <para>IndigoHTTPPort: 8103</para>
                  <para>WSManTcpPort: <?Comment ak: As per TFS bug456606 2014-09-08T18:01:00Z  Id='2?>5985<?CommentEnd Id='2'
    ?></para>
                  <para>BitsTcpPort: 443</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>CreateNewLibraryShare</para>
                </TD>
                <TD>
                  <para>0: Use an existing <?Comment SJ: GLOBAL COMMENT: This topic uses a mix of &quot;library share&quot; and &quot;file share.&quot; Please standardize on whichever is more accurate. 2014-09-08T18:01:00Z  Id='3?>library share<?CommentEnd Id='3'
    ?>.</para>
                  <para>1: Create a new library share.</para>
                </TD>
                <TD>
                  <para>1</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LibraryShareName</para>
                </TD>
                <TD>
                  <para>Name of the file share to be used or created.</para>
                </TD>
                <TD>
                  <para>MSSCVMMLibrary</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LibrarySharePath</para>
                </TD>
                <TD>
                  <para>Location of the existing file share or the new file share to be created.</para>
                </TD>
                <TD>
                  <para>C:ProgramDataVirtual Machine Manager Library Files</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LibraryShareDescription</para>
                </TD>
                <TD>
                  <para>Description of the share.</para>
                </TD>
                <TD>
                  <para>Virtual Machine Manager Library Files</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SQMOptIn</para>
                </TD>
                <TD>
                  <para>0: Do not opt in for "Diagnostic and Usage Data". </para>
                  <para>1: Opt in for "Diagnostic and Usage Data</para>
                  
                <para>For more information about data collection and usage see <externalLink><linkText>Privacy Statement for System Center 2016 Technical Preview 4</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=623851&amp;clcid=0x409</linkUri></externalLink> </para></TD>
                <TD>
                  <para>1</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>MUOptIn</para>
                </TD>
                <TD>
                  <para>0: Do not opt in to Microsoft Update. </para>
                  <para>1: Opt in to Microsoft Update. </para>
                  <para>For more information about Microsoft Update, see <externalLink><linkText>Frequently Asked Questions</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=115474</linkUri></externalLink>. </para>
                  <para>For Microsoft Update privacy information, see <externalLink><linkText>Update Services Privacy Statement</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=115475</linkUri></externalLink>. </para>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>VmmServiceLocalAccount</para>
                </TD>
                <TD>
                  <para>0: Use a domain account for the <token>vmm12shorToken> service (scvmmservice). </para>
                  <para>1: Use the Local System account for the <token>vmm12shorToken> service.</para>
                  <alert class="note">
                    <para>To use a domain account, when you run <system>setup.exe</system>, provide values for the <system>VMMServiceDomain</system>, <system>VMMServiceUserName</system>, and <system>VMMServiceUserPassword</system> parameters. </para>
                    <para>For more information about service accounts, see <link xlink:href="edaf90db-563d-4fd3-b6ef-55ea5abc7835">Specifying a Service Account for VMM</link>.</para>
                  </alert>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>TopContainerName</para>
                </TD>
                <TD>
                  <para>Container for Distributed Key Management (DKM); for example, “CN=DKM,DC=contoso,DC=com”. </para>
                  <para>For more information about DKM, see <link xlink:href="1238b5b8-98fc-4c2b-bdb5-253e4e1b3baa">Configuring Distributed Key Management in VMM</link>.</para>
                </TD>
                <TD>
                  <para>VMMServer</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>HighlyAvailable</para>
                </TD>
                <TD>
                  <para>0: Do not install as highly available.</para>
                  <para>1: Install as highly available.</para>
                  <para>For information about highly available installations, see <link xlink:href="b952e8ab-ce6f-4014-9e96-50cedaf415ed">Installing a Highly Available VMM Management Server</link>.</para>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>VmmServerName</para>
                </TD>
                <TD>
                  <para>Clustered service name for a highly available <token>vmm12shorToken> management server.</para>
                  <alert class="important">
                    <para>Do not enter the name of the failover cluster or the name of the computer on which the highly available <token>vmm12shorToken> management server is installed. For more information, see <link xlink:href="dbc92290-e10b-4a9b-9794-3dc4bc71ca25">How to Install a Highly Available VMM Management Server</link>.</para>
                  </alert>
                </TD>
                <TD>
                  <para>
                    <placeholder>&lt;VMMServerName&gt;</placeholder>
                  </para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>VMMStaticIPAddress</para>
                </TD>
                <TD>
                  <para>IP address for the clustered service name for a highly available <token>vmm12shorToken> management server, if you are not using Dynamic Host Configuration Protocol (DHCP).</para>
                  <alert class="note">
                    <para>Both IPv4 and IPv6 are supported.</para>
                  </alert>
                </TD>
                <TD>
                  <para>
                    <placeholder>&lt;comma-separated-ip-for-HAVMM&gt;</placeholder>
                  </para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Upgrade</para>
                </TD>
                <TD>
                  <para>0: Do not upgrade from a previous version of <token>vmm12shorToken>.</para>
                  <para>1: Upgrade from a previous version.</para>
                </TD>
                <TD>
                  <para>1</para>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Installing a VMM management server by using a command prompt</title>
        <content>
          <para>After you edit VMServer.ini, open an elevated command prompt, and then run <system>setup.exe</system> by using the following parameters: </para>
          <list class="bullet">
            <listItem>
              <para>
                <system>/server</system>
              </para>
              <para>Specifies installation of the <token>vmm12shorToken> management server.</para>
            </listItem>
            <listItem>
              <para>
                <system>/i</system> or <system>/x</system></para>
              <para>Specifies whether to install (<system>/i</system>) or uninstall (<system>/x</system>) the server.</para>
            </listItem>
            <listItem>
              <para>
                <system>/f &lt;filename&gt;</system>
              </para>
              <para>Specifies the .ini file to use.</para>
              <alert class="important">
                <para>Be sure that this parameter points to the correct .ini file. If <system>setup.exe</system> does not find an .ini file, it will perform the installation by using its own default values. </para>
              </alert>
            </listItem>
            <listItem>
              <para>
                <system>/VmmServiceDomain &lt;domainName&gt;</system>
              </para>
              <para>Specifies the domain name for the account that is running the <token>vmm12shorToken> service (scvmmservice). Use this parameter only if you set <system>VmmServiceLocalAccount</system> to 0 in VMServer.ini.</para>
            </listItem>
            <listItem>
              <para>
                <system>/VmmServiceUserName &lt;userName&gt;</system>
              </para>
              <para>Specifies the user name for the account that is running the <token>vmm12shorToken> service (scvmmservice). Use this parameter only if you set <system>VmmServiceLocalAccount</system> to 0 in VMServer.ini.</para>
            </listItem>
            <listItem>
              <para>
                <system>/VmmServiceUserPassword &lt;password&gt;</system>
              </para>
              <para>Specifies the password for the account that is running the <token>vmm12shorToken> service (scvmmservice). Use this parameter only if you set <system>VmmServiceLocalAccount</system> to 0 in VMServer.ini.</para>
            </listItem>
            <listItem>
              <para>
                <system>/SqlDBAdminDomain &lt;domainName&gt;</system>
              </para>
              <para>Specifies the domain name for the administrator account for the SQL Server database. Use this parameter if the current user does not have <?Comment SJ: I used this phrasing for consistency with the next two list items. Please confirm that &quot;administrative rights to SQL Server&quot; is more accurate than &quot;administrative rights to the server that is running SQL Server.&quot; All three list items should use the same phrasing. 2014-09-08T18:01:00Z  Id='6?>administrative rights to SQL Server<?CommentEnd Id='6'
    ?>.</para>
            </listItem>
            <listItem>
              <para>
                <system>/SqlDBAdminName &lt;userName&gt;</system>
              </para>
              <para>Specifies the user name for the administrator account for the SQL Server database. Use this parameter if the current user does not have administrative rights to SQL Server.</para>
            </listItem>
            <listItem>
              <para>
                <system>/SqlDBAdminPassword &lt;password&gt;</system>
              </para>
              <para>Specifies the password for the administrator account for the SQL Server database. Use this parameter if the current user does not have administrative rights to SQL Server.</para>
            </listItem>
            <listItem>
              <para>
                <system>/IACCEPTSCEULA</system> </para>
              <para>Notes acceptance of the Microsoft Software License Terms. This is a mandatory parameter.</para>
            </listItem>
          </list>
          <para>For example, to use a VMServer.ini file that is stored in C:Temp with a SQL Server administrator account of contosoSQLAdmin01 and a <token>vmm12shorToken> service account of contosoVMMadmin14, use the following command:</para>
          <para>
            <userInput>setup.exe /server /i /f C:TempVMServer.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123 /VmmServiceDomain contoso /VmmServiceUserName VMMadmin14 /VmmServiceUserPassword password456 /IACCEPTSCEULA</userInput>
          </para>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>Uninstalling a VMM management server by using a command prompt</title>
    <content>
      <para>To uninstall a <token>vmm12shorToken> management server, edit the VMServerUninstall.ini file and then run the <system>setup.exe</system> command.</para>
    </content>
    <sections>
      <section>
        <title>Configuring options for uninstalling a VMM management server</title>
        <content>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Option</para>
                </TD>
                <TD>
                  <para>Values</para>
                </TD>
                <TD>
                  <para>Default</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>RemoteDatabaseImpersonation</para>
                </TD>
                <TD>
                  <para>0: Local SQL Server installation. </para>
                  <para>1: Remote SQL Server installation. </para>
                  <para>When you run <system>setup.exe</system>, provide a value for the <system>SqlDBAdminName</system>, <system>SqlDBAdminPassword,</system> and <system>SqlDBAdminDomain</system> parameters unless the user who is running <system>setup.exe</system> is an administrator for SQL Server.</para>
                  <para>Replaces the <system>OnRemoteServer</system> setting in VMM 2008 R2.</para>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>RetainSqlDatabase</para>
                </TD>
                <TD>
                  <para>0: Remove the SQL Server database. </para>
                  <para>1: Do not remove the SQL Server database.</para>
                  <alert class="important">
                    <para>To remove the SQL Server database, when you run <system>setup.exe</system>, provide a value for the <system>SqlDBAdminName</system>, <system>SqlDBAdminPassword,</system> and <system>SqlDBAdminDomain</system> parameters unless the user who is running Setup is an administrator for SQL Server.</para>
                  </alert>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>ForceHAVMMUninstall</para>
                </TD>
                <TD>
                  <para>0: Do not force uninstallation if <system>setup.exe</system> cannot verify whether this node is the final node of the highly available installation.</para>
                  <para>1: Force the uninstallation. </para>
                  <para>For more information about uninstalling a highly available <token>vmm12shorToken> management server, see <link xlink:href="d664710d-7e8e-4f83-a4b2-2979197aa099">How to Uninstall a Highly Available VMM Management Server</link>.</para>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Uninstalling a VMM management server by using a command prompt</title>
        <content>
          <para>To uninstall a <token>vmm12shorToken> management server by using a VMServerUninstall.ini file that is stored in C:Temp, with a SQL Server administrator account of contosoSQLAdmin01, use this command:</para>
          <para>
            <userInput>setup.exe /server /x /f C:TempVMServerUninstall.ini /SqlDBAdminDomain contoso /SqlDBAdminName SQLAdmin01 /SqlDBAdminPassword password123</userInput>
          </para>
        </content>
      </section>
    </sections>
  </section>
  <section>
    <title>Installing or uninstalling a VMM console by using a command prompt</title>
    <content>
      <para>To install a <token>vmm12shorToken> console, edit the VMClient.ini file and then run the <system>setup.exe</system> command.</para>
      <para>To uninstall a <token>vmm12shorToken> console, run the <system>setup.exe</system> command. There is no separate .ini file for uninstalling the <token>vmm12shorToken> console.</para>
      <alert class="note">
        <para>Do not attempt to uninstall the <token>vmm12shorToken> console from a system that includes a <token>vmm12shorToken> management server. You must first uninstall the <token>vmm12shorToken> management server.</para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Configuring options for a VMM console</title>
        <content>
          <para/>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Option</para>
                </TD>
                <TD>
                  <para>Values</para>
                </TD>
                <TD>
                  <para>Default</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>ProgramFiles</para>
                </TD>
                <TD>
                  <para>Location for <token>vmm12shorToken> files.</para>
                </TD>
                <TD>
                  <para>C:Program FilesMicrosoft System Center 2012Virtual Machine Manager</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>IndigoTcpPort</para>
                </TD>
                <TD>
                  <para>Port that is used for communication between the <token>vmm12shorToken> management server and the <token>vmm12shorToken> console.</para>
                </TD>
                <TD>
                  <para>8100</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>MUOptIn</para>
                </TD>
                <TD>
                  <para>0: Do not opt in to Microsoft Update. </para>
                  <!--Need to update these links--><para>1: Opt in to Microsoft Update. </para>
                  <para>For more information about Microsoft Update, see <externalLink><linkText>Frequently Asked Questions</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=115474</linkUri></externalLink>. </para>
                  <para>For Microsoft Update privacy information, see <externalLink><linkText>Update Services Privacy Statement</linkText><linkUri>http://go.microsoft.com/fwlink/p/?LinkID=115475</linkUri></externalLink>. </para>
                </TD>
                <TD>
                  <para>0</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>VmmServerForOpsMgrConfig</para>
                </TD>
                <TD>
                  <para>This setting is not used. For more information, see <link xlink:href="ac1948c6-41f2-4c5b-9933-b307a2e21420">Configuring Operations Manager Integration with VMM</link>.</para>
                </TD>
                <TD>
                  <para>
                    <placeholder>&lt;VMMServerName&gt;</placeholder>
                  </para>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Installing a VMM console by using a command prompt</title>
        <content>
          <para>After you edit VMClient.ini, use an elevated command prompt to run <system>setup.exe</system> by using the following parameters: </para>
          <list class="bullet">
            <listItem>
              <para>
                <system>/client</system>
              </para>
              <para>Specifies installation of the <token>vmm12shorToken> console.</para>
            </listItem>
            <listItem>
              <para>
                <system>/i</system> or <system>/x</system></para>
              <para>Specifies whether to install (<system>/i</system>) or uninstall (<system>/x</system>) the console.</para>
            </listItem>
            <listItem>
              <para>
                <system>/f &lt;filename&gt;</system>
              </para>
              <para>Specifies the .ini file to use.</para>
              <alert class="important">
                <list class="bullet">
                  <listItem>
                    <para>Be sure that the <system>/f &lt;filename&gt;</system> parameter points to the correct .ini file. If <system>setup.exe</system> does not find an .ini file, it will perform the installation by using its own default values.</para>
                  </listItem>
                  <listItem>
                    <para>Do not use the <system>/opsmgr</system> parameter. Instead, see <link xlink:href="ac1948c6-41f2-4c5b-9933-b307a2e21420">Configuring Operations Manager Integration with VMM</link>.</para>
                  </listItem>
                </list>
              </alert>
            </listItem>
          </list>
          <para>For example, to use a VMClient.ini file that is stored in C:Temp, use this command:</para>
          <para>
            <userInput>setup.exe /client /i /f C:TempVMClient.ini</userInput>
          </para>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics>
    <link xlink:href="1b4c3f5f-4ade-44c2-8866-f7b37168607d">Installing System Center vNext Virtual Machine Manager</link>
  </relatedTopics>
</developerConceptualDocument>


