---
title: How to Use Active Directory Domain Services to Assign Computers to Management Servers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ffd9fca-cae1-420a-9e6f-ea57f3633045
author:mgoedtel
manager:cfreemanwa
---
# How to Use Active Directory Domain Services to Assign Computers to Management Servers
The Operations Manager&nbsp;Agent Assignment and Failover Wizard creates an agent assignment rule that uses Active Directory Domain Services \(AD DS\) to assign computers to a management group and assign the computers' primary management server and secondary management servers. Use the following procedures to start and use the wizard.  
  
> [!IMPORTANT]  
> The Active Directory Domain Services container for the management group must be created prior to running the Agent Assignment and Failover Wizard.  
  
The Agent Assignment and Failover Wizard does not deploy the agent. You must deploy the agent to the computers using MOMAgent.msi.  
  
Changing the agent assignment rule can result in computers no longer being assigned to, and therefore monitored by, the management group. The state of these computers will change to critical, because the computers no longer send heartbeats to the management group. These computers can be deleted from the management group and, if the computer is not assigned to other management groups, the Operations Manager&nbsp;agent can be uninstalled.  
  
### To start the Operations Manager&nbsp;Agent Assignment and Failover Wizard  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the Administration workspace, click **Management Servers**.  
  
4.  In the **Management Servers** pane, right\-click the management server or gateway server to be **Primary Management Server** for the computers returned by the rules you will create in the following procedure, and then click **Properties**.  
  
    > [!NOTE]  
    > Gateway servers work like management servers in this context.  
  
5.  In the **Management Server Properties** dialog box, click the **Auto Agent Assignment** tab, and then click **Add** to start the Agent Assignment and Failover Wizard.  
  
### To use the Operations Manager&nbsp;Agent Assignment and Failover Wizard to assign computers to a management group  
  
1.  In the **Agent Assignment and Failover Wizard**, on the **Introduction** page, click **Next**.  
  
    > [!NOTE]  
    > The **Introduction** page does not appear if the wizard has been run and **Do not show this page again** was selected.  
  
2.  On the **Domain** page, do the following:  
  
    > [!NOTE]  
    > To assign computers from multiple domains to a management group, run the **Agent Assignment and Failover Wizard** for each domain.  
  
    -   Select the domain of the computers from the **Domain name** drop\-down list. The management server and all computers in the AD Agent Assignment resource pool must be able to resolve the domain name.  
  
        > [!IMPORTANT]  
        > The management server and the computers that you want to manage must be in two\-way trusted domains.  
  
    -   Set **Select Run As Profile** to the Run As profile associated with the Run As account provided when MOMADAdmin.exe was run for the domain. The default account used to perform agent assignment is the default action account specified during Setup, also referred to as the **Active Directory Based Agent Assignment Account**. This account represents credentials used when connecting to the specified domain's Active Directory and modifying Active Directory objects, and should match the account specified when running MOMAdmin.exe. If this was not the account used to run MOMADAdmin.exe, select **Use a different account to perform agent assignment in the specified domain,** and then select or create the account from the **Select Run As Profile** drop\-down list. The **Active Directory Based Agent Assignment Account** profile must be configured to use an Operations Manager administrator account which is distributed to all servers in the AD Agent Assignment resource pool.  
  
        > [!NOTE]  
        > For more information about Run As profiles and Run As accounts, see [Managing Run As Accounts and Profiles](../../om/manage/Managing-Run-As-Accounts-and-Profiles.md).  
  
3.  On the **Inclusion Criteria** page, either type the LDAP query for assigning computers to this management server in the text box and then click **Next,** or click **Configure**. If you click **Configure**, do the following:  
  
    1.  In the **Find Computers** dialog box, type the desired criteria for assigning computers to this management server.  
  
    2.  Click **OK,** and then click **Next**.  
  
        > [!NOTE]  
        > The following LDAP query will return computers with a name starting with MsgOps, **\(&\(sAMAccountType\=805306369\)\(objectCategory\=computer\)\(cn\=MsgOps\*\)\)**.  For more information about LDAP queries, see  [Creating a Query Filter](https://go.microsoft.com/fwlink/?LinkId=73366).  
  
4.  On the **Exclusion Criteria** page, type the FQDN of computers that you explicitly want to prevent from being managed by this management server, and then click **Next**.  
  
    > [!IMPORTANT]  
    > You must separate the computer FQDNs that you type with a semicolon, colon, or a new line \(CTRL\+ENTER\).  
  
5.  On the **Agent Failover** page, either select **Automatically manage failover** and click **Create** or select **Manually configure failover**. If you select **Manually configure failover**, do the following:  
  
    1.  Clear the check boxes of the management servers to which you do not want the agents to failover.  
  
    2.  Click **Create**.  
  
        > [!NOTE]  
        > With the **Manually configure failover** option, you must run the wizard again if you subsequently add a management server to the management group and want the agents to failover to the new management server.  
  
6.  In the **Management Server Properties** dialog box, click **OK**.  
  
    > [!NOTE]  
    > It can take up to one hour for the agent assignment setting to propagate in AD DS.  
  
## See Also  
[Integrating Active Directory and Operations Manager](../../om/manage/Integrating-Active-Directory-and-Operations-Manager.md)  
[Using Active Directory Domain Services to Assign Computers to Operations Manager Management Groups](../../om/manage/Using-Active-Directory-Domain-Services-to-Assign-Computers-to-Operations-Manager-Management-Groups.md)  
[How to Create an Active Directory Domain Services Container for a Management Group](../../om/manage/How-to-Create-an-Active-Directory-Domain-Services-Container-for-a-Management-Group.md)  
[Changing the Active Directory Integration Setting for an Agent](../../om/manage/Changing-the-Active-Directory-Integration-Setting-for-an-Agent.md)  
  
