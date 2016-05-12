---
title: WDS: Managing and Deploying Driver Packages
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88541bde-edd9-43c1-94a1-b2d20e879e45
---
# WDS: Managing and Deploying Driver Packages
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>You can use Windows Deployment Services to add driver packages to the server and configure them to be deployed to client computers along with the install image. The following sections will guide you through this process:  </para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="#term">Terminology reference</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#choosing">Choosing a scenario</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#pre">Prerequisites</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#scen1">Scenario 1: Deploy Driver Packages Based on the Plug and Play Hardware of the Client</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#scen2">Scenario 2: Deploy Driver Packages Using Filters to Define Which Clients Have Access to Each Driver Group</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#scen3">Scenario 3: Deploy All Driver Packages in a Driver Group to Clients</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#scen4">Managing Driver Groups and Driver Packages</link>
        </para>
      </listItem>
      <listItem>
        <para>
          <link xlink:href="#boot">Adding Driver Packages to Boot Images</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="term">
    <title>Terminology reference</title>
    <content>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Term</para>
            </TD>
            <TD>
              <para>Definition</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Driver group</para>
            </TD>
            <TD>
              <para>A driver group is a collection of driver packages. You can add filters to a driver group to make the packages in the group available to a select group of client computers. Alternatively, if there are no filters on a driver group, then the packages will be available to all clients that have matching hardware. You can define whether clients that have access to the driver group install either 1) all the packages in the group, or 2) only those packages that match the hardware that is connected to or installed on the client (that is, Plug and Play hardware).</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Filters</para>
            </TD>
            <TD>
              <para>Filters enable you to map the packages in a driver group to specific client computers. The filters define which clients have access to the packages. There are two types of filters: filters based on the hardware of the client (for example, manufacturer and BIOS vendor) and filters based on the attributes of the install image that is selected on the client (for example, the version or edition of the image). </para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Plug and Play hardware</para>
            </TD>
            <TD>
              <para>Plug and Play functionality provides automatic configuration of hardware and devices for Windows operating systems.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="choosing">
    <title>Choosing a Scenario</title>
    <content>
      <para>You can configure the driver packages to be deployed to clients in three ways. The following table describes each of these methods and describes when you should use each.</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>Scenario</para>
            </TD>
            <TD>
              <para>Description</para>
            </TD>
            <TD>
              <para>When To Use This Scenario</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>Scenario 1: Deploy driver packages to clients based on the Plug and Play hardware of the client</para>
            </TD>
            <TD>
              <para>In this scenario, you make all packages available to all clients (that is, you do not add filters to your driver groups), and you configure the groups so that only those packages that match the hardware on the computer will be installed. </para>
            </TD>
            <TD>
              <para>This is the simplest scenario to configure, and most companies should try this scenario first. However, if you encounter problems because incompatible packages are installed simultaneously on a computer (for example, if you have computers that cannot boot, or hardware that does not work correctly), then you will need to add filters to your driver groups as defined in Scenario 2.</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Scenario 2: Deploy driver packages using filters to define which clients have access to each driver group</para>
            </TD>
            <TD>
              <para>In this scenario, you organize your packages into driver groups, and then map each group to computers using filters. The filters define which computers have access to the driver group based on the hardware of the computer and/or the attributes of the selected install image. You can still configure the packages to be installed based on Plug and Play hardware, but you can use the filters to further define which clients will have access to the packages.</para>
            </TD>
            <TD>
              <para>You should consider using this scenario if:</para>
              <list class="bullet">
                <listItem>
                  <para>Scenario 1 is resulting in hardware that does not work correctly on a computer.</para>
                </listItem>
                <listItem>
                  <para>You have a complex environment including computers with various hardware and software configurations.</para>
                </listItem>
                <listItem>
                  <para>You need to install specific driver packages on certain computers (for example, computers with different languages or versions of an install image). </para>
                </listItem>
              </list>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>Scenario 3: Deploy all driver packages in a driver group to clients</para>
            </TD>
            <TD>
              <para>In this scenario, you deploy all of the driver packages in a driver group to a client computer (not just those that match the Plug and Play hardware on the client). After the installation, when you connect the hardware to the client, the device driver will be installed automatically.</para>
            </TD>
            <TD>
              <para>Use this option if you have hardware that is disconnected from the computer (for example, a printer or scanner) and you want to force all of the packages in a driver group to be installed on the client. Typically, you should use this scenario in combination with either Scenario 1 or 2.</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <section address="pre">
    <title>Prerequisites</title>
    <content>
      <para>The following are prerequisites for all three of the scenarios:</para>
      <list class="bullet">
        <listItem>
          <para>A Windows Deployment Services server configured with the following:</para>
          <list class="bullet">
            <listItem>
              <para>The boot image from either <token>winblue_client_Token>, <token>winblue_server_Token>, <token>win8_client_Token>, <token>win8_server_Token> Windows 7 or Windows Server 2008 R2 (from \Sources\Boot.wim on the DVD).</para>
            </listItem>
            <listItem>
              <para>Install images for <token>winblue_client_Token>, <token>winblue_server_Token>, <token>win8_client_Token>, <token>win8_server_Token>, Windows Server 2008, Windows 7, or Windows Server 2008 R2. </para>
            </listItem>
          </list>
        </listItem>
        <listItem>
          <para>Driver packages for the hardware that you want to deploy. Note that these packages must be extracted (that is, the package cannot be a .msi or .exe file).</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="scen1">
    <title>Scenario 1: Deploy Drivers Based on the Plug and Play Hardware of the Client
