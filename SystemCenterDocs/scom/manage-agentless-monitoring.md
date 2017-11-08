---
title: Agentless Monitoring in Operations Manager
description: This article describes how to use agentless monitoring in Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 03/13/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: e5b25d0f-9316-42d2-aeb9-4ba0b0afc6cf
---
# Agentless Monitoring in Operations Manager

System Center 2016 - Operations Manager can gather performance and availability data on a computer that does not have an agent installed by using a proxy agent that is installed on another computer. Use agentless-monitoring of computers when it is not possible or desirable to install an agent on a computer.  
  
An agentless-managed computer is a Windows-based computer that is discovered by using the Operations console. You assign a management server or agent-managed computer to provide remote (proxy) agent functionality for the computers.  
  
Agentless-managed computers are managed as if there is an agent installed on them. Not all management packs work in agentless mode. For more information, see the documentation for the management packs you are running.  
  
> [!IMPORTANT]  
> Agentless management of a computer will not work if the agentless-managed computer and its proxy communicate through a firewall. A management server will not collect descriptions for events or publishers that are present on an agentless managed computer but are not present on the proxy agent.  
  
For information about configuring an agent-managed computer as a proxy for agentless-managed computers, see [How to configure a proxy for agentless monitoring](#how-to-configure-a-proxy-for-agentless-monitoring).  
  
> [!IMPORTANT]  
> An agentless-managed computer places additional resource utilization on a management server than an agent-managed computer.  
  
To change an agentless-managed computer to an agent-managed computer, do the following:  
  
1.  Delete the agentless-managed computer from the management group by right-clicking the computer in **Agentless Managed** in the **Administration** workspace and then clicking **Delete**.  
  
2.  Deploy the agent to the computer. For more information, see [managing discovery and agents](../om/manage/managing-discovery-and-agents.md).  
  
## Agentless monitoring compared to Agentless Exception Monitoring  
Agentless monitoring provides monitoring of computers without agents by using a proxy agent and applying those management packs that support agentless monitoring. Agentless Exception Monitoring (AEM) redirects hardware, operating system, and application crash information to Operations Manager, which can aggregate, view, and report on error reports that are sent by the Windows Error Reporting service. For information on AEM, see [Client monitoring using Agentless Exception Monitoring in Operations Manager](manage-client-monitoring-using-aem.md).  
  
You can monitor a computer without an agent by using either agentless monitoring, AEM, or both.  

## To configure Windows-based computers for agentless management  
  
1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role for the management group.  
  
2.  Click **Administration**.  
  
3.  At the bottom of the navigation pane, click **Discovery Wizard**.  
  
4.  On the **Discovery Type** page, click **Windows computers**.  
  
5.  On the **Auto or Advanced?** page, do the following:  
  
    1.  Select either **Automatic computer discovery** or **Advanced discovery**. Automatic computer discovery scans for Windows-based computers in the domain. Advanced discovery allows you to specify criteria for the computers that the wizard will return, such as computer names starting with WKS. If you select **Automatic computer discovery**, click **Next**, and then go to step 7. If you select **Advanced discovery**, continue with the following steps.  
  
    2.  In the **Computer and Device Classes** list, select **Servers and Clients**, **Servers Only**, or **Clients Only**.  
  
    3.  In the **Management Server** list, click the management server or gateway server to discover the computers.  
  
    4.  If you selected **Servers and Clients**, you can select the **Verify discovered computers can be contacted** check box. This is likely to increase the success rate of agent deployment, but discovery can take longer.  
  
        > [!NOTE]  
        > If the Active Directory catalog does not contain the NetBIOS names for computers in a domain, select **Verify discovered computers can be contacted**. Otherwise, the **Browse, or Type In** option fails to find computers. This affects computers in the same domain as the management server, in another domain with a full trust relationship, and in untrusted domains by using a gateway server.  
  
    5.  Click **Next**.  
  
    > [!NOTE]  
    > The wizard can return approximately 4000 computers if **Verify discovered computers can be contacted** is selected, and it can return 10,000 computers if this option is not selected. Automatic computer discovery verifies that discovered computers can be contacted. A computer that is already managed by the management group is not returned.  
  
6.  On the **Discovery Method** page, you can locate the computers that you want to manage by either scanning or browsing Active Directory Domain Services or typing the computer names.  
  
    If you want to scan, do the following:  
  
    1.  If it is not already selected, select **Scan Active Directory** and then click **Configure**.  
  
    2.  In the **Find Computers** dialog box, type the criteria that you want to use for discovering computers, and then click **OK**.  
  
    3.  In the **Domain** list, click the domain of the computers that you want to discover.  
  
    If you want to browse Active Directory Domain Services or type the computer names, do the following:  
  
    -   Select **Browse for, or type-in computer names**, click **Browse**, specify the names of the computers that you want to manage, and then click **OK**.  
  
    -   In the **Browse for, or type-in computer names** box, type the computer names, separated by a semi-colon, comma, or a new line. You can use NetBIOS computer names or fully qualified domain names (FQDN).  
  
7.  Click **Next**, and on the **Administrator Account** page, do one of the following:  
  
    -   Select **Use selected Management Server Action Account** if it is not already selected.  
  
    -   Select **Other user account**, type the **User name** and **Password**, and then select the **Domain** from the list. If the user name is not a domain account, select **This is a local computer account, not a domain account**.  
  
        > [!IMPORTANT]  
        > The account must have administrative privileges on the targeted computers. If **This is a local computer account, not a domain account** is selected, the management server action account will be used to perform discovery.  
  
8.  Click **Discover** to display the **Discovery Progress** page. The time it takes discovery to finish depends on many factors, such as the criteria specified and the configuration of the environment.  
  
    > [!NOTE]  
    > Computers that are already managed by the management group will not be returned by the wizard.  
  
9. On the **Select Objects to Manage**  page, do the following:  
  
    1.  Select the computers that you want to be agent-managed computers.  
  
    2.  In the **Management Mode** list, click **Agentless** and then click **Next**.  
  
    3.  Click **Change**, select the proxy agent that you want to use, click **OK**, and then click **Next**.  
  
10. On the **Summary** page, do the following:  
  
    1.  Leave the **Agent installation directory** set to the default of **%ProgramFiles%\Microsoft Monitoring Agent** or type an installation path.  
  
        > [!IMPORTANT]  
        > If a different **Agent installation directory** is specified, the root of the path must exist on the targeted computer or the agent installation fails. Subdirectories, such as **\Agent**, are created if they do not exist.  
  
    2.  Leave **Agent Action Account** set to the default, **Local System**, or select **Other** and type the **User name**, **Password**, and **Domain**. The Agent Action Account is the default account that the agent will use to perform actions.  
  
    3.  Click **Finish**.  
  
11. In the **Agent Management Task Status** dialog box, the **Status** for each selected computer changes from **Queued** to **Success**; the computers are ready to be managed.  
  
    > [!NOTE]  
    > If the task fails for a computer, click the targeted computer. The reason for the failure is displayed in the **Task Output** text box.  
  
12. Click **Close**. The computers will be listed in the **Administration** workspace in **Agentless Managed**.   

## How to configure a proxy for agentless monitoring

When you set up agentless monitoring of a computer, you select a proxy for each agentless-managed computer. Being configured as a proxy agent allows an agent to submit data on behalf of another source. A management group can serve as a proxy, but this takes up system resources. A best practice is using an agent-managed computer as a proxy agent.  
  
You might also configure a computer to act as a proxy to support specific features of a management pack. For example, the Active Directory Management Pack requires enabling domain controllers to act as proxy agents.  
  
> [!NOTE]  
> If a proxy agent is removed from management, its agentless systems are no longer managed.  
  
Both the agentless-managed system and its proxy need to have access to the managing server through any firewalls. For more information about interacting with firewalls, see [Configuring a firewall for Operations Manager](plan-security-config-firewall.md).  
  
1.  In the **Administration** workspace, click **Agent Managed**, right-click the computer, and then click **Properties**.  
  
2.  In the **Agent Properties** dialog box, click the **Security** tab.  
  
3.  On the **Security** tab, select **Allow this agent to act as a proxy and discover managed objects on other computers**, and then click **OK**.  
  
### How to configure a management server as a proxy for agentless-managed computers  
  
1.  In the **Administration** workspace, click **Management Servers**, right-click the management server, and then click **Properties**.  
  
2.  In the **Management Server Properties** dialog box, click the **Security** tab.  
  
3.  On the **Security** tab, select **Allow this server to act as a proxy and discover managed objects on other computers,** and then click **OK**.  
  
### How to change the proxy agent for agentless-managed computers  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role for the management group.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Click **Agentless Managed**.  
  
4.  In the **Agentless Managed** pane, select the agentless-managed computers for which you want to change the proxy agent, right-click them, and then select **Change Proxy Agent**.  
  
5.  In the **Change Proxy Agent** dialog box, select the computer you want to be the new proxy agent, and then click **OK**. 

## Next steps
  
Monitoring of applications, features, and services are enabled by importing management packs. See [Using Management Packs](/system-center/scom/manage/using-management-packs) for an explanation of what management packs do, and how to import and manage them.
  
