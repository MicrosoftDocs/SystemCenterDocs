---
title: How to Configure a Proxy for Agentless Monitoring
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a3c14c5-98cf-4de2-a6ce-6383d3b231f5
author:mgoedtel
manager:cfreemanwa
---
# How to Configure a Proxy for Agentless Monitoring
[!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] can monitor Microsoft Windows\-based computers on which an agent is not installed by using an agent on another computer to act as a proxy. This is called agentless management.  
  
> [!NOTE]  
> Not all management packs support agentless management, so make sure agentless management will serve your needs before using it. For example, the Active Directory and Microsoft Exchange Server&nbsp;2003 management packs do not support agentless management.  
  
When you set up agentless monitoring of a computer, you select a proxy for each agentless\-managed computer. Being configured as a proxy agent allows an agent to submit data on behalf of another source. A management group can serve as a proxy, but this takes up system resources. A best practice is using an agent\-managed computer as a proxy agent.  
  
You might also configure a computer to act as a proxy to support specific features of a management pack. For example, the Active Directory Management Pack requires enabling domain controllers to act as proxy agents.  
  
> [!NOTE]  
> If a proxy agent is removed from management, its agentless systems are no longer managed.  
  
Both the agentless\-managed system and its proxy need to have access to the managing server through any firewalls. For more information about interacting with firewalls, see \(link to appropriate content in deployment\).  
  
### To configure an agent\-managed computer as a proxy for agentless\-managed computers  
  
1.  In the **Administration** workspace, click **Agent Managed**, right\-click the computer, and then click **Properties**.  
  
2.  In the **Agent Properties** dialog box, click the **Security** tab.  
  
3.  On the **Security** tab, select **Allow this agent to act as a proxy and discover managed objects on other computers**, and then click **OK**.  
  
### How to configure a management server as a proxy for agentless\-managed computers  
  
1.  In the **Administration** workspace, click **Management Servers**, right\-click the management server, and then click **Properties**.  
  
2.  In the **Management Server Properties** dialog box, click the **Security** tab.  
  
3.  On the **Security** tab, select **Allow this server to act as a proxy and discover managed objects on other computers,** and then click **OK**.  
  
### To change the proxy agent for agentless\-managed computers  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role for the management group.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Click **Agentless Managed**.  
  
4.  In the **Agentless Managed** pane, select the agentless\-managed computers for which you want to change the proxy agent, right\-click them, and then select **Change Proxy Agent**.  
  
5.  In the **Change Proxy Agent** dialog box, select the computer you want to be the new proxy agent, and then click **OK**.  
  
## See Also  
[Agentless Monitoring in Operations Manager](../../om/manage/Agentless-Monitoring-in-Operations-Manager.md)  
[How to Configure a Computer for Agentless Management](../../om/manage/How-to-Configure-a-Computer-for-Agentless-Management.md)  
  
