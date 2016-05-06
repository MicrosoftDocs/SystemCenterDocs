---
title: WDS: Working with Images
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497f5b73-b795-41d7-a801-6d8cc5fdbf6c
---
# WDS: Working with Images
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>This topic contains information about the images that you use with Windows Deployment Services. Windows Deployment Services uses two basic image types, both of which use the Windows Image (.wim) file format:</para>
    <list class="bullet">
      <listItem>
        <para>
          <system>Install image</system>: The operating system image that you deploy to the client computer. To create install images using Windows Deployment Services, you must first create a capture image.</para>
      </listItem>
      <listItem>
        <para>
          <system>Boot image</system>: The Microsoft Windows Preinstallation Environment (Windows PE) image that you boot a client into before you install the install image. To install an operating system, you first boot the computer into the boot image, and then you select the install image to install. You can also create two additional types of boot images:</para>
        <list class="bullet">
          <listItem>
            <para>
              <system>Capture image</system>: A type of boot image that you boot a client computer into to capture the operating system as a .wim file. You must first create a capture image when you are creating custom install images. </para>
          </listItem>
          <listItem>
            <para>
              <system>Discover image</system>: A type of boot image that you can use to install an operating system on a computer that is not Pre-Boot Execution Environment (PXE) enabled. When you boot a computer into a discover image, a Windows Deployment Services server will be located, and then you can choose the install image you want to install. </para>
          </listItem>
        </list>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_2" DoNotNumber="false">
    <title>Boot Images</title>
    <content>
      <para>These images contain Windows PE and the Windows Deployment Services client. The Windows Deployment Services client is Windows Vista Setup.exe with some additional functionality needed for network deployments. In most cases, you should use the standard boot image that is included on the operating system DVD (located at \Sources\boot.wim) without modification. </para>
    </content>
    <sections>
      <section address="Custom" DoNotNumber="false">
        <title>Creating Custom Boot Images</title>
        <content>
          <para>You can use the tools in the Windows Automated Installation Kit (AIK) to create custom boot images. You may want to create custom boot images for different tasks and architecture types. For example, you could have boot images that do the following:</para>
          <list class="bullet">
            <listItem>
              <para>Start Setup to install Windows.</para>
            </listItem>
            <listItem>
              <para>Reformat the hard disks to support BitLocker Drive Encryption (using unattend), and then install Windows. </para>
            </listItem>
            <listItem>
              <para>Contain the Windows Recovery Environment (Windows RE) that you want to use when a computer fails to start. </para>
            </listItem>
            <listItem>
              <para>Include a Windows PE image for administrators who want to perform other operations within Windows PE.</para>
            </listItem>
          </list>
          <para>To create custom boot image, use one of the following procedures:</para>
          <procedure>
            <title>To create a custom boot image using Windows PE 2.0 or 2.1</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Download the appropriate version of the Windows AIK.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Create a Windows PE build environment. For example: <codeInline>copype.cmd x86 c:\winpe_x86</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Mount the Windows PE image. For example: <codeInline>imagex /mountrw c:\winpe_x86\winpe.wim 1 c:\winpe_x86\mount</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Create a top-level folder named <system>Sources</system> in the \mount directory.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Obtain the Boot.wim from the product DVD and copy all of the files from the \Sources folder to the \Sources folder of your mounted image.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>As desired, add any Windows features, applications, or scripts that you want. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>If desired, remove any non-installed packages from the final image (to reduce the image size a minimal amount): <codeInline>peimg /prep c:\winpe_x86\mount\Windows</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Unmount and commit changes. For example: <codeInline>imagex /unmount c:\winpe_x86\mount /commit</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Now you are ready to add the custom boot image to the Windows Deployment Services server. </para>
                </content>
              </step>
            </steps>
          </procedure>
          <procedure>
            <title>To create a custom boot image using Windows PE 3.0</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Download the appropriate version of the Windows AIK.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Create a WinPE build environment. For example: <codeInline>copype.cmd x86 c:\winpe_x86</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Mount the .wim image using DISM. For example: <codeInline>dism /mount-wim /wimfile:c:\winpe_x86\winpe.wim /index:1 /mountdir: c:\winpe_x86\mount</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Add the following components using the DISM /AddPackage option.</para>
                  <list class="ordered">
                    <listItem>
                      <para>Setup package: <codeInline>disImage:c:\winpe_x86\mount /add-package:”&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE_FPs\winpe-setup.cab”</codeInline></para>
                    </listItem>
                    <listItem>
                      <para>Setup branding: <codeInline>disImage:c:\winpe_x86\mount /add-package:”&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE-FPs\winpe-setup-server.cab”</codeInline></para>
                      <alert class="note">
                        <para>You can also use the winpe-setup-client.cab instead as there is no difference between the files.</para>
                      </alert>
                    </listItem>
                    <listItem>
                      <para>Windows Deployment Services tools: <codeInline>disImage:”c:\winpe_x86\mount /add-package:&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE_FPs\winpe-wds-tools.cab”</codeInline></para>
                    </listItem>
                  </list>
                </content>
              </step>
              <step>
                <content>
                  <para>Add language packs for the above feature packs: </para>
                  <code>disImage:c:\winpe_x86\mount /add-package:&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE_FPs\&lt;lang&gt;\winpe-setup_&lt;lang&gt;.cab</code>
                  <code>disImage:c:\winpe_x86\mount /add-package:&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE_FPs\&lt;lang&gt;\winpe-setup-server_&lt;lang&gt;.cab</code>
                  <code>disImage:c:\winpe_x86\mount /add-package:&lt;path to WAIK&gt;\Tools\PETools\&lt;arch&gt;\WinPE_FPs\&lt;lang&gt;\winpe-wds-tools_&lt;lang&gt;.cab</code>
                </content>
              </step>
              <step>
                <content>
                  <para>Unmount and commit the changes: <codeInline>dism /unmount-wim /mountdir:c:\winpe_x86\mount /commit</codeInline></para>
                </content>
              </step>
              <step>
                <content>
                  <para>Now you are ready to add the custom boot image to the Windows Deployment Services server. </para>
                </content>
              </step>
            </steps>
          </procedure>
          <para>Note the following about creating custom boot images:</para>
          <list class="bullet">
            <listItem>
              <para>You can also make additional changes to the boot menu, using the Bcdedit.exe tool to edit the Default.bcd file located at %REMINST%\boot\&lt;architecture&gt;. For more information, see How to Modify the BCD Store Using Bcdedit (<externalLink><linkText>http://go.microsoft.com/fwlink/?LinkId=115267</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=115267</linkUri></externalLink>). </para>
            </listItem>
            <listItem>
              <para>The boot menu on x86-based computers will display only x86 boot images (because x86-based computers cannot run x64 boot images); however, if you boot into an x86-based boot image from an x64-based computer, x86-based and x64-based install images will be displayed. If you boot into an x64-based boot image from an x64-based computer, only x64-based boot images will be displayed.</para>
            </listItem>
            <listItem>
              <para>If you have a WinPESHL.ini file in the boot image, you need to create an entry in the WinPESHL.ini file to start Setup.exe in Windows Deployment Services mode. For more information, see “When Setup Is Started in Windows Deployment Services Mode” in How the Windows Deployment Services Client Works (<externalLink><linkText>http://go.microsoft.com/fwlink/?LinkID=147067</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=147067</linkUri></externalLink>). </para>
            </listItem>
          </list>
          <alert class="important">
            <para>When creating custom boot images, the version of Windows PE that you use must match or be newer than the install image. </para>
          </alert>
        </content>
      </section>
    </sections>
  </section>
  <section address="DiscoverImage" DoNotNumber="false">
    <title>Discover Images</title>
    <content>
      <para>Discover images are generally used in scenarios where the client cannot perform a network boot. These images enable a computer to locate a Windows Deployment Services server to install an image. To create a discover image, right-click a boot image in the MMC snap-in, and then click <ui>Create discover boot image</ui>. In most cases, you should use the Boot.wim file included on the operating system install media to create your image. For instructions, see the <externalLink><linkText>Windows Deployment Services Getting Started Guide</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=84628</linkUri></externalLink>.When you create a discover images, you configure one of the following:</para>
      <list class="bullet">
        <listItem>
          <para>
            <system>Static discovery</system>. Static discovery is when you specify the server that the computer should use when you create the discover image. Static discovery works well in data center environments or branch offices where DHCP may not be available. One major disadvantage of static discovery is that it introduces a single point of failure. For example, if the server that is specified is unavailable, Windows Deployment Services will not work, and there is no way to have the client try a different server. Another flaw is that static discovery does not allow for load balancing, because all clients using a particular boot image would use the specified server. </para>
        </listItem>
        <listItem>
          <para>
            <system>Dynamic discovery</system>. If you do not specify the server to use when you create a discover image, Windows Deployment Services will emulate a network boot request from within Windows PE. Based on the responses to that request, the client can locate a valid server and continue the installation process. </para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="Capture" DoNotNumber="false">
    <title>Capture Images</title>
    <content>
      <para>Capture images are a type of boot image that you boot a client computer into to capture the operating system as a .wim file. You must first create a capture image when you are creating custom install images. These images are an alternative to using ImageX. </para>
      <para>Capture images contain Windows PE and the Windows Deployment Services Image Capture Wizard. When you boot a computer (that has been prepared with Sysprep) into a capture image, the wizard creates an install image of the computer and saves it as a .wim file. Then you can upload the image to the Windows Deployment Services server or copy it to bootable media (CD, DVD, USB drive, and so on). You create capture images from existing boot images — most commonly, the Boot.wim file from the operating system install media. For instructions on creating these images, see the <externalLink><linkText>Windows Deployment Services Getting Started Guide</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=84628</linkUri></externalLink>. </para>
      <para>Capture images provide a subset of the functionality included in the <system>ImageX /capture</system> command. The following table compares these two tools.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD >
              <para>Functionality</para>
            </TD>
            <TD >
              <para>Image Capture Wizard</para>
            </TD>
            <TD >
              <para>ImageX</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD >
              <para>Captures a partial volume?</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Captures an image that has not been prepared by using Sysprep?</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Uploads directly to the Windows Deployment Services server?</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Can the process be automated?</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Has a GUI?</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Provides additional functionality beyond image capture?</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Enables me to specify a capture exclusion list?</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
          <tr>
            <TD >
              <para>Captures directly to a network location without making a local image copy?</para>
            </TD>
            <TD >
              <para>No</para>
            </TD>
            <TD >
              <para>Yes</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <para>Regardless of which tool you use (capture images or ImageX), the high-level process for capturing images remains essentially the same:</para>
      <list class="ordered">
        <listItem>
          <para>Install Windows on a reference computer. </para>
        </listItem>
        <listItem>
          <para>Perform customizations and install software.</para>
        </listItem>
        <listItem>
          <para>Run the correct version of Sysprep for the reference computer's operating system.</para>
        </listItem>
        <listItem>
          <para>Reboot into Windows PE.</para>
        </listItem>
        <listItem>
          <para>Capture the image into .wim format.</para>
        </listItem>
        <listItem>
          <para>Upload the image to the Windows Deployment Services server.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_custom" DoNotNumber="false">
    <title>Custom Discover or Capture Images</title>
    <content>
      <para>For advanced scenarios as part of a custom deployment solution, you can create discover or capture images manually by using the tools provided in the Windows AIK. </para>
      <procedure>
        <title>To create a discover or capture image manually</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Locate the boot image that you want to modify, and save it to a known location. This boot image can be either the custom boot image that you created in the “Creating Custom Boot Images” section, or the Boot.wim from the product DVD.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Mount the image using either DISM or ImageX.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Create a Winpeshl.ini file in the Windows\System32 folder of the custom boot image with one of the following sections.</para>
              <list class="bullet">
                <listItem>
                  <para>
                    <embeddedLabel>Capture Images</embeddedLabel>.</para>
                  <code>[LaunchApps]%SYSTEMROOT%\system32\wdscapture.exe</code>
                </listItem>
                <listItem>
                  <para>
                    <embeddedLabel>Discover Images</embeddedLabel>.</para>
                  <code>[LaunchApps]%SYSTEMROOT%\sources\setup.exe, "/wds /wdsdiscover"</code>
                  <para>or</para>
                  <code>[LaunchApps]%SYSTEMROOT%\sources\setup.exe, "/wds /wdsdiscover /wdsserver:&lt;server&gt;"</code>
                  <para>Note the following about the /wdsdiscover and /wdsserver options:</para>
                  <list class="bullet">
                    <listItem>
                      <para>
                        <embeddedLabel>/WDSDiscover</embeddedLabel>. (Default) Specifies that the Windows Deployment Services client should be in discover mode. If you do not specify /WDSServer with this option, Windows Deployment Services will search for a server.</para>
                    </listItem>
                    <listItem>
                      <para>
                        <embeddedLabel>/WDSServer:&lt;ServerName&gt;</embeddedLabel>. Specifies the name of the Windows Deployment Services server that the client should connect to. Note that <system>&lt;ServerName&gt;</system> can be an IP address, a NetBIOS name, or a fully qualified domain name (FQDN). You must also specify <system>/WDSDiscover</system>. </para>
                    </listItem>
                  </list>
                </listItem>
              </list>
            </content>
          </step>
          <step>
            <content>
              <para>Unmount and commit the changes using either DISM or ImageX.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Update the image metadata to reflect any changes to the image name or description.</para>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>

