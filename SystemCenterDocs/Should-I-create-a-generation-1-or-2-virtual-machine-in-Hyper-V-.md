---
title: Should I create a generation 1 or 2 virtual machine in Hyper-V?
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - hyper-v
  - techgroup-compute
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
robots: noindex,nofollow
---
# Should I create a generation 1 or 2 virtual machine in Hyper-V?
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This content is preliminary and subject to change.</para>
    <para>Your choice to create a generation 1 or generation 2 virtual machine will depend on which guest operating system you want to install and the boot method you want to use to deploy the virtual machine. We recommend that you create a generation 2 virtual machine to take advantage of features like Secure Boot unless one of the following statements is true:</para>
    <list class="bullet">
      <listItem>
        <para>The VHD you want to boot from is not <externalLink><linkText>UEFI-compatible</linkText><linkUri>http://technet.microsoft.com/library/hh824898.aspx</linkUri></externalLink>.</para>
      </listItem>
      <listItem>
        <para>You <externalLink><linkText>plan to move your virtual machine to Azure</linkText><linkUri>https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-questions/</linkUri></externalLink>.</para>
      </listItem>
      <listItem>
        <para>Generation 2 doesn’t support the operating system you want to run on the virtual machine.</para>
      </listItem>
      <listItem>
        <para>Generation 2 doesn’t support the boot method you want to use.</para>
      </listItem>
    </list>
    <para>You can’t change a virtual machine’s generation after you’ve created it. So review the following sections in this article to make sure the generation you pick supports the operating system, boot method, and features you want to use.</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_OS">Which guest operating systems are supported?</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Boot">How can I boot the virtual machine?</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Advantages">What are the advantages of using generation 2 virtual machines?</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_OS">
    <title>Which guest operating systems are supported?</title>
    <content>
      <para>Generation 1 virtual machines support most guest operating systems. Generation 2 virtual machines support most 64-bit versions of Windows and more current versions of Linux and FreeBSD operating systems. Use the following sections to see which generation of virtual machine will support the guest operating system you want to install.  </para>
      <list class="bullet">
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Windows">Windows guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_CentOS">CentOS and Red Hat Enterprise Linux guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Debian">Debian guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_FreeBSD">FreeBSD guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Oracle">Oracle Linux guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_SUSE">SUSE guest operating system support</link>
          </para>
        </listItem>
        <listItem>
          <para>
            <link xlink:href="02e31413-6140-4723-a8d6-46c7f667792d#BKMK_Ubuntu">Ubuntu guest operating system support</link>
          </para>
        </listItem>
      </list>
    </content>
    <sections>
      <section address="BKMK_Windows">
        <title>Windows guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for 64-bit versions of Windows as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>64-bit versions of Windows</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>
                    <token>winblue_server_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>win8_server_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Windows Server 2008 R2</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Windows Server 2008</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>winthreshold_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>winblue_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>win8_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Windows 7</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for 32-bit versions of Windows as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>32-bit versions of Windows</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>
                    <token>winthreshold_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>winblue_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>
                    <token>win8_client_./Token>
                  </para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Windows 7</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="b1ddf7cd-dab8-4cc0-bd32-528f8df97540">Generation 2 Virtual Machine Overview</legacyLink>.</para>
        </content>
      </section>
      <section address="BKMK_CentOS">
        <title>CentOS and Red Hat Enterprise Linux guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for versions of Red Hat Enterprise Linux (RHEL) and CentOS as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Operating system versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>RHEL/CentOS 7.x Series</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>RHEL/CentOS 6.x Series</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>RHEL/CentOS 5.x Series</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="4bf8783d-dee5-4b3e-8cce-2b11b117c189">CentOS and Red Hat Enterprise Linux virtual machines on Hyper-V</legacyLink>. </para>
        </content>
      </section>
      <section address="BKMK_Debian">
        <title>Debian guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for versions of Debian as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Operating system versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Debian 7.0-7.8</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="3cc62c10-02a3-4633-960c-23bf91a45bd5">Debian virtual machines on Hyper-V</legacyLink>. </para>
        </content>
      </section>
      <section address="BKMK_FreeBSD">
        <title>FreeBSD guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for versions of FreeBSD as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Operating system versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>FreeBSD 10 and 10.1</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>FreeBSD 9.1 and 9.3</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>FreeBSD 8.4</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="930e758f-bd50-46b4-a3a4-9857110f17b4">FreeBSD virtual machines on Hyper-V</legacyLink>.</para>
        </content>
      </section>
      <section address="BKMK_Oracle">
        <title>Oracle Linux guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for Red Hat Compatible Kernel Series versions as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Red Hat Compatible Kernel Series versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Oracle Linux 7.x Series</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Oracle Linux 6.6, 6.5, and 6.4</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for Unbreakable Enterprise Kernel versions as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Unbreakable Enterprise Kernel (UEK) versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Oracle Linux UEK R3 QU3</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Oracle Linux UEK R3 QU2</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Oracle Linux UEK R3 QU1</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="c02fdb5b-62f3-43cb-a190-ab74b3ebcf77">Oracle Linux virtual machines on Hyper-V</legacyLink>. </para>
        </content>
      </section>
      <section address="BKMK_SUSE">
        <title>SUSE guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for versions of SUSE as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Operating system versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>SUSE Linux Enterprise Server 12</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SUSE Linux Enterprise Server 11 SP3</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>SUSE Linux Enterprise Server 11 SP2</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Open SUSE 12.3</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="7ec0e14c-4498-4bd9-8fe6-b94260198efc">SUSE virtual machines on Hyper-V</legacyLink>. </para>
        </content>
      </section>
      <section address="BKMK_Ubuntu">
        <title>Ubuntu guest operating system support</title>
        <content>
          <para>The following table shows what generation 1 and generation 2 virtual machines support for versions of Ubuntu as guest operating systems.</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Operating system versions</para>
                </TD>
                <TD>
                  <para>Generation 1</para>
                </TD>
                <TD>
                  <para>Generation 2</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>Ubuntu 14.04 and later versions</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Ubuntu 12.04</para>
                </TD>
                <TD>
                  <para>✔</para>
                </TD>
                <TD>
                  <para>✖</para>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>For more information, see <legacyLink xlink:href="95ea5f7c-25c6-494b-8ffd-2a77f631ee94">Ubuntu virtual machines on Hyper-V</legacyLink>. </para>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_Boot">
    <title>How can I boot the virtual machine?</title>
    <content>
      <para>The following table shows which boot methods are supported by generation 1 and generation 2 virtual machines.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Boot method</para>
            </TD>
            <TD>
              <para>Generation 1</para>
            </TD>
            <TD>
              <para>Generation 2</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>PXE boot by using a standard network adapter</para>
            </TD>
            <TD>
              <para>✖</para>
            </TD>
            <TD>
              <para>✔</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>PXE boot by using a legacy network adapter</para>
            </TD>
            <TD>
              <para>✔</para>
            </TD>
            <TD>
              <para>✖</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Boot from a SCSI virtual hard disk (.VHDX) or virtual DVD (.ISO)</para>
            </TD>
            <TD>
              <para>✖</para>
            </TD>
            <TD>
              <para>✔</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Boot from IDE Controller virtual hard disk (.VHD) or virtual DVD (.ISO)</para>
            </TD>
            <TD>
              <para>✔</para>
            </TD>
            <TD>
              <para>✖</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Boot from floppy (.VFD) </para>
            </TD>
            <TD>
              <para>✔</para>
            </TD>
            <TD>
              <para>✖</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="BKMK_Advantages">
    <title>What are the advantages of using generation 2 virtual machines?</title>
    <content>
      <para>Here are some of the advantages you get when you use a generation 2 virtual machine: </para>
      <list class="bullet">
        <listItem>
          <para>
            <embeddedLabel>Secure Boot</embeddedLabel> – This is a feature that verifies the boot loader is signed by a trusted authority in the UEFI database to help prevent unauthorized firmware, operating systems, or UEFI drivers from running at boot time. Secure Boot is enabled by default for generation 2 virtual machines. If you need to run a guest operating system that’s not supported by Secure Boot, you can disable it after the virtual machine’s created.  For more information, see <legacyLink xlink:href="fa233171-694e-484f-95fe-1dea0ab2a310">Secure Boot</legacyLink>. </para>
          <para>To Secure Boot generation 2 Linux virtual machines, you need to choose the UEFI CA Secure Boot template when you create the virtual machine.</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Larger boot volume</embeddedLabel> - The maximum boot volume for generation 2 virtual machines is 64TB. This is the maximum disk size supported by a .VHDX. For generation 1 virtual machines, the maximum boot volume is 2TB for a .VHDX and 2040GB for a .VHD. For more information, see <legacyLink xlink:href="248806ae-6797-46d1-b1be-24cbf1bafba4">Hyper-V Virtual Hard Disk Format Overview</legacyLink>.</para>
        </listItem>
      </list>
      <para>For more information like a device support comparison and frequently asked questions, see <legacyLink xlink:href="b1ddf7cd-dab8-4cc0-bd32-528f8df97540">Generation 2 Virtual Machine Overview</legacyLink>.</para>
    </content>
  </section>
  <relatedTopics>
    <legacyLink xlink:href="b1ddf7cd-dab8-4cc0-bd32-528f8df97540">Generation 2 Virtual Machine Overview</legacyLink>
    <legacyLink xlink:href="990ff94a-30fb-434b-b4a2-3804a5245ba6">Linux and FreeBSD Virtual Machines on Hyper-V</legacyLink>
  </relatedTopics>
</developerConceptualDocument>

