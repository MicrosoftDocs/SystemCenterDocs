---
title: Prerequisites: adding servers or clusters as Hyper-V hosts or host clusters in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b52fed50-3a05-4261-9924-a858300e80de
---
# Prerequisites: adding servers or clusters as Hyper-V hosts or host clusters in VMM
Before you add existing servers or clusters as Hyper\-V hosts in Virtual Machine Manager \(VMM\), consider the location of the existing servers or clusters, relative to the VMM management server—in the same or a trusted domain, in an untrusted domain, or in a disjointed namespace. \(For existing servers in a perimeter network, see [How to add Hyper-V hosts in a perimeter network in VMM](How-to-add-Hyper-V-hosts-in-a-perimeter-network-in-VMM.md).\) The prerequisites are as follows:

-   [Prerequisites for the same domain or a trusted domain](Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md#BKMK_trusted)

-   [Prerequisites for an untrusted domain](Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md#BKMK_untrusted)

-   [Prerequisites for a disjointed namespace](Prerequisites--adding-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md#BKMK_disjoint)

For information about other methods for adding or provisioning hosts or host clusters to VMM, see the links at the end of this topic.

## <a name="BKMK_trusted"></a>Prerequisites for the same domain or a trusted domain

-   The stand\-alone server or the failover cluster must be in an Active Directory domain that has a two\-way trust with the domain of the VMM management server.

-   The computers you want to add must be running an operating system that is supported for Hyper\-V hosts, as described in the[Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx) requirements. If a computer does not already have the Hyper\-V role installed, make sure that the BIOS on the computer is configured to support Hyper\-V. If the Hyper\-V role is not already installed, VMM automatically installs the role when you add the server.

-   If you want to add the VMM management server as a managed Hyper\-V host, make sure that you enable the Hyper\-V role on the VMM management server before you add the computer.

    > [!IMPORTANT]
    > You cannot add a highly available VMM management server as a managed Hyper\-V host cluster.

-   You can add a failover cluster that you have already created, and it will become a host cluster that is managed by VMM \(see [How to add existing servers or clusters as Hyper-V hosts or host clusters in VMM](How-to-add-existing-servers-or-clusters-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)\). If you want to use VMM to create the cluster, see the following topics:

    -   [Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)

    -   [Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)

-   If you use Group Policy to configure Windows Remote Management \(WinRM\) settings, review the following requirements:

    -   WinRM Service settings must be configured through Group Policy, and can only apply to hosts that are in a trusted Active Directory domain. Specifically, VMM supports the configuration of the **Allow automatic configuration of listeners**, **Turn On Compatibility HTTP Listener**, and **Turn on Compatibility HTTPS Listener** Group Policy settings. VMM does not support other WinRM Service policy settings.

    -   If you enable the **Allow automatic configuration of listeners** policy setting, you must configure it to allow messages from any IP address. In other words, in the policy setting, the IPv4 filter and IPv6 filter \(depending on whether you use IPv6\) must be set to **\***.

    -   WinRM Client settings cannot be configured through Group Policy. These policy settings might override client properties that VMM requires for the VMM agent to work correctly.

    If you enable any unsupported WinRM Group Policy settings, installation of the VMM agent may fail.

    > [!NOTE]
    > The WinRM policy settings are located in the Computer Configuration\\Administrative Templates\\Windows Components\\Windows Remote Management \(WinRM\) node of the Local Group Policy Editor or the Group Policy Management Console \(GPMC\).

-   You must specify account credentials for an account that has administrative rights on the computers that you want to add.

    > [!IMPORTANT]
    > If you configured the VMM service to use a domain account when you installed the VMM management server, do not use the same domain account to add or remove Hyper\-V hosts from VMM.

    You can enter a user name \(as *domain\_name*\\*user\_name*\) and password, or specify a Run As account. If you use a Run As account, you can create it beforehand, or at the time that you add the servers to VMM. For example, you could create a Run As account called **Trusted Hyper\-V Hosts**. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

## <a name="BKMK_untrusted"></a>Prerequisites for an untrusted domain
When you add servers or clusters that are in an untrusted domain, when VMM installs the agent on the servers or clusters, VMM also generates a certificate. The certificate is used to help secure communications with the host. When VMM adds the host or cluster, the certificate is automatically imported into the VMM management server’s trusted certificate store.

Review the following prerequisites:

-   The computers you want to add must be running an operating system that is supported for Hyper\-V hosts, as described in the[Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx) requirements.  If a computer does not already have the Hyper\-V role installed, make sure that the BIOS on the computer is configured to support Hyper\-V. If the Hyper\-V role is not already installed, VMM automatically installs the role when you add the server.

-   VMM does not support the configuration of Windows Remote Management \(WinRM\) Group Policy settings \(Service or Client\) on hosts that are in an untrusted Active Directory domain. If WinRM Group Policy settings are enabled, installation of the VMM agent—required on the hosts—might fail.

    > [!NOTE]
    > The WinRM policy settings are located in the Computer Configuration\\Administrative Templates\\Windows Components\\Windows Remote Management \(WinRM\) node of the Local Group Policy Editor or the Group Policy Management Console \(GPMC\).

-   You will need the name of an account that has administrative rights on the computers that you want to add. From that account, you can create a Run As account beforehand, or you can create the Run As account while you are adding the servers or the cluster.

    For example, you could create the Run As account **Untrusted Hyper\-V Hosts**. For more information about Run As accounts, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

## <a name="BKMK_disjoint"></a>Prerequisites for a disjointed namespace
Review these prerequisites if the server or cluster you want to add to VMM as a managed host or host cluster is in a disjointed namespace. A disjointed namespace occurs when the computer’s primary Domain Name System \(DNS\) suffix does not match the domain of which it is a member. For example, the namespace is disjointed when a computer that has the DNS name of HyperVHost03.contosocorp.com is in a domain that has the DNS name of contoso.com. For more information about disjointed namespaces, see [Naming conventions in Active Directory for computers, domains, sites, and OUs](http://support.microsoft.com/kb/909264).

Review the following prerequisites:

-   The computers you want to add must be running an operating system that is supported for Hyper\-V hosts, as described in the[Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx) requirements.  If a computer does not already have the Hyper\-V role installed, make sure that the BIOS on the computer is configured to support Hyper\-V. If the Hyper\-V role is not already installed, VMM automatically installs the role when you add the server.

-   The System Center Virtual Machine Manager service must be running as the local system account or as a domain account that has permission to register a Service Principal Name \(SPN\) in Active Directory Domain Services \(AD DS\).

    When you try to add a computer that is in a disjointed namespace, VMM checks AD DS to see if an SPN exists. If it does not, VMM tries to create one. If the permissions are configured as described, VMM adds the missing SPN automatically. Otherwise, host addition fails.

    If host addition fails, you must add the SPN manually. To add the SPN, at the command prompt, type the following command, where *<FQDN>* represents the disjointed namespace FQDN, and *<NetBIOSName>* is the NetBIOS name of the host:

    **setspn \-A HOST\/<FQDN> <NetBIOSName>**

    For example, **setspn –A HOST\/hypervhost03.contosocorp.com hypervhost03**.

    > [!TIP]
    > To view a list of registered SPNs for the host, at the command prompt, type **setspn \-l <NetBIOSName>**, where *<NetBIOSName>* is the NetBIOS name of the host.

-   If the host cluster is in a disjointed namespace and the VMM management server is not, you must add the Domain Name System \(DNS\) suffix for the host cluster to the TCP\/IP connection settings on the VMM management server.

-   If you use Group Policy to configure Windows Remote Management \(WinRM\) settings, review the following requirements:

    -   WinRM Service settings must be configured through Group Policy, and can only apply to hosts that are in a trusted Active Directory domain. Specifically, VMM supports the configuration of the **Allow automatic configuration of listeners**, **Turn On Compatibility HTTP Listener**, and **Turn on Compatibility HTTPS Listener** Group Policy settings. VMM does not support other WinRM Service policy settings.

    -   If you enable the **Allow automatic configuration of listeners** policy setting, you must configure it to allow messages from any IP address. In other words, in the policy setting, the IPv4 filter and IPv6 filter \(depending on whether you use IPv6\) must be set to **\***.

    -   WinRM Client settings cannot be configured through Group Policy. These policy settings might override client properties that VMM requires for the VMM agent to work correctly.

    If you enable any unsupported WinRM Group Policy settings, installation of the VMM agent may fail.

    > [!NOTE]
    > The WinRM policy settings are located in the Computer Configuration\\Administrative Templates\\Windows Components\\Windows Remote Management \(WinRM\) node of the Local Group Policy Editor or the Group Policy Management Console \(GPMC\).

## See Also
[Adding Windows servers as Hyper-V hosts or host clusters in VMM](Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md)
[Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