</title>
    <content>
      <para>In this scenario, you make all packages available to all clients (that is, you do not add filters to your driver groups) and you configure the groups so that only those packages that match the hardware on the computer will be installed. 
</para>
      <alert class="important">
        <para>You should thoroughly test this scenario before implementing it across your organization. </para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Known issues</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>Depending on the driver packages on the server and the hardware of the client, this scenario could result in a computer that will not boot. If this happens, you will need to figure out which driver packages are causing the problem and either remove them from the server, or restrict them using filters as outlined in Scenario 2. </para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <content>
          <procedure>
            <title>To add packages and configure the server</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open the Windows Deployment Services MMC snap-in.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Expand the <ui>Servers</ui> node and the node for your Windows Deployment Services server.  </para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click the <ui>Drivers</ui> node and click <ui>Add Driver Package</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Follow the instructions in the wizard to add the driver packages. When asked which driver group to add the packages to, click <ui>Select an existing driver group</ui>, and ensure that <ui>DriverGroup1</ui> is selected. This driver group (by default) is configured as follows: 1) it has no filters so all clients will have access to the packages in this group and 2) only packages that match the client’s hardware will be installed. To view these settings, right-click <ui>DriverGroup1</ui>, and click <ui>Properties</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>On the last page of the wizard, do not select the check box to modify the filters for the group, and click <ui>Finish</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Repeat steps 3-5 until you have added all of your driver packages to <ui>DriverGroup1</ui>.</para>
                  <alert class="note">
                    <para>If you would prefer to organize your packages into different driver groups, you can create driver groups when adding packages. However, you should not add any filters to them for this scenario. </para>
                  </alert>
                  <para>The server is now configured, so all computers that install a supported image will have access to this driver group. However, computers will only install those packages that match the Plug and Play hardware. You can now install an image as described in the next procedure.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <procedure>
            <title>To install the driver packages and an install image</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Ensure that all hardware (for which you want packages to be installed) is connected to client computers.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Boot a client computer and install an image.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>When the installation is complete, open <ui>Device Manager</ui> on the client computer and verify that the device drivers for all connected hardware were installed.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="scen2">
    <title>Scenario 2: Deploy Drivers Using Filters to Define Which Clients Have Access to Each Driver Group</title>
    <content>
      <para>This scenario is not as simple as Scenario 1 in that it will require you to test your configuration until the filters are configured appropriately for your environment. You may need to create many driver groups with different filter combinations before you find a configuration that works for you. In general, the more complex your environment is, the more complex your configuration will need to be. </para>
    </content>
    <sections>
      <section>
        <title>Known issues</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>The filter value must exactly match the client hardware or the install image specifications. The two available operators for most filters are <system>Equal to</system> or <system>Not equal to</system>. Therefore, if the value you specify is one character off (for example, if you omit a period) the filters will not filter the clients as intended. For this reason, we recommend that you create multiple filters to account for all cases. For example, create filters for <system>Fabrikam, Inc. </system> and <system>Fabrikam</system> and so on.</para>
            </listItem>
            <listItem>
              <para>When searching through the packages using the MMC snap-in to perform a task (for example, to delete a package), the dialog may be briefly unresponsive if you have hundreds of packages on your server. In these cases, note that you should continue to wait because the server is working on your request. For this reason we recommend that you add no more than 2000 driver packages to a group at time (although there is not an enforced limit).</para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title>Steps for deploying driver packages using filters</title>
        <content>
          <para>The first step in this scenario is to create driver groups that have filters. The filters define which computers should have access to the driver packages in that group. You can configure packages to be installed based on the hardware of the client (for example, the manufacturer or BIOS vendor) and the attributes of the Windows image that is selected during the installation (for example, the version or edition). For example, you could specify that the only client computers that should have access to a group are those that 1) are manufactured by Fabrikam, Inc. and 2) select a Windows 8 image during the installation. Once you have your driver groups configured, you will add packages to them, and then you will be ready to boot a computer and install an operating system. </para>
          <procedure>
            <title>To create driver groups with filters</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Open the Windows Deployment Services MMC snap-in. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>Expand the <ui>Servers</ui> node and the node for your Windows Deployment Services server.  </para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click <ui>DriverGroup1</ui> and click <ui>Disable</ui>. You must disable DriverGroup1 because (by default) it does not have filters on it and therefore, it will deploy all packages to all clients.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click the <ui>Drivers</ui> node and click <ui>Add Driver Group</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Type a name for the group, click <ui>Next</ui>, and follow the instructions to add filters as appropriate for your organization. For a list of filters, see Driver Group Filters (<externalLink><linkText>http://go.microsoft.com/fwlink/?LinkID=155158</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=155158</linkUri></externalLink>). </para>
                </content>
              </step>
              <step>
                <content>
                  <para>On the <ui>Packages to Install</ui> screen, select <ui>Install only the driver packages that match a client’s hardware</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Click <ui>Next</ui> and then click <ui>Finish</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Repeat steps 3-6 until you have created and configured all desired driver groups.</para>
                </content>
              </step>
            </steps>
          </procedure>
          <para>Now that you have configured your driver groups, you are ready to add driver packages to them as described in the next procedure.</para>
          <procedure>
            <title>To add driver packages to the driver groups</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>For packages that you have not already added to the server, right-click the <ui>Drivers</ui> node, click <ui>Add Driver Package</ui>, and follow the instructions to add the package to one of the groups that you created in the previous procedure.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>For packages that are already on the server but are not in the correct group, right-click the desired driver group, and click <ui>Add Driver Packages to this Group</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Use the search attributes to search through the packages that are on the server, and then click <ui>Add</ui> to add them to the group. </para>
                  <alert class="note">
                    <para>To add a specific package to a group, you can also right-click the package and click <ui>Add or Remove from Groups</ui>. In the dialog, configure the driver package using the arrows, and then click <ui>Apply</ui>.</para>
                  </alert>
                </content>
              </step>
              <step>
                <content>
                  <para>Repeat steps 1-3 until you have added all the packages that you want, and click <ui>Close</ui>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>If you need to remove a package from a group, click the group, right-click the specific driver package in the right pane. Then you can click <ui>Add or Remove from Groups</ui> to see a list of groups that you can add it to or remove it from. You can also click <ui>Remove from this Group</ui> to remove it instantly. To delete the package from the server, right-click the package and click <ui>Delete</ui>. </para>
                </content>
              </step>
            </steps>
          </procedure>
          <para>Now that you have configured driver groups and added packages to them, you are ready to boot a client as described in the following procedure.</para>
          <procedure>
            <title>To install the driver packages and an install image</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Ensure that all hardware (that you want the driver packages to be installed for) is connected to client computers.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Boot a computer and install an image.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>When the installation is complete, open <ui>Device Manager</ui> on the client computer from the Control Panel and verify that the appropriate device drivers were installed.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <section address="scen3">
    <title>Scenario 3: Deploy All Driver Packages in a Driver Group to Clients</title>
    <content>
      <para>You can configure any driver group so that <placeholder>all</placeholder> of the packages within it will be deployed to applicable clients—not only those for which hardware is connected to the client. To configure a driver group in this way, use the following procedure. </para>
      <alert class="important">
        <para>Depending on the driver packages on the server and the hardware of the client, this scenario could result in a computer that will not boot. If this happens, you will need to figure out which driver packages are causing the problem and either remove them from the server, or restrict them using filters as outlined in Scenario 2. </para>
      </alert>
      <procedure>
        <title>To install all packages to applicable clients</title>
        <steps class="ordered">
          <step>
            <content>
              <para>Open the Windows Deployment Services MMC snap-in. </para>
            </content>
          </step>
          <step>
            <content>
              <para>Right-click the driver group, and click <ui>Properties</ui>. </para>
            </content>
          </step>
          <step>
            <content>
              <para>Under <ui>Applicability</ui>, select <ui>All driver packages in the group</ui> from the drop-down menu.</para>
            </content>
          </step>
          <step>
            <content>
              <para>Boot a client computer and install an image.</para>
            </content>
          </step>
          <step>
            <content>
              <para>When the installation is complete, connect the Plug and Play hardware to the client computer and verify that Windows finds the device driver for it.</para>
            </content>
          </step>
        </steps>
      </procedure>
    </content>
  </section>
  <section address="scen4">
    <title>Managing Driver Groups and Driver Packages</title>
    <content>
      <para>In general, you can manage your driver groups and packages by right-clicking the <ui>Drivers</ui> node, a driver group, or a specific package. Then, you can select one of the available tasks such as adding, deleting, or enabling the item. For a list of the attribute you use to perform these tasks, see Driver Package Attributes (<externalLink><linkText>http://go.microsoft.com/fwlink/?LinkId=155167</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=155167</linkUri></externalLink>).</para>
    </content>
  </section>
  <section address="boot">
    <title>Adding Driver Packages to Boot Images</title>
    <content>
      <para>You can use Windows Deployment Services to add driver packages (such as network adapter drivers, mass storage drivers, and bus drivers) to your <token>winblue_client_Token>, <token>winblue_server_Token>, <token>win8_client_Token>, <token>win8_server_Token>, <token>nextref_client_Token> and <token>nextref_server_Token> boot images. This means that you do not have to export the image, use the tools in the Windows Automated Installation Kit to add driver packages manually, and then add the updated boot image.</para>
    </content>
    <sections>
      <section>
        <title>Known issues</title>
        <content>
          <list class="bullet">
            <listItem>
              <para>You should only add <placeholder>necessary</placeholder> driver packages to boot images (that is, network adapter drivers, mass storage drivers, and system bus drivers). We recommend this because it will reduce the size of the image, and also to reduce the chances that drivers collide with each other. </para>
            </listItem>
          </list>
        </content>
      </section>
      <section>
        <title />
        <content>
          <para />
          <procedure>
            <title>To add driver packages to a boot image using the Windows interface</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Add the driver package to the server. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>In the Windows Deployment Services MMC snap-in, expand the <system>Boot Images</system> node. It is okay if the image that you are updating is currently being downloaded to a client when you perform this procedure. Windows Deployment Services ensures that the client will get a consistent copy of the file.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Right-click the image that you want to add the driver to, and click <system>Add Driver Packages to Image</system>. </para>
                </content>
              </step>
              <step>
                <content>
                  <para>Follow the instructions in the wizard to search for the package and then add it to the image. </para>
                </content>
              </step>
            </steps>
          </procedure>
          <alert class="note">
            <para>When adding driver packages to boot images using WDSUTIL, you must specify <system>/filtertype:packagearchitecture /operator:equal /value:&lt;arch&gt;</system> where &lt;arch&gt; matches the architecture of the boot image. For example, run <system>WDSUTIL /verbose /progress /add-imagedriverpackageImage:"Microsoft Windows Setup (x64)Imagetype:boot /architecture:x64 /filtertype:packagearchitecture /operator:equal /value:x64</system>. If you do not specify this command and the package contains packages that do not match the architecture of the image, the command will fail.  </para>
          </alert>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>

