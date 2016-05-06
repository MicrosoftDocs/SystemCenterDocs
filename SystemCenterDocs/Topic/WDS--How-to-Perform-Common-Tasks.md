---
title: WDS: How to Perform Common Tasks
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e73be1e0-2dca-43b2-97e9-5691ea47fbf6
---
# WDS: How to Perform Common Tasks
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic contains procedures for performing common tasks using Windows Deployment Services MMC snap-in. and the WDSUTIL command line tool. The management tasks that you can perform with these tools fall into the following categories:</para>
  </introduction>
  <section>
    <title />
    <content>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD colspan="1">
              <para>Category</para>
            </TD>
            <TD colspan="1">
              <para>Task groups</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD colspan="1">
              <para>
                <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_wdssvrmgmt">Server Management Tasks</link>
              </para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>
                    <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_genset">General WDS server setup</link>
                  </para>
                </listItem>
                <listItem>
                  <para>DHCP configuration settings</para>
                </listItem>
                <listItem>
                  <para>Client request settings</para>
                </listItem>
                <listItem>
                  <para>Client boot settings</para>
                </listItem>
                <listItem>
                  <para>AD DS settings</para>
                </listItem>
                <listItem>
                  <para>Unattend file configuration</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_wdscmgmt">Computer Management Tasks</link>
              </para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>Create and delete prestaged accounts in Active Directory Domain Services (AD DS)</para>
                </listItem>
                <listItem>
                  <para>View information about prestaged computers </para>
                </listItem>
                <listItem>
                  <para>Configure settings for prestaged computers</para>
                </listItem>
                <listItem>
                  <para>Reject/approve pending computers</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_wdsimgmt">Image Management Tasks</link>
              </para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>View information about images and image groups</para>
                </listItem>
                <listItem>
                  <para>Create images</para>
                </listItem>
                <listItem>
                  <para>Add, copy, export, remove, update images from the image store</para>
                </listItem>
                <listItem>
                  <para>Set attributes and associate unattend files for install images.</para>
                </listItem>
                <listItem>
                  <para>Convert RIPREP images </para>
                </listItem>
                <listItem>
                  <para>Add and remove image groups</para>
                </listItem>
                <listItem>
                  <para>Set attributes of an image group</para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD colspan="1">
              <para>
                <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_wdsbcdedit">How to use Bcdedit to Modify the BCD File</link>
              </para>
            </TD>
            <TD colspan="1">
              <list class="bullet">
                <listItem>
                  <para>To view the contents of the BCD store </para>
                </listItem>
                <listItem>
                  <para>To configure the default selection time-out value </para>
                </listItem>
                <listItem>
                  <para>To configure a localized boot manager experience </para>
                </listItem>
                <listItem>
                  <para>To configure the TFTP block size and window size </para>
                </listItem>
                <listItem>
                  <para>To configure Windows debugger options </para>
                </listItem>
              </list>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
    <sections>
      <section address="BKMK_wdssvrmgmt">
        <title>Server Management Tasks</title>
        <content>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD colspan="1">
                  <para>Type</para>
                </TD>
                <TD colspan="1">
                  <para>Procedure</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD colspan="1">
                  <para>
                    <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_genset">General WDS server setup</link>
                  </para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_remote">To manage a server remotely </link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_configure">To configure Windows Deployment Services</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_startstop">To start or stop the server</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_enable">To enable the server</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_logging">To enable logging for the Windows Deployment Services client </link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_rpcport">To choose the port number for RPCs</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_nic">To specify the network interfaces for Windows Deployment Services to listen on</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_refresh">To configure how often the server refreshes its settings</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_risfolder">To force the server to update files in the RemoteInstall folder</link>
                      </para>
                    </listItem>
                    <listItem>
                      <para>
                        <link xlink:href="e73be1e0-2dca-43b2-97e9-5691ea47fbf6#BKMK_netpro">To configure the network profile for the server</link>
                      </para>
                    </listItem>
                  </list>
                </TD>
              </tr>
              <tr>
                <TD colspan="1">
                  <para>DHCP configuration settings</para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>To configure Windows Deployment Services to run on the same computer as Microsoft DHCP</para>
                    </listItem>
                    <listItem>
                      <para>To configure Windows Deployment Services to run on the same computer as non-Microsoft DHCP</para>
                    </listItem>
                    <listItem>
                      <para>To turn on the DHCP authorization requirement</para>
                    </listItem>
                    <listItem>
                      <para>To authorize the server in DHCP</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
              <tr>
                <TD colspan="1">
                  <para>Client request settings</para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>To configure the server to answer clients</para>
                    </listItem>
                    <listItem>
                      <para>To set a delay in the server’s answers to network requests</para>
                    </listItem>
                    <listItem>
                      <para>To configure unknown clients to perform network boots without requiring F12</para>
                    </listItem>
                    <listItem>
                      <para>To configure clients who have booted without F12 to require a key press on subsequent boots</para>
                    </listItem>
                    <listItem>
                      <para>To configure the server to determine the architecture of booting clients</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
              <tr>
                <TD colspan="1">
                  <para>Client boot settings</para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>To choose which boot images are displayed on x64-based computers</para>
                    </listItem>
                    <listItem>
                      <para>To choose the default network boot program for each architecture</para>
                    </listItem>
                    <listItem>
                      <para>To choose the default network boot program that does not require F12 for each architecture</para>
                    </listItem>
                    <listItem>
                      <para>To choose the default boot image for each architecture</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
              <tr>
                <TD colspan="1">
                  <para>AD DS settings</para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>To specify a domain controller for Windows Deployment Services</para>
                    </listItem>
                    <listItem>
                      <para>To specify a global catalog server for Windows Deployment Services</para>
                    </listItem>
                    <listItem>
                      <para>To choose whether to search for computer accounts in the domain controller before searching the global catalog</para>
                    </listItem>
                    <listItem>
                      <para>To configure the server to prestage clients by using their MAC address instead of their GUID</para>
                    </listItem>
                    <listItem>
                      <para>To maintain a list of GUIDs that belong to multiple computers</para>
                    </listItem>
                    <listItem>
                      <para>To specify how to generate client computer names</para>
                    </listItem>
                    <listItem>
                      <para>To specify the domain and OU in which to create client computer accounts</para>
                    </listItem>
                    <listItem>
                      <para>To specify that client computers should not be joined to a domain</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
              <tr>
                <TD colspan="1">
                  <para>Unattend file configuration</para>
                </TD>
                <TD colspan="1">
                  <list class="bullet">
                    <listItem>
                      <para>To choose a default unattend file for the Windows Deployment Services client </para>
                    </listItem>
                    <listItem>
                      <para>To specify whether an unattend file on the client computer overrides the default unattend file </para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
        <sections>
          <section address="BKMK_genset">
            <title>General WDS server setup</title>
            <content>
              <para />
            </content>
            <sections>
              <section address="BKMK_remote">
                <title>To manage a server remotely </title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Method</para>
                        </TD>
                        <TD colspan="1">
                          <para>Explanation</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>Managing from another Windows Deployment Services server</para>
                        </TD>
                        <TD colspan="1">
                          <para>To do this, you must specify which server you want to manage. You can do this in either of the following ways:</para>
                          <list class="bullet">
                            <listItem>
                              <para>
                                <system>Using the Windows Deployment Services MMC snap-in</system>. First you must add the server to the console. To do this, right-click the <ui>Servers</ui> node and then click <ui>Add Server</ui>. Next, type the name of the server you want to add, or select it in the list. The server will be added to the left pane in the console, and you can perform any task by selecting it just as you would select the local server.</para>
                            </listItem>
                            <listItem>
                              <para>
                                <system>Using WDSUTIL</system>. To specify a remote server to run a WDSUTIL command, append <system>/Server:&lt;name&gt;</system> to the command. For example:</para>
                              <para>
                                <system>WDSUTIL /Add-Image /ImageFile:C:\images\capture.wim /Server:MY-WDS-02 /ImageType:Boot</system>
                              </para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                      <tr>
                        <TD colspan="1">
                          <para>Managing from a remote server that is running Windows Server 2008 (but not Windows Deployment Services)</para>
                        </TD>
                        <TD colspan="1">
                          <para>To do this, you can install Remote Server Administration Tools, which will install WDSUTIL and the Windows Deployment Services MMC snap-in on the server. To install Remote Server Administration Tools, open <ui>Server Manager</ui>, right-click the <ui>Features</ui> node, click <ui>Add Features</ui>, and then click <ui>Remote Server Administration Tools</ui>. Next click  <ui>Role Administration Tools</ui>, and then click <ui>Windows Deployment Services Tools</ui>.</para>
                        </TD>
                      </tr>
                      <tr>
                        <TD colspan="1">
                          <para>Using PsExec</para>
                        </TD>
                        <TD colspan="1">
                          <para>You can also manage the server by using PsExec. For example: <system>psexec \\&lt;servername&gt; \wdsutil /get-device /id:&lt;GUID&gt;</system></para>
                          <para>For information about using PsExec, see <externalLink><linkText>http://go.microsoft.com/fwlink/?LinkId=110605</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=110605</linkUri></externalLink>.</para>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_configure">
                <title>To configure Windows Deployment Services</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Install Windows Deployment Services. For more information, see the <externalLink><linkText>Windows Deployment Services Getting Started Guide</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=84628</linkUri></externalLink>.</para>
                            </listItem>
                            <listItem>
                              <para>Click <ui>Start</ui>, click<ui> Administrative  Tools</ui>, and then click <ui>Windows Deployment Services</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>In the left pane of the Windows Deployment Services snap-in, right-click the server and then click <ui>Configure Server</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Follow the instructions in the wizard.</para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Install Windows Deployment Services. For more information, see the <externalLink><linkText>Windows Deployment Services Getting Started Guide</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=84628</linkUri></externalLink>.</para>
                            </listItem>
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, click <ui>Run as administrator</ui>, and then run <codeInline>WDSUTIL /Verbose /Progress /Initialize-Server /RemInst:&lt;path&gt;</codeInline>, where &lt;path&gt; is the path where you would like the RemoteInstall folder to be located.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_startstop">
                <title>To start or stop the server</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Right-click the server, and then click <ui>All Tasks</ui>. </para>
                            </listItem>
                            <listItem>
                              <para>Click <ui>Stop Server</ui> or <ui>Start Server</ui>.</para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Start-Server</codeInline> or <codeInline>WDSUTIL /Stop-Server</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_enable">
                <title>To enable the server</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Enable-Server</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_logging">
                <title>To enable logging for the Windows Deployment Services client </title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>To turn on client logging, run <codeInline>WDSUTIL /Set-Server /WDSClientLogging /Enabled:Yes</codeInline>. </para>
                            </listItem>
                            <listItem>
                              <para>To change which events are logged, run <codeInline>WDSUTIL /Set-Server /WDSClientLogging /LoggingLevel:{None|Errors|Warnings|Info}</codeInline> (each category includes all events from the previous categories).</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_rpcport">
                <title>To choose the port number for RPCs</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /RPCPort:X</codeInline>, where X is the RPC port number you want to use.</para>
                            </listItem>
                            <listItem>
                              <para>You must restart the service before the changes will take effect. To do this, run <codeInline>wdsutil /stop-server</codeInline> and then run <codeInline>wdsutil /start-server</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <alert class="note">
                    <para>If this remote procedure call (RPC) port is changed from the default value, you must add a firewall exception for the new RPC port.</para>
                  </alert>
                </content>
              </section>
              <section address="BKMK_nic">
                <title>To specify the network interfaces for Windows Deployment Services to listen on</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Do one of the following:</para>
                              <list class="bullet">
                                <listItem>
                                  <para>To add an interface to the list, run <codeInline>WDSUTIL /Set-Server /BindPolicy /Add /Address:&lt;IP or MAC address&gt; /AddressType:{IP|MAC}</codeInline>. </para>
                                </listItem>
                                <listItem>
                                  <para>To bind to only the interfaces on the list, run <codeInline>WDSUTIL /Set-Server /BindPolicy /Policy:Include</codeInline>. </para>
                                </listItem>
                                <listItem>
                                  <para>To bind to all interfaces other than those on the list, run <codeInline>WDSUTIL /Set-Server /BindPolicy /Policy:Exclude</codeInline>. </para>
                                </listItem>
                              </list>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_refresh">
                <title>To configure how often the server refreshes its settings</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /RefreshPeriod:&lt;time in seconds&gt;</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_risfolder">
                <title>To force the server to update files in the RemoteInstall folder</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Update-ServerFiles</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section address="BKMK_netpro">
                <title>To configure the network profile for the <?Comment SDA: Confirm this is still required 2013-04-30T10:24:00Z  Id='0?>server<?CommentEnd Id='0'
    ?></title>
                <content>
                  <para />
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Right-click the server, and then click <ui>Properties</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>On the <ui>Network Settings</ui> tab under <ui>Network Profile</ui>, select the option that specifies the network speed of your organization. </para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server [/Server:&lt;name&gt;] /Transport /Profile:{10Mbps|100Mbps|1Gbps|Custom}</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                  <alert class="important">
                    <para>You should not modify the other profiles that are provided. Instead, you should create a custom profile even if you want to change only one setting.</para>
                  </alert>
                </content>
              </section>
            </sections>
          </section>
          <section address="BKMK_dhcp">
            <title>DHCP</title>
            <content />
            <sections>
              <section>
                <title>To configure Windows Deployment Services to run on the same computer as Microsoft DHCP</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Right-click the server, and then click <ui>Properties</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>On the <ui>DHCP</ui> tab, select <ui>Do not listen on port 67</ui> and <ui>Configure DHCP Option 60 to PXEClient</ui> (<?Comment tjg:  2013-04-30T11:45:00Z  Id='2?>for Windows Server 2008 R2, this option is labeled “Configure DHCP option 60 to indicate that this server is also a PXE server”<?CommentEnd Id='2'
    ?>).</para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section>
                <title>To configure Windows Deployment Services to run on the same computer as non-Microsoft DHCP</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Right-click the server, and then click <ui>Properties</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>On the <ui>DHCP</ui> tab, select <ui>Do not listen on port 67</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Use your DHCP server tools to set the option 60 tag to PXEClient.</para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /UseDHCPPorts:No</codeInline>.</para>
                            </listItem>
                            <listItem>
                              <para>Use your DHCP server tools to set the option 60 tag to PXEClient.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section>
                <title>To turn on the DHCP authorization requirement</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <para>N/A</para>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /RogueDetection:Yes</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
              <section>
                <title>To authorize the server in DHCP</title>
                <content>
                  <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
                    <thead>
                      <tr>
                        <TD colspan="1">
                          <para>Using the MMC</para>
                        </TD>
                        <TD colspan="1">
                          <para>Using WDSUTIL</para>
                        </TD>
                      </tr>
                    </thead>
                    <tbody>
                      <tr>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Ensure that you are a domain administrator in the root domain of the forest or an enterprise administrator. </para>
                            </listItem>
                            <listItem>
                              <para>Right-click the server, and then click <ui>Properties</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>On the <ui>Advanced</ui> tab, select <ui>Authorize the Windows Deployment Server in DHCP</ui>.</para>
                            </listItem>
                          </list>
                        </TD>
                        <TD colspan="1">
                          <list class="ordered">
                            <listItem>
                              <para>Ensure that you are a domain administrator in the root domain of the forest or an enterprise administrator. </para>
                            </listItem>
                            <listItem>
                              <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                            </listItem>
                            <listItem>
                              <para>Run <codeInline>WDSUTIL /Set-Server /Authorize:Yes</codeInline>.</para>
                            </listItem>
                          </list>
                        </TD>
                      </tr>
                    </tbody>
                  </table>
                </content>
              </section>
            </sections>
          </section>
          <section address="BKMK_clientreq">
            <title>Client requests</title>
            <content>
              <para />
            </content>
          </section>
          <section address="BKMK_clientboot">
            <title>Client boot settings</title>
            <content>
              <para />
            </content>
          </section>
          <section address="BKMK_adds">
            <title>AD DS settings</title>
            <content>
              <para />
            </content>
          </section>
          <section address="BKMK_unattend">
            <title>Unattend file configuration</title>
            <content>
              <para />
            </content>
          </section>
        </sections>
      </section>
      <section address="BKMK_wdscmgmt">
        <title>Computer Management Tasks</title>
        <content>
          <para />
        </content>
      </section>
      <section address="BKMK_wdsimgmt">
        <title>Image Management Tasks</title>
        <content>
          <para />
        </content>
      </section>
      <section address="BKMK_wdsbcdedit">
        <title>How to use Bcdedit to Modify the BCD File</title>
        <content>
          <para />
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>