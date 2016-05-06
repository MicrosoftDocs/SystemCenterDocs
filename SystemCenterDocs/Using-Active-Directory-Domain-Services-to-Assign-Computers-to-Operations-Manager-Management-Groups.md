---
title: Using Active Directory Domain Services to Assign Computers to Operations Manager Management Groups
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6c0aefa-d842-4f09-9c7e-681a81055851
---
# Using Active Directory Domain Services to Assign Computers to Operations Manager Management Groups
[!INCLUDE[om12long](./Token/om12long_md.md)] allows you to take advantage of your investment in Active Directory Domain Services \(AD DS\) by enabling you to use it to assign agent\-managed computers to management groups.

To assign computers to management groups by using AD DS:

-   The functional level of AD DS domains must be Windows 2000 native or Windows Server 2003.

-   Agent\-managed computers and all managements servers in the AD Agent Assignment resource pool must be in the same or two\-way trusted domains.

    > [!NOTE]
    > Regardless of whether AD DS is used to assign computers to a management group, agent\-managed computers and their primary management server and secondary management server must be in the same or two\-way trusted domains or a gateway server must be used. For more information about gateway servers, see [About Gateway Servers in Operations Manager](./About-Gateway-Servers-in-Operations-Manager.md).

Following are the phases for using AD DS to assign computers to Operations Manager management groups.

1.  A domain administrator uses MOMADAdmin.exe to create an AD DS container for an Operations Manager management group in the domains of the computers it will manage. The AD DS security group that is specified when running MOMADAdmin.exe is granted Read and Delete Child permissions to the container. By creating a container this way, Operations Manager administrators are given the permission necessary to add management servers to the container and assign computers to them, without needing to be domain administrators.

2.  An Operations Manager administrator uses the Agent Assignment and Failover Wizard to assign computers to a primary management server and secondary management server.

    > [!NOTE]
    > Domain controllers cannot be assigned to a management group using Active Directory Domain Services.

3.  The Operations Manager agent is deployed using MOMAgent.msi to the desired computers and configured to get its management group information from Active Directory.

    > [!NOTE]
    > Active Directory Integration is disabled for agents that were installed from the Operations console. By default, Active Directory Integration is enabled for agents installed manually using MOMAgent.msi. To disable Active Directory Integration for manual installs, use the command line parameter **USE\_SETTINGS\_FROM\_AD\=0** as explained in [Install Agent Using the Command Line](./Install-Agent-Using-the-Command-Line.md).

Configuring agents to get their management group information from AD DS is also helpful if your organization uses images to deploy computers. For example, add the Operations Manager agent to the SQL Server 2005 image and configure the agent to get its management group information from Active Directory. When you bring up a new SQL Server 2005 server from an image, the server is automatically configured to be managed by the appropriate Operations Manager management group and download the applicable management packs.

## See Also
[Integrating Active Directory and Operations Manager](./Integrating-Active-Directory-and-Operations-Manager.md)
[How to Create an Active Directory Domain Services Container for a Management Group](./How-to-Create-an-Active-Directory-Domain-Services-Container-for-a-Management-Group.md)
[How to Use Active Directory Domain Services to Assign Computers to Management Servers](./How-to-Use-Active-Directory-Domain-Services-to-Assign-Computers-to-Management-Servers.md)
[Changing the Active Directory Integration Setting for an Agent](./Changing-the-Active-Directory-Integration-Setting-for-an-Agent.md)


