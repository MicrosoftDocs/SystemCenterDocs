---
title: WDS: How to Manage Client Computers
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac91604f-229f-45ad-ac8e-e23e899369bf
---
# WDS: How to Manage Client Computers
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic contains procedures for the tasks that are listed and described in the following table.</para>
    <alert class="note">
      <para>Help for WDSUTIL is available by typing <system>WDSUTIL /?</system> at a command prompt or online at <externalLink><linkText>http://go.microsoft.com/fwlink/?LinkId=112194</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=112194</linkUri></externalLink>.</para>
    </alert>
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
              <link xlink:href="#BKMK_1">Prestage Computers</link>
            </para>
          </TD>
          <TD colspan="1">
            <list class="bullet">
              <listItem>
                <para>To prestage a client computer</para>
              </listItem>
              <listItem>
                <para>To prestage a client computer to boot from a different server</para>
              </listItem>
              <listItem>
                <para>To prestage a client computer to use a network boot program other than the default</para>
              </listItem>
              <listItem>
                <para>To prestage a client computer to use an unattend file other than the default for the Windows PE phase of unattended setup</para>
              </listItem>
              <listItem>
                <para>To prestage a client computer to use a boot image other than the default</para>
              </listItem>
              <listItem>
                <para>To prestage a client computer to join a domain</para>
              </listItem>
              <listItem>
                <para>To view the attributes of a prestaged client</para>
              </listItem>
            </list>
          </TD>
        </tr>
        <tr>
          <TD colspan="1">
            <para>
              <link xlink:href="#BKMK_3">Configure the Auto-Add Policy</link>
            </para>
          </TD>
          <TD colspan="1">
            <list class="bullet">
              <listItem>
                <para>To enable the Auto-Add policy</para>
              </listItem>
              <listItem>
                <para>To change the length of time approved computers are held in the Auto-Add database</para>
              </listItem>
              <listItem>
                <para>To change the length of time rejected and pending computers are held in the Auto-Add database </para>
              </listItem>
              <listItem>
                <para>To delete the rejected or approved computers table</para>
              </listItem>
            </list>
          </TD>
        </tr>
        <tr>
          <TD colspan="1">
            <para>
              <link xlink:href="#BKMK_2">Specify Settings for Pending Computers</link>
            </para>
          </TD>
          <TD colspan="1">
            <list class="bullet">
              <listItem>
                <para>To change the rate at which pending computers will poll the server</para>
              </listItem>
              <listItem>
                <para>To change the number of times pending computers will poll the server</para>
              </listItem>
              <listItem>
                <para>To change the message displayed to pending computers</para>
              </listItem>
              <listItem>
                <para>To set a default server for pending computers to boot from</para>
              </listItem>
              <listItem>
                <para>To set a default network boot program for pending computers</para>
              </listItem>
              <listItem>
                <para>To set a default unattend file for pending computers</para>
              </listItem>
              <listItem>
                <para>To set a default boot image for pending computers</para>
              </listItem>
              <listItem>
                <para>To set domain join options for pending computers</para>
              </listItem>
            </list>
          </TD>
        </tr>
        <tr>
          <TD colspan="1">
            <para>
              <link xlink:href="#BKMK_4">Approve and Reject Pending Computers</link>
            </para>
          </TD>
          <TD colspan="1">
            <list class="bullet">
              <listItem>
                <para>To view the table of computers that are pending approval</para>
              </listItem>
              <listItem>
                <para>To approve a pending computer by using the default settings</para>
              </listItem>
              <listItem>
                <para>To approve all pending computers by using the default settings</para>
              </listItem>
              <listItem>
                <para>To approve a pending computer, but change a setting</para>
              </listItem>
              <listItem>
                <para>To approve all pending computers, but change a setting</para>
              </listItem>
              <listItem>
                <para>To reject a pending computer</para>
              </listItem>
            </list>
          </TD>
        </tr>
      </tbody>
    </table>
  </introduction>
  <section address="BKMK_1">
    <title>Prestage Computers</title>
    <content />
    <sections>
      <section>
        <title>To prestage a client computer</title>
        <content>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD colspan="1">
                  <para>Using the Active Directory Users and Computers snap-in</para>
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
                      <para>On the server running Active Directory Users and Computers, open the Active Directory Users and Computers MMC snap-in (click <ui>Start</ui>, click <ui>Run</ui>, type <system>dsa.msc</system>, and then click <ui>OK</ui>).</para>
                      <alert class="note">
                        <para>To manage the server remotely, you can install “AD DS Snap-Ins and Command-Line Tools” in the Remote Server Administration Tools. To do this, click <ui>Add Features</ui> in Server Manager, and install the feature from the following location: <codeInline>Remote Server Administration Tools&gt;Remote Administration Tools&gt;AD DS and AD LDS Tools&gt;AD DS Tools&gt;AD DS Snap-Ins and Command-line Tools</codeInline>.</para>
                      </alert>
                    </listItem>
                    <listItem>
                      <para>In the console tree, right-click the organizational unit that will contain the new client computer.</para>
                    </listItem>
                    <listItem>
                      <para>Click <ui>New</ui>, and then click <ui>Computer</ui>. </para>
                    </listItem>
                    <listItem>
                      <para>Type the client computer name, click <ui>Next</ui>, and then click <ui>This is a managed computer</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>In the text box, type the client computer's MAC address preceded with twenty zeros or the globally unique identifier (GUID) in the format: {<placeholder>XXXXXXXX-XXXX-XXXX-XXX-XXXXXXXXXXXX</placeholder>}. </para>
                    </listItem>
                    <listItem>
                      <para>Click <ui>Next</ui>, and click one of the following options to specify which server or servers will support this client computer:</para>
                      <list class="bullet">
                        <listItem>
                          <para>
                            <ui>Any available remote installation server</ui>
                          </para>
                        </listItem>
                        <listItem>
                          <para>
                            <ui>The following remote installation server</ui>
                          </para>
                        </listItem>
                      </list>
                    </listItem>
                    <listItem>
                      <para>Click <ui>Next</ui>, and then click <ui>Finish</ui>.</para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Add-Device /Device:&lt;name&gt; /ID:&lt;GUIDorMACAddress&gt;</codeInline> where <codeInline>&lt;GUIDorMACAddress&gt;</codeInline> is the identifier of the new computer. If you use a MAC address, you must precede it with twenty zeros (0).</para>
                      <para>For example: <system>WDSUTIL /Add-Device /Device:Computer1  
