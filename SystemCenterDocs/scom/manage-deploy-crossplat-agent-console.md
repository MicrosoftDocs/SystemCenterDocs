---
ms.assetid: 706132d8-a84c-4331-97bc-cf68c551a6fe
title: Install Agent on UNIX and Linux Using the Discovery Wizard
description: This article describes how to install the Operations Manager agent on UNIX and Linux computers.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/17/2023
ms.custom: UpdateFrequency2, intro-installation, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Install agent on UNIX and Linux using the Discovery Wizard

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Use the **Computer and Device Management Wizard** to discover and install agents on UNIX and Linux computers. For a list of the supported operating system versions, see [Supported Operating Systems and Versions](plan-supported-crossplat-os.md).

Before you run the wizard, gather the following information:

- The host name, IP address, or range of IP addresses of the UNIX or Linux computers that you want to discover.

- At a minimum, you'll need a low-privileged account established on the UNIX or Linux computer to discover it. To install an agent, you'll need privileged access. For more information, see [Planning Security Credentials for UNIX and Linux Computers](plan-security-crossplat-credentials.md).

- If defined, the name of the resource pool created to monitor UNIX or Linux computers. Resource pools can contain management servers or gateways for monitoring UNIX or Linux computers. For more information, see [Resource Pool Design Considerations](plan-resource-pool-design.md).

## Discover and install an agent on a UNIX or Linux computer

Follow these steps to discover and install an agent on a UNIX or Linux computer:

1. Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2. Select **Administration**.

3. At the bottom of the navigation pane, select **Discovery Wizard**.

4. On the **Discovery Type** page, select **Unix/Linux computers**.

5. On the **Discovery Criteria** page, do the following:

    1. Select **Add** to define a discovery scope. In the **Discovery Criteria** dialog, do the following:

        a.  For the **Discovery scope**, select the ellipsis button **…** to specify the host name, IP address, or range of IP addresses of the UNIX- or Linux-based computers to be discovered.

        b.  For the **Discovery type**, select **Discover all computers** or **Discover only computers with the UNIX/Linux agent installed**.

           If you choose to discover only computers with the agent installed, the only credential that you'll need to provide is for the agent verification. This can be a low-privileged account on the UNIX or Linux computer.

           > [!IMPORTANT]
           > Discovering only computers with the agent installed requires that the agent is currently installed and configured with a signed certificate.

        c.  To specify the credentials for installing an agent, select **Set credentials**. For detailed instructions, see **Credentials for Installing Agents** in [Setting Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).

        Alternatively, to use default credentials, check the box **Use Run As Credentials**. If this option is selected, a default Run As account must be defined in the **UNIX/Linux Action Account** and **UNIX/Linux Agent Maintenance Account** Run As profiles. The default account is the one that is associated with **All Managed Objects**.

        d.  Select **Save**.

    2. Select a resource pool to monitor the UNIX or Linux computer.

6. Select **Discover** to display the **Discovery Progress** page. The time it takes to finish discovery depends on many factors, such as the criteria specified and the configuration of the environment. If a large number (100 or more) of computers are being discovered or agents are being installed, the Operations console won't be usable during discovery and agent installation.

7. On the **Computer Selection** page, on the **Manageable computers** tab, select the computers that you want to be managed. The **Additional results** tab lists any errors and computers that are already being managed.

8. Select **Manage**.

9. On the **Computer Management** page, after the deployment process is completed, select **Done**.

You must have, at a minimum, a UNIX/Linux Action Account profile configured with a Monitoring Run As Account to monitor the UNIX or Linux computer. For more information, see [How to Configure Run As Accounts and Profiles for UNIX and Linux Access](~/scom/manage-security-config-crossplat-runas-profile.md).

::: moniker range="< sc-om-2019"

> [!NOTE]
> Solaris Zones are supported on Solaris 10 or newer versions. In monitoring a computer with Zones, each Zone is treated like a separate computer. You must install the agent on each computer that you want to monitor. Install the agent on the global zone first, because sparse zones share files with the global zone. If you try to install on a sparse zone first, the installation fails. For more information about troubleshooting, see [Operating System Issues](/previous-versions/system-center/system-center-2012-R2/hh212755(v=sc.12)).

::: moniker-end

## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](~/scom/manage-install-crossplat-agent-cmdline.md).

- To learn how to configure object discovery rules and disable discovery of a specific object, see [Applying Overrides to Object Discoveries](manage-apply-overrides-object-discovery.md).

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](~/scom/manage-upgrade-uninstall-crossplat-agent.md).

- To understand what options and steps need to be performed to properly uninstall the agent from your UNIX and Linux computers, review [Manually Uninstalling Agents from UNIX and Linux Computers](manage-uninstall-crossplat-agent.md).
