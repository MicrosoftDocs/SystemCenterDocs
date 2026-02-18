---
ms.assetid:
title: include file
description: include article to detail the detail how to install the System Center 2016 - Operations Manager agent manually on UNIX and Linux computers.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  07/01/2024
ms.topic:  include
ms.service:  system-center
ms.subservice:  operations-manager
ms.update-cycle: 1095-days
---

## Install Operations Manager agent on UNIX and Linux computers
The following procedures show how to manually install agents to UNIX and Linux computers for monitoring in System Center 2016 - Operations Manager.

## To install the agent on Red Hat Enterprise Linux and SUSE Linux Enterprise Server

1.  Transfer the Red Hat Enterprise agent to the Linux server:

    `scx-<version>.rhel.<version>.<arch>.sh`  

    or for SUSE Linux Enterprise Server:  

    `scx-<version>.sles.<version>.<arch>.sh`  

2.  To install the Red Hat Enterprise package, enter:

    `sh ./scx-<version>.rhel.<version>.<arch>.sh --install`

    or for SUSE Linux Enterprise package, enter:

    `sh ./scx-<version>.sles.<version>.<arch>.sh --install`  

3.  To verify that the package is installed, enter:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `scxadmin -status`

## To install the agent on RPM based Universal Linux Servers (Oracle)

1.  Transfer the agent (`scx-<version>.universalr.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, enter:

    `sh ./scx-<version>.universalr.<version>.<arch>.sh --install`

3.  To verify that the package is installed, enter:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `scxadmin -status`

## To install the agent on DPKG-based Universal Linux Servers (Debian and Ubuntu)

1.  Transfer the agent (`scx-<version>.universald.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, enter:

    `sh ./scx-<version>.universald.<version>.<arch>.sh --install`

3.  To verify that the package is installed, enter:

    `dpkg -l scx`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `scxadmin -status`

## To install the agent on Solaris

1.  Transfer the agent (`scx-<version>.solaris.<version>.<arch>.sh`) to the Solaris server.  

2.  To install the package, enter:

    `sh ./scx-<version>.solaris.<version>.<arch>.sh -install`

3.  To verify that the package is installed, enter:

    `pkginfo -l scx`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `svcs omiserver`

## To install the agent on HP-UX

1.  Transfer the agent (`scx-<version>.hpux.<version>.<arch>.sh`) to the HP server.

2.  To install the package, enter:

    `sh .scx-<version>.hpux.<version>.<arch>.sh --install`

3.  To verify that the package is installed, enter:

    `swlist scx`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `ps -ef | grep omi`

    Look for the following process in the list:

    omiserver

## To install the agent on AIX

1.  Transfer the agent (`scx-<version>.aix.<version>.<arch>.sh`) to the AIX server.

2.  To install the package, enter:

    `sh ./scx-<version>.aix.<version>.<arch>.sh --install`

3.  To verify that the package is installed, enter:

    `lslpp -l “scx*"`

4.  To verify that the Microsoft SCX CIM Server is running, enter:

    `ps -ef | grep omi`

    Look for the following process in the list:

    omiserver

## Signing agent certificates

When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard, deployment and certificate signing. Then, you use the Discovery Wizard to add the computer to the management group.

If there are existing certificates on the system, they're reused during agent installation. New certificates aren't created. Certificates aren't automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the `/etc/opt/microsoft/scx/ssl` folder. To regenerate the certificates at install, you must remove this folder before agent installation.

You must have already manually installed an agent before you start this procedure. You'll need a root or elevated account to perform the procedure.

## To install certificates for UNIX and Linux support

1.  On the computer that is running the UNIX or Linux operating system, locate the file `/etc/opt/microsoft/scx/ssl/scx-host-<hostname>.pem` and securely copy or transfer it to any location on the computer that is hosting Operations Manager.

2.  On the computer that is hosting Operations Manager, on the Windows desktop, select **Start**, and select **Run**.

3.  In the **Run** dialog, enter **cmd**, and then press **Enter**.

4.  Change directories to the location where you copied the `pem` file.

5.  Enter the command `scxcertconfig -sign scx-host-<hostname>.pem scx_new.pem`, and then press **Enter**. This command will self-sign your certificate (`scx-host-<hostname>.pem`) and then save the new certificate (`scx-host-<hostname>_new.pem`).

    > [!NOTE]
    > Ensure that the location where Operations Manager is installed is in your path statement, or use the fully qualified path of the `scxcertconfig.exe` file.

6.  Securely copy or transfer the `scx_new.pem` file into the `/etc/opt/microsoft/scx/ssl` folder on the computer that is hosting the UNIX or Linux operating system. This replaces the `original scx-host-<hostname>.pem` file.

7.  Restart the agent by entering `scxadmin -restart`.

## Discovering computers after manual deployment

After you've manually deployed agents to UNIX and Linux computers, they still need to be discovered by Operations Manager by using the Discovery Wizard. For the **Discovery type**, select **Discover only computers with the UNIX/Linux agent installed**. For more information, see [Install Agent on UNIX and Linux Using the Discovery Wizard](~/scom/manage-deploy-crossplat-agent-console.md).