</system>
</para>
                      <para>
                        <system>/ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6}</system>
                      </para>
                      <para>
                        <system>/ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com /WDSClientUnattend:WDSClientUnattend\unattend.xml</system>
                      </para>
                      <para>
                        <system>/User:Domain\MyUser /JoinRights:Full /BootImagePath:boot\x86\images\boot.wim /OU:"OU=MyOU,CN=Test,DC=Domain,DC=com"</system>
                      </para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To prestage a client computer to boot from a different server</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /ReferralServer:&lt;ServerName&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To prestage a client computer to use a network boot program other than the default</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /BootProgram:&lt;path&gt;</codeInline>, where <codeInline>&lt;path&gt;</codeInline> is the relative path to the boot program you want from the RemoteInstall folder.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To prestage a client computer to use an unattend file other than the default for the Windows PE phase of unattended setup</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /WDSClientUnattend:&lt;path&gt;</codeInline>, where the path is relative to the unattend file you want from the RemoteInstall folder.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To prestage a client computer to use a boot image other than the default</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /BootImagePath:&lt;path&gt;</codeInline>, where <codeInline>&lt;path&gt;</codeInline> is the relative path to the boot image you want from the RemoteInstall folder. </para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To prestage a client computer to join a domain</title>
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
                          <para>To enable the specified user to join the client computer to the specified domain once, run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /User:&lt;user&gt; /JoinRights:JoinOnly /JoinDomain:Yes /Domain:&lt;domain&gt; /ResetAccount</codeInline>, where:</para>
                          <para>
                            <codeInline>&lt;user&gt;</codeInline> is domain\user or user@domain</para>
                          <para>
                            <codeInline>&lt;name&gt;</codeInline> is the name of the computer</para>
                          <para>
                            <codeInline>&lt;domain&gt;</codeInline> is the name of the domain</para>
                        </listItem>
                        <listItem>
                          <para>To enable the specified user to join the client computer to the specified domain at any time, run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /User:&lt;user&gt; /JoinRights:Full /JoinDomain:Yes /Domain:&lt;domain&gt;</codeInline>.</para>
                        </listItem>
                        <listItem>
                          <para>To join the client computer to the specified domain without granting any user rights, run <codeInline>WDSUTIL /Set-Device /Device:&lt;name&gt; /JoinDomain:Yes /Domain:&lt;domain&gt;</codeInline>.</para>
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
      <section>
        <title>To view the attributes of a prestaged client</title>
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
                          <para>To view the prestaged client by name in the local domain, run <codeInline>WDSUTIL /Get-Device /Device:&lt;name&gt;</codeInline>. </para>
                        </listItem>
                        <listItem>
                          <para>To view a prestaged client by ID (GUID or MAC) in the local domain, run <codeInline>WDSUTIL /Get-Device /ID:&lt;ID&gt;</codeInline>. </para>
                          <alert class="note">
                            <para>To specify that the client is in a domain other than the local one, specify <codeInline>/Domain:&lt;domain&gt;</codeInline> with either of these commands.</para>
                          </alert>
                          <alert class="note">
                            <para> To search the entire AD DS forest, specify <codeInline>/Forest:Yes</codeInline> with either of these commands.</para>
                          </alert>
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
    </sections>
  </section>
  <section address="BKMK_3">
    <title>Configure the Auto-Add Policy</title>
    <content>
      <para>For more information about the Auto-Add policy, see Enabling the Auto-Add Policy at <externalLink><linkText>Prestaging Client Computers</linkText><linkUri>https://technet.microsoft.com/en-us/library/cc770832(v=ws.10).aspx</linkUri></externalLink></para>
    </content>
    <sections>
      <section>
        <title>To enable the Auto-Add policy</title>
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
                      <para>On the <ui>PXE Response settings</ui> tab, click <ui>Respond to all (known and unknown) client computers</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Select the check box <ui>For unknown clients, notify administrator and respond after approval</ui>.</para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /Policy:AdminApproval</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To change the length of time approved computers are held in the Auto-Add database</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /RetentionPeriod /Approved:&lt;time in days&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To change the length of time rejected and pending computers are held in the Auto-Add database</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /RetentionPeriod /Others:&lt;time in days&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To delete the approved or rejected computers table</title>
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
                      <para>Run <codeInline>WDSUTIL /Delete-AutoAddDevices /DeviceType:&lt;ApprovedDevices|RejectedDevices&gt;</codeInline>.</para>
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
  <section address="BKMK_2">
    <title>Specify Settings for Pending Computers</title>
    <content />
    <sections>
      <section>
        <title>To change the rate at which pending computers will poll the server</title>
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
                      <para>To set the time between polls, run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /PollInterval:&lt;time in seconds&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To change the number of times pending computers will poll the server</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /MaxRetry:&lt;retries&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To change the message displayed to pending computers</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddPolicy /Message:&lt;message&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To set a default server for pending computers to boot from</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddSettings /Architecture:{x86|x64|ia64} /ReferralServer:&lt;server name&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To set a default network boot program for pending computers</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddSettings /Architecture:{x86|x64|ia64} /BootProgram:&lt;path&gt;</codeInline>, where the <codeInline>&lt;path&gt;</codeInline> is relative to the RemoteInstall folder.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To set a default unattend file for pending computers</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddSettings /Architecture:{x86|x64|ia64} /WDSClientUnattend:&lt;path&gt;</codeInline>, where the path is relative to the RemoteInstall folder.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To set a default boot image for pending computers</title>
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
                      <para>Run <codeInline>WDSUTIL /Set-Server /AutoAddSettings /Architecture:{x86|x64|ia64} /BootImage:&lt;path&gt;</codeInline>, where <codeInline>&lt;path&gt;</codeInline> is relative to the RemoteInstall folder.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To set domain join options for pending computers</title>
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
                          <para>To enable the specified user (specified as domain\user or user@domain) to join the client computer to the specified domain once, run <codeInline>WDSUTIL /Set-Server /AutoAddSettings Architecture:{x86|x64|ia64} /User:&lt;user&gt; /JoinRights:JoinOnly /JoinDomain:Yes /Domain:&lt;domain&gt;</codeInline>.</para>
                        </listItem>
                        <listItem>
                          <para>To enable the specified user to join the client computer to the specified domain at any time, run <codeInline>WDSUTIL /Set-Server /AutoAddSettings Architecture:{x86|x64|ia64} /User:&lt;user&gt; /JoinRights:Full /JoinDomain:Yes /Domain:&lt;domain&gt;</codeInline>.</para>
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
    </sections>
  </section>
  <section address="BKMK_4">
    <title>Approve and Reject Pending Computers</title>
    <content />
    <sections>
      <section>
        <title>To view the list of computers that are pending approval</title>
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
                      <para>Expand the server node.</para>
                    </listItem>
                    <listItem>
                      <para>Select the <ui>Pending Devices </ui>node.</para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Get-AutoAddDevices /DeviceType:PendingDevices</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To approve a pending computer by using the default settings</title>
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
                      <para>Select the <ui>Pending Devices </ui>node.</para>
                    </listItem>
                    <listItem>
                      <para>Right-click the computer you want to approve, and then click <ui>Approve.</ui></para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Approve-AutoAddDevices /RequestID:&lt;ID&gt;</codeInline> with the ID obtained from the Auto-Add database.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To approve all pending computers by using the default settings</title>
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
                      <para>Right-click the <ui>Pending Devices</ui> node.</para>
                    </listItem>
                    <listItem>
                      <para>Click <ui>Approve All</ui>.</para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Approve-AutoAddDevices /RequestID:All</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To approve a pending computer, but change a setting</title>
        <content>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD colspan="1">
                  <para>Using the MMC (name change only)</para>
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
                      <para>Select the <ui>Pending Devices</ui> node.</para>
                    </listItem>
                    <listItem>
                      <para>Select the computer you want to approve.</para>
                    </listItem>
                    <listItem>
                      <para>On the <ui>Action</ui> menu, click <ui>Name and Approve</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>In the dialog box, type the name you want to give the computer.</para>
                    </listItem>
                  </list>
                </TD>
                <TD colspan="1">
                  <list class="ordered">
                    <listItem>
                      <para>Click <ui>Start</ui>, right-click <ui>Command Prompt</ui>, and click <ui>Run as administrator</ui>.</para>
                    </listItem>
                    <listItem>
                      <para>Run <codeInline>WDSUTIL /Approve-AutoAddDevices  /RequestID:&lt;ID&gt;</codeInline> with the ID obtained from the Auto-Add database</para>
                    </listItem>
                  </list>
                  <para>In addition, you can append this command with the following options:</para>
                  <list class="bullet">
                    <listItem>
                      <para>To change the name, specify <codeInline>/MachineName:&lt;name&gt;</codeInline> </para>
                    </listItem>
                    <listItem>
                      <para>To change the organizational unit (OU) where the account will be created, specify <codeInline>/OU:&lt;name of OU&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the user account for the domain join, specify <codeInline>/User:&lt;name&gt;</codeInline> where the name is domain\user or user@domain.</para>
                    </listItem>
                    <listItem>
                      <para>To enable the user to join this computer to the domain only once, specify <codeInline>/JoinRights:JoinOnly</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To enable the user to join this computer to the domain at any time, specify <codeInline>/JoinRights:Full</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To join this computer to the domain, specify <codeInline>/JoinDomain:Yes</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To direct the computer to install from a different Windows Deployment Services server, specify <codeInline>/ReferralServer:&lt;server name&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the network boot program used, specify <codeInline>/BootProgram:&lt;path&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the unattend file used for the Microsoft Windows Preinstallation Environment (Windows PE) phase of unattended setup, specify <codeInline>/WDSClientUnattend:&lt;path&gt;</codeInline>. </para>
                    </listItem>
                    <listItem>
                      <para>To change the boot image used, specify <codeInline>/BootImagePath:&lt;path&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To approve all pending computers, but change a setting</title>
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
                      <para>Run <codeInline>WDSUTIL /Approve-AutoAddDevices /RequestID:All</codeInline> </para>
                    </listItem>
                  </list>
                  <para>In addition, you can append this command with the following options:</para>
                  <list class="bullet">
                    <listItem>
                      <para>To change the OU where the accounts will be created, specify <codeInline>/OU:&lt;name of OU&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the user account used for domain join, specify <codeInline>/User:&lt;name&gt;</codeInline> where the name is domain\user or user@domain.</para>
                    </listItem>
                    <listItem>
                      <para>To allow the user to join these computers to the domain once only, specify <codeInline>/JoinRights:JoinOnly</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To allow the user to join these computers to the domain at any time, specify <codeInline>/JoinRights:Full</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To join these computers to the domain, specify <codeInline>/JoinDomain:Yes</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To direct the computers to install from a different Windows Deployment Services server, specify <codeInline>/ReferralServer:&lt;server name&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the network boot program used, specify <codeInline>/BootProgram:&lt;path&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the unattend file used for the Windows PE phase of unattended setup, specify <codeInline>/WDSClientUnattend:&lt;path&gt;</codeInline>.</para>
                    </listItem>
                    <listItem>
                      <para>To change the boot image used, specify <codeInline>/BootImagePath:&lt;path&gt;</codeInline>.</para>
                    </listItem>
                  </list>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>To reject a pending computer</title>
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
                      <para>Select the <ui>Pending Devices</ui> node.</para>
                    </listItem>
                    <listItem>
                      <para>Right-click the computer, and then click <ui>Reject </ui>or <ui>Reject All</ui>.</para>
                    </listItem>
                  </list>
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
                          <para>To reject a single computer, run <codeInline>WDSUTIL /Reject-AutoAddDevices /RequestID:&lt;ID&gt;</codeInline> with the ID obtained from the Auto-Add database. </para>
                        </listItem>
                        <listItem>
                          <para>To reject all computers, run <codeInline>WDSUTIL /Reject-AutoAddDevices /RequestID:All</codeInline>.</para>
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
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>

