---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  mgoedtel
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Install Agent on UNIX and Linux Using the Discovery Wizard
ms.technology:  operations-manager
ms.assetid:  da7f3214-dd4a-449a-bdc3-7435c6378e45
---



# Install Agent on UNIX and Linux Using the Discovery Wizard

>Applies To: System Center 2016 Technical Preview - Operations Manager

Use the **Computer and Device Management Wizard** to discover and install agents on UNIX and Linux computers. For a list of the supported operating system versions, see [Supported Configurations](http://go.microsoft.com/fwlink/p/?LinkID=223642).

Before you run the wizard, gather the following information:

-   The host name, IP address, or range of IP addresses of the UNIX or Linux computers that you want to discover.

-   At a minimum, you will need a low-privileged account established on the UNIX or Linux computer to discover it. To install an agent, you will need privileged access. For more information, see [Accessing UNIX and Linux Computers in Operations Manager](https://technet.microsoft.com/library/hh212886%28v=sc.12%29.aspx).

-   If defined, the name of the resource pool created to monitor UNIX or Linux computers. Resource pools can contain management servers or gateways for monitoring UNIX or Linux computers. For more information, see [Managing Resource Pools for UNIX and Linux Computers](https://technet.microsoft.com/library/hh287152%28v=sc.12%29.aspx).

### To discover and install an agent on a UNIX or Linux Computer

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Click **Administration**.

3.  At the bottom of the navigation pane, click **Discovery Wizard**.

4.  On the **Discovery Type** page, click **Unix/Linux computers**.

5.  On the **Discovery Criteria** page, do the following:

    1.  Click **Add** to define a discovery scope. In the **Discovery Criteria** dialog box, do the following:

        1.  For the **Discovery scope**, click the ellipsis button **** to specify the host name, IP address, or range of IP addresses of the UNIX- or Linux-based computers to be discovered.

        2.  For the **Discovery type** select **Discover all computers** or **Discover only computers with the UNIX/Linux agent installed**.

            If you choose to discover only computers with the agent installed, the only credential that you will need to provide is for the agent verification. This can be a low-privileged account on the UNIX or Linux computer.

            > [!IMPORTANT]
            > Discovering only computers with the agent installed requires that the agent is currently installed and configured with a signed certificate.

        3.  To specify the credentials for installing an agent, click **Set credentials**. For detailed instructions, see "Credentials for Installing Agents" in [Setting Credentials for Accessing UNIX and Linux Computers](https://technet.microsoft.com/library/hh287150%28v=sc.12%29.aspx).

        4.  Click **Save**.

    2.  Select a resource pool to monitor the UNIX or Linux computer.

6.  Click **Discover** to display the **Discovery Progress**  page. The time it takes to finish discovery depends on many factors, such as the criteria specified and the configuration of the environment. If a large number (100 or more) of computers are being discovered or agents are being installed, the Operations console will not be usable during discovery and agent installation.

7.  On the **Computer Selection** page, on the **Manageable computers** tab, select the computers that you want to be managed. The **Additional results** tab lists any errors and computers that are already being managed.

8.  Click **Manage**.

9. On the **Computer Management** page, after the deployment process is completed, click **Done**.

You must have, at a minimum, a UNIX/Linux Action Account profile configured with a Monitoring Run As Account to monitor the UNIX or Linux computer. For more information, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](https://technet.microsoft.com/library/hh212926%28v=sc.12%29.aspx).

> [!NOTE]
> Solaris Zones are supported on Solaris 10 or newer versions. In monitoring a computer with Zones, each Zone is treated like a separate computer. You must install the agent on each computer that you want to monitor. Install the agent on the global zone first, because sparse zones share files with the global zone. If you try to install on a sparse zone first, the installation fails. For more information about troubleshooting, see [Operating System Issues](http://go.microsoft.com/fwlink/?LinkId=318149).

## See Also
[Operations Manager Agent Installation Methods](Operations-Manager-Agent-Installation-Methods.md)
[Install Agent on Windows Using the Discovery Wizard](Install-Agent-on-Windows-Using-the-Discovery-Wizard.md)
[Install Agent Using the MOMAgent.msi Setup Wizard](Install-Agent-Using-the-MOMAgent.msi-Setup-Wizard.md)
[Install Agent Using the Command Line](Install-Agent-Using-the-Command-Line.md)
[Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)
[Managing Certificates for UNIX and Linux Computers](Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Process Manual Agent Installations](Process-Manual-Agent-Installations.md)
[Applying Overrides to Object Discoveries](Applying-Overrides-to-Object-Discoveries.md)
[Configuring Agents](Configuring-Agents.md)
[Examples of Using MOMAgent Command to Manage Agents](Examples-of-Using-MOMAgent-Command-to-Manage-Agents.md)
[Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)
[Manually Uninstalling Agents from UNIX and Linux Computers](Manually-Uninstalling-Agents-from-UNIX-and-Linux-Computers.md)
[Uninstall Agent from Windows-based Computers](Uninstall-Agent-from-Windows-based-Computers.md)



