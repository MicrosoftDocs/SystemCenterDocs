---
ms.assetid: 379b60d2-28f3-47d1-bf54-55409cd436ec
title: Install Agent and Certificate on UNIX and Linux Computers Using the Command Line
description: This article describes how to install the Operations Manager agent manually on UNIX and Linux computers.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 05/22/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Install agent and certificate on UNIX and Linux computers using the command line

>Applies To: System Center 2016 - Operations Manager

Your environment may require that you manually install the agent. Use the following procedures to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager 2016 - Operations Manager.  The agent packages can be found in the the following folder on a management server - *%ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\AgentManagement\UnixAgents\DownloadedKits* after you import  the required management packs for the specific version of UNIX/Linux you need to monitor.  The management pack are available in the Operations Manager installation media, in the *\ManagementPacks* directory or you can download the latest version from the [Download Center](https://www.microsoft.com/download/details.aspx?id=29696).

## To install the agent on Red Hat Enterprise Linux and SUSE Linux Enterprise Server

1.  Transfer the Red Hat Enterprise agent (`scx-<version>.rehl.<version>.<arch>.sh`) to the Linux server, type:

    `scx-<version>.rehl.<version>.<arch>.sh`  

    or for SUSE Linux Enterprise Server, type:  

    `scx-<version>.sles.<version>.<arch>.sh`  

2.  To install the Red Hat Enterprise package, type:

    `rpm -i sscx-<version>.rehl.<version>.<arch>.sh` 

    or for SUSE Linux Enterprise package, type:

    `rpm -i sscx-<version>.sles.<version>.<arch>.sh`  

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `service omiserver status`

## To install the agent on RPM based Universal Linux Servers (Oracle and Centos)

1.  Transfer the agent (`scx-<version>.universalr.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `rpm -i scx-<version>.universalr.<version>.<arch>.sh`

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

## To install the agent on DPKG-based Universal Linux Servers (Debian and Ubuntu)

1.  Transfer the agent (`scx-<version>.universald.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `dpkg -i scx-<version>.universald.<version>.<arch>.sh`

3.  To verify that the package is installed, type:

    `dpkg -l scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

## To install the agent on Solaris

1.  Transfer the agent (`scx-<version>.solaris.<version>.<arch>.sh`) to the Solaris server, type:

    `scx-<version>.solaris.<version>.<arch>.sh`

2.  Run the following command:

    `uncompress scx-<version>.solaris.<version>.<arch>.sh`

3.  To install the package, type:

    `pkgadd -d scx-<version>.solaris.<version>.<arch>.sh MSFTscx`

4.  To verify that the package is installed, type:

    `pkginfo –l MSFTscx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `svcs omiserver`

## To install the agent on HP-UX

1.  Transfer the agent (`scx-<version>.hpux.<version>.<arch>.sh`) to the HP server:

    `cp scx-<version>.hpux.<version>.<arch>.sh`

2.  To unzip the package, type:

    `gzip –d scx-<version>.hpux.<version>.<arch>.sh

3.  To install the package, type:

    `swinstall –s /path/scx-<version>.hpux.<version>.<arch> scx`

4.  To verify that the package is installed, type:

    `swlist scx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `ps –ef|grep scx`

    Look for the following process in the list:

    `scxcimserver`

## To install the agent on AIX

1.  Transfer the agent (`scx-<version>.aix.<version>.<arch>.sh`) to the AIX server, type:

    `cp scx-<version>.aix.<version>.<arch>.sh`

2.  To unzip the package, type:

    `gzip –d scx-<version>.aix.<version>.<arch>.sh`

3.  To install the package, type:

    `/usr/sbin/installp -a -d scx-<version>.aix.<version>.<arch> scx`

4.  To verify that the package is installed, type:

    `swlist scx`

5.  To verify that the Microsoft SCX CIM Server is running, type:

    `ps –ef|grep omi`

    Look for the following process in the list:

    omiserver

## Signing agent certificates

When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard, deployment and certificate signing. Then, you use the Discovery Wizard to add the computer to the Operations Manager database.

If there are existing certificates on the system, they are reused during agent installation. New certificates are not created. Certificates are not automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the `/etc/opt/microsoft/scx/ssl` folder. To regenerate the certificates at install, you must remove this folder before agent installation.

You must have already manually installed an agent before you start this procedure. You will need a root or elevated account to perform the procedure.

## To install certificates for UNIX and Linux support

1.  On the computer that is running the UNIX or Linux operating system, locate the file `/etc/opt/microsoft/scx/ssl/scx-host-<hostname>.pem` and securely copy or transfer it to any location on the computer that is hosting Operations Manager.

2.  On the computer that is hosting Operations Manager, on the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd**, and then press **Enter**.

4.  Change directories to the location where you copied the `pem` file.

5.  Type the command `scxcertconfig -sign scx-host-<hostname>.pem scx_new.pem`, and then press **Enter**. This command will self-sign your certificate (`scx-host-<hostname>.pem`) and then save the new certificate (`scx-host-<hostname>_new.pem`).

    > [!NOTE]
    > Ensure that the location where Operations Manager is installed is in your path statement, or use the fully qualified path of the `scxcertconfig.exe` file.

6.  Securely copy or transfer the `scx_new.pem` file into the `/etc/opt/microsoft/scx/ssl` folder on the computer that is hosting the UNIX or Linux operating system. This replaces the `original scx-host-<hostname>.pem` file.

7.  Restart the agent by typing `scxadmin –restart`.

## Discovering computers after manual deployment

After you have manually deployed agents to UNIX and Linux computers, they still need to be discovered by Operations Manager by using the Discovery Wizard. For the **Discovery type**, select **Discover only computers with the UNIX/Linux agent installed**. For more information see [Install Agent on UNIX and Linux Using the Discovery Wizard](manage-deploy-crossplat-agent-console.md).

## Next steps

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](manage-apply-overrides-object-discovery.md)

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md)

- Review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md) to understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers.  


