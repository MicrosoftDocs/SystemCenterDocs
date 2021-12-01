---
ms.assetid: 
title: include file
description: include article to detail how to install the Operations Manager version 2019 agent manually on UNIX and Linux computers.
author: v-pgaddala
ms.author: v-pgaddala
manager:  evansma
ms.date:  11/29/2021
ms.topic:  include
ms.prod:  system-center
ms.technology:  operations-manager
---

## Install Operations Manager 2022 agent on UNIX and Linux computers
The following procedures show how to manually install agents to UNIX and Linux computers for monitoring in System Center Operations Manager version 2022.

## To install the agent on Red Hat Enterprise Linux and SUSE Linux Enterprise Server

1.  Transfer the Red Hat Enterprise agent to the Linux server:

    `scx-<version>.rhel.<version>.<arch>.sh`  

    or for SUSE Linux Enterprise Server:  

    `scx-<version>.sles.<version>.<arch>.sh`  

2.  To install the Red Hat Enterprise package, type:

    `sh ./scx-<version>.rhel.<version>.<arch>.sh --install --enable-opsmgr`

    or for SUSE Linux Enterprise package, type:

    `sh ./scx-<version>.sles.<version>.<arch>.sh --install --enable-opsmgr`  

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

## To install the agent on RPM based Universal Linux Servers (Oracle)

1.  Transfer the agent (`scx-<version>.universalr.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `sh ./scx-<version>.universalr.<version>.<arch>.sh --install --enable-opsmgr`

3.  To verify that the package is installed, type:

    `rpm -q scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

## To install the agent on DPKG-based Universal Linux Servers (Debian and Ubuntu)

1.  Transfer the agent (`scx-<version>.universald.<version>.<arch>.sh`) to the Linux server. This should be done via SCP or FTP in binary mode.

2.  To install the package, type:

    `sh ./scx-<version>.universald.<version>.<arch>.sh --install --enable-opsmgr`

3.  To verify that the package is installed, type:

    `dpkg -l scx`

4.  To verify that the Microsoft SCX CIM Server is running, type:

    `scxadmin -status`

## Signing agent certificates

When you manually deploy an agent, you perform the first two steps that are typically handled by the Discovery Wizard, deployment and certificate signing. The certificate gets encrypted with SHA256. Then, you use the Discovery Wizard to add the computer to the management group. 

If there are existing certificates on the system, they are reused during agent installation. New certificates are not created. Certificates are not automatically deleted when you uninstall an agent. You must manually delete the certificates that are listed in the folder `/etc/opt/microsoft/scx/ssl` for UNIX and `/etc/opt/microsoft/scx/scom/certs` folder for Linux. To regenerate the certificates at install, you must remove this folder before agent installation. 

You must have already manually installed an agent before you start this procedure. You will need a root or elevated account to perform the procedure. 

## To install certificates for UNIX and Linux support

1.  On the computer that is running the UNIX or Linux operating system, locate the file `/etc/opt/microsoft/scx/ssl/scx-host-<hostname>.pem` and securely copy or transfer it to any location on the computer that is hosting Operations Manager.

2.  On the computer that is hosting Operations Manager, on the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd**, and then press **Enter**.

4.  Change directories to the location where you copied the `pem` file.

5.  Type the command `scxcertconfig -sign scx-host-<hostname>.pem scx_new.pem`, and then press **Enter**. This command will self-sign your certificate (`scx-host-<hostname>.pem`) and then save the new certificate (`scx-host-<hostname>_new.pem`).

    > [!NOTE]
    > Ensure that the location where Operations Manager is installed is in your path statement, or use the fully qualified path of the `scxcertconfig.exe` file.

6.  Securely copy or transfer the `scx_new.pem` file into the `/etc/opt/microsoft/scx/ssl` folder on the computer that is hosting the UNIX or Linux operating system. This replaces the original `scx-host-<hostname>.pem` file.

7.  Restart the agent by typing `scxadmin –restart`.

## Discovering computers after manual deployment

After you have manually deployed agents to UNIX and Linux computers, they still need to be discovered by Operations Manager by using the Discovery Wizard. For the **Discovery type**, select **Discover only computers with the UNIX/Linux agent installed**. For more information see [Install Agent on UNIX and Linux Using the Discovery Wizard](~/scom/manage-deploy-crossplat-agent-console.md).
