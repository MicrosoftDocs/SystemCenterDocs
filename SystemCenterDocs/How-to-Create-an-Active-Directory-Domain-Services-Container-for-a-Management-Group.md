---
title: How to Create an Active Directory Domain Services Container for a Management Group
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51705eeb-fdc1-4c11-8c01-0c73a73d31ec
---
# How to Create an Active Directory Domain Services Container for a Management Group
You can use the following command\-line syntax and procedure to create an Active Directory Domain Service \(AD DS\) container for a [!INCLUDE[om12long](Token/om12long_md.md)] management group. MOMADAdmin.exe is provided for this purpose and is installed with the Operations Manager management server. MOMADAdmin.exe must be run by an administrator of the specified domain. It can be run on a computer running Microsoft Windows 2000 SP4, Windows XP SP2, and Windows Server 2003 with Microsoft .NET Framework 2.0 installed.

**Command line syntax:**

**<path>\\MOMADAdmin.exe <ManagementGroupName> <MOMAdminSecurityGroup> < RunAsAccount> <Domain>**

> [!IMPORTANT]
> You must put a value inside quotation marks if the value contains a space.

**ManagementGroupName** is the name of the management group for which an AD container is being created.

**MOMAdminSecurityGroup** is a domain security group, **domain\\security\_group** format, which is a member of the Operations Managers Administrators security role for the management group.

-   For Active Directory integration to work, the security group must be either a global security group \(if Active Directory integration needs to function in multiple domains with 2 way trusts\) or a local domain group \(if Active Directory integration is only used in one domain\)

-   To make a security group to be the Management Group Operations Manager Group Administrator, use the following procedure.

    1.  In Operations console, select **Administration**.

    2.  In the **Administration** workspace, select **User Roles** under **Security**.

    3.  In **User Roles**, select **Operations Manager Administrators** and click the **Properties** action or right click **Operations Manager Administrators** and select **Properties**.

    4.  Click **Add** to open the **Select Group** dialog box.

    5.  Select the desired security group, and then click **OK** to close the dialog box.

    6.  Click **OK** to close **User Role Properties**.

    > [!NOTE]
    > We recommend one security group, which might contain several groups, be used for the Operations Manager Administrators role. That way, groups and members of groups can be added and removed from groups without a domain administrator needing to perform manual steps to assign them Read and Delete Child permissions to the Management Group container.

**RunAsAccount**: This is the domain account which will be used by the management server to read, write, and delete objects in AD. Use the format domain\\username.

**Domain** is the name of the domain in which the management group container will be created. MOMADAdmin.exe can be run across domains only if a two\-way trust exists between them.

### To create an Active Directory Domain Services container for a management group

1.  Open the command window.

2.  At the prompt, for example, type the following:

    **"C:\\Program Files\\System Center Operations Manager 2012\\MOMADAdmin.exe" "Message Ops" MessageDom\\MessageMOMAdmins MessageDom\\ MessageAdAcct MessageDom**

3.  The preceding command\-line example will:

    1.  Run the MOMADAdmin.exe utility from the command line.

    2.  Create the **"Message Ops"** Management Group AD DS container in the AD DS schema root of the **MessageDom** domain. To create the same Management Group AD DS container in additional domains, run MOMADAdmin.exe for each domain.

    3.  Add the **MessageDom\\MessageAdAcct** domain user account to the **MessageDom\\MessageMOMAdmin** AD DS security group and assign the security AD DS group the rights necessary to manage the AD DS container.

## See Also
[Integrating Active Directory and Operations Manager](Integrating-Active-Directory-and-Operations-Manager.md)
[Using Active Directory Domain Services to Assign Computers to Operations Manager Management Groups](Using-Active-Directory-Domain-Services-to-Assign-Computers-to-Operations-Manager-Management-Groups.md)
[How to Use Active Directory Domain Services to Assign Computers to Management Servers](How-to-Use-Active-Directory-Domain-Services-to-Assign-Computers-to-Management-Servers.md)
[Changing the Active Directory Integration Setting for an Agent](Changing-the-Active-Directory-Integration-Setting-for-an-Agent.md)


