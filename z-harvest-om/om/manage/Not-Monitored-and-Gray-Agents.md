---
title: Not Monitored and Gray Agents
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a96716d-49f8-48a8-ac34-ca69e8f6363b
author:mgoedtel
manager:cfreemanwa
---
# Not Monitored and Gray Agents
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], you may see discovered objects in the Operations console displayed as not monitored or gray, as shown in the following illustration.  
  
![State view showing "not monitored"](../../om/manage/media/OM12NotMonitored.gif "OM12NotMonitored")  
  
The state view in the previous illustration contrasts two “unknown” states.  
  
-   The agent is shown as healthy, but the indicator is gray.  
  
-   The operating system is shown as not monitored.  
  
![Grayed-out healthy icon](../../om/manage/media/Healthygrayicon.gif "Healthygrayicon") The gray icon indicates that the health service watcher on the management server that is watching the health service on the monitored computer is not receiving heartbeats from the agent anymore. The health service watcher had received heartbeats previously and the state was reported as healthy. This also means that the management servers are no longer receiving any information from the agent.  
  
![White button indicates unknown status](../../om/manage/media/Unknownicon.gif "Unknownicon") The not monitored icon indicates that there are no monitors for the object. In the previous illustration, the view tells you that there are no monitors for the operating system on this computer. In this case, this is because the management packs for the Windows Server operating systems have not been imported in this management group.  
  
## What to do for a gray state  
Some of the common reasons for a gray state are:  
  
-   Heartbeat failure  
  
-   Health service is not running  
  
-   Incorrect configuration  
  
-   System workflows failure  
  
-   Operational or data warehouse database performance  
  
-   Management server or gateway server performance  
  
-   Network or authentication issues  
  
The **Show Gray Agent Connectivity Data** task will help you identify why an agent is gray.  
  
#### To check a gray agent for connectivity  
  
1.  Open the Operations console and click **Monitoring**.  
  
2.  Navigate to the Operations Manager\\Agent Details\\Agent Health State view.  
  
3.  In **Agent State from Health Service Watcher**, click the agent you want to check connectivity for.  
  
4.  In the **Tasks** pane, select the task **Show Gray Agent Connectivity Data**.  
  
5.  The **Run Task – Show Gray Agent Connectivity Data** dialog box appears. Click **Run**.  
  
6.  The Task Status dialog box appears. When the task is completed, you can click **Copy Text** or **Copy HTML** and paste the task output in the appropriate tool for further review.  
  
    The task output will identify the following information:  
  
    -   The last time a heartbeat was received from the agent.  
  
    -   Whether the System Center Management Health service is running on the agent.  
  
    -   Whether the agent responds to ping.  
  
    -   The last time the configuration on the agent was updated.  
  
    -   Possible reasons that the agent is unavailable.  
  
    -   The management server that the agent reports to.  
  
For information on troubleshooting, see the Knowledge Base article [Troubleshooting gray agent state](http://go.microsoft.com/fwlink/p/?LinkID=200488). Although the article was written for Operations Manager 2007, the troubleshooting steps will also be helpful for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)].  
  
## What to do for a not monitored state  
When an object shows as not monitored, check whether the appropriate management pack for monitoring the object is imported. Ensure that the appropriate monitors are enabled.  
  
Sometimes restarting the System Center Management Health service on the agent\-managed computer can resolve the issue. You can also try placing the object in maintenance mode for several minutes. For more information, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](../../om/manage/How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md).  
  
Next, check the DNS configuration for the computer, both FQDN and DNS suffix.  
  
An agent can also show as not monitored because the new agent has the same NetBIOS name as a previously installed agent. When the agent is deleted from Operations Manager, the grooming of the deleted agent is occurs after two days. Therefore, the agent is not immediately groomed out of the database completely. To work around this limitation, wait three days after deleting the agent to install the new agent.  
  
For more ideas for troubleshooting, see the blog post [Getting headaches trying to figure out why you are seeing the 'Not Monitored' state for Management Servers or Agents?](http://go.microsoft.com/fwlink/p/?LinkId=229513).  
  
## See Also  
[Using the Operations Manager Consoles](../../om/manage/Using-the-Operations-Manager-Consoles.md)  
[Finding Data and Objects in the Operations Manager Consoles](../../om/manage/Finding-Data-and-Objects-in-the-Operations-Manager-Consoles.md)  
[Using Views in Operations Manager](../../om/manage/Using-Views-in-Operations-Manager.md)  
[Using SharePoint to View Operations Manager Data](../../om/manage/Using-SharePoint-to-View-Operations-Manager-Data.md)  
[Subscribing to Alert Notifications](../../om/manage/Subscribing-to-Alert-Notifications.md)  
[Using Reports in Operations Manager](../../om/manage/Using-Reports-in-Operations-Manager.md)  
  
