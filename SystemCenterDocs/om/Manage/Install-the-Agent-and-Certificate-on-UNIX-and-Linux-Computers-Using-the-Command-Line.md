---
title: Install the Agent and Certificate on UNIX and Linux Computers Using the Command Line
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a0a10f3-b755-4a3a-b6e7-e2475dfae2f2
---
# Install the Agent and Certificate on UNIX and Linux Computers Using the Command Line
Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)] and [!INCLUDE[sc_threshold_1](../../includes/sc_threshold_1_md.md)], [!INCLUDE[scom_threshold_1](../../includes/scom_threshold_1_md.md)].

#### To install the agent on Red Hat Enterprise Linux and SUSE Linux Enterprise Server

1.  Transfer the agent \(`scx-<version>-<os>-<arch>.rpm`\) to the Linux server, type:

    `scx-<version>-<os>-<arch>.rpm`

2.  To install the package, type:

    `rpm -i scx-<version>-<os>-<arch>.rpm`

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `service omiserver status`

#### To install the agent on RPM based Universal Linux Servers \(Oracle and Centos\)

1.  Transfer the agent \(`scx-<version>-universalr-<arch>.rpm`\) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `rpm -i scx-<version>-universalr-<arch>.rpm`

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

#### To install the agent on DPKG\-based Universal Linux Servers \(Debian and Utuntu\)

1.  Transfer the agent \(`scx-<version>-universald-<arch>.rpm`\) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `dpkg -i scx-<version>-universald-<arch>.deb`

3.  To verify that the package is installed, type:

    `dpkg -l scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

#### To install the agent on Solaris

1.  Transfer the agent \(`scx-<version>-<os>-<arch>.pkg.Z`\) to the Solaris server, type:

    `scx-<version>-<os>-<arch>.pkg.Z`

2.  Run the following command:

    `uncompress scx-<version>-<os>-<arch>.pkg.Z`

3.  To install the package, type:

    `pkgadd -d scx-<version>-<os>-<arch>.pkg MSFTscx`

4.  To verify that the package is installed, type:

    `pkginfo –l MSFTscx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `svcs omiserver`

#### To install the agent on HP\-UX

1.  Transfer the agent \(`scx-<version>-<os>-<arch>.gz`\) to the HP server:

    `cp scx-<version>-<os>-<arch>.gz`

2.  To unzip the package, type:

    `gzip –d scx-<version>-<os>-<arch>.gz`

3.  To install the package, type:

    `swinstall –s /path/scx-<version>-<os>-<arch> scx`

4.  To verify that the package is installed, type:

    `swlist scx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `ps –ef|grep scx`

    Look for the following process in the list:

    `scxcimserver`

#### To install the agent on AIX

1.  Transfer the agent \(`scx-<version>-<os>-<arch>.gz`\) to the AIX server, type:

    `cp scx-<version>-<os>-<arch>.gz`

2.  To unzip the package, type:

    `gzip –d scx-<version>-<os>-<arch>.gz`

3.  To install the package, type:

    `/usr/sbin/installp -a -d scx-<version>-<os>-<arch> scx`

4.  To verify that the package is installed, type:

    `swlist scx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `ps –ef|grep omi`

    Look for the following process in the list:

    omiserver

## Signing Agent Certificates
When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard, deployment and certificate signing. Then, you use the Discovery Wizard to add the computer to the Operations Manager database.

If there are existing certificates on the system, they are reused during agent installation. New certificates are not created. Certificates are not automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the `/etc/opt/microsoft/scx/ssl` folder. To regenerate the certificates at install, you must remove this folder before agent installation.

You must have already manually installed an agent before you start this procedure. You will need a root or elevated account to perform the procedure.

#### To install certificates for UNIX and Linux support

1.  On the computer that is running the UNIX or Linux operating system, locate the file `/etc/opt/microsoft/scx/ssl/scx-host-<hostname>.pem` and securely copy or transfer it to any location on the computer that is hosting [!INCLUDE[om12short](../../includes/om12short_md.md)].

2.  On the computer that is hosting [!INCLUDE[om12short](../../includes/om12short_md.md)], on the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd**, and then press **Enter**.

4.  Change directories to the location where you copied the `pem` file.

5.  Type the command `scxcertconfig -sign scx-host-<hostname>.pem scx_new.pem`, and then press **Enter**. This command will self\-sign your certificate \(`scx-host-<hostname>.pem`\) and then save the new certificate \(`scx-host-<hostname>_new.pem`\).

    > [!NOTE]
    > Ensure that the location where [!INCLUDE[om12short](../../includes/om12short_md.md)] is installed is in your path statement, or use the fully qualified path of the `scxcertconfig.exe` file.

6.  Securely copy or transfer the `scx_new.pem` file into the `/etc/opt/microsoft/scx/ssl` folder on the computer that is hosting the UNIX or Linux operating system. This replaces the `original scx-host-<hostname>.pem` file.

7.  Restart the agent by typing `scxadmin –restart`.

## <a name="bkmk_DiscoveringSystemsafterManualDeployment"></a>Discovering Computers after Manual Deployment
After you have manually deployed agents to UNIX and Linux computers, they still need to be discovered by Operations Manager by using the Discovery Wizard. For the **Discovery type**, select **Discover only computers with the UNIX\/Linux agent installed**. For more information see [Install the Agent Using the Discovery Wizard](Install-the-Agent-Using-the-Discovery-Wizard.md).


