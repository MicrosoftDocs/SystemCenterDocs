---
title: Not Monitored and Gray Agents
description: "This article describes how Operations Manager detects and reports when an agent isnt communicating and reporting monitoring data as expected."
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.date: 02/04/2026
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 4a96716d-49f8-48a8-ac34-ca69e8f6363b
---

# Not monitored and gray agents

In System Center Operations Manager, you might see discovered objects in the Operations console that appear as not monitored or gray, as shown in the following illustration.  

:::image type="content" source="./media/manage-agents-not-healthy/om2016-operations-console-windowscomputer-healthstate.png" alt-text="Illustration showing State view showing 'not monitored'.":::

The state view in the previous illustration contrasts two "unknown" states.  

- The agent is healthy, but the indicator is gray.  

- The operating system is not monitored.  

:::image type="content" source="./media/manage-agents-not-healthy/om2016-healthygrayicon.png" alt-text="Screenshot of Grayed-out healthy icon."::: The gray icon indicates that the health service watcher on the management server that is watching the health service on the monitored computer isn't receiving heartbeats from the agent anymore. The health service watcher previously received heartbeats and reported the state as healthy.  This condition also means that the management servers no longer receive any information from the agent.    


:::image type="content" source="./media/manage-agents-not-healthy/om2016-unknownicon.png" alt-text="Screenshot of White button indicates unknown status."::: The not monitored icon indicates that there are no monitors for the object. In the previous illustration, the view tells you that there are no monitors for the operating system on this computer. In this case, this condition exists because the management packs for the Windows Server operating systems aren't imported in this management group.  


## What to do for a gray state  

Some common reasons for a gray state include:  

- Heartbeat failure  

- Health service isn't running  

- Incorrect configuration  

- System workflows failure  

- Operational or data warehouse database performance  

- Management server or gateway server performance  

- Network or authentication issues  

- Computer name changed after agent installation

The **Show Gray Agent Connectivity Data** task helps you identify why an agent is gray.  

## Check a gray agent for connectivity  

1. Open the Operations console and select **Monitoring**.  

2. Go to the **Operations Manager\Agent Details\Agent Health State** view.    

3. In **Agent State from Health Service Watcher**, select the agent you want to check connectivity for.    

4. In the **Tasks** pane, select the task **Show Gray Agent Connectivity Data**.    

5. The **Run Task - Show Gray Agent Connectivity Data** dialog appears. Select **Run**.    

6. The Task Status dialog appears. When the task finishes, you can select **Copy Text** or **Copy HTML** and paste the task output in the appropriate tool for further review.    

    The task output shows the following information:  

    - The last time a heartbeat was received from the agent.  

    - Whether the System Center Management Health service is running on the agent.  

    - Whether the agent responds to a ping.  

    - The last time the configuration on the agent was updated.  

    - Possible reasons that the agent is unavailable.  

    - The management server that the agent reports to.  

For information on troubleshooting, see the Knowledge Base article [Troubleshooting gray agent state](https://support.microsoft.com/kb/2288515). Although the article was written for Operations Manager 2007 and 2012, the troubleshooting steps are also helpful for Operations Manager 2016 and later.  

## What to do for a not monitored state

When an object shows as not monitored, check whether you imported the appropriate management pack for monitoring the object. Make sure that you enabled the appropriate monitors.  

Sometimes, restarting the Microsoft Monitoring Agent service on the agent-managed computer or clearing the agent cache resolves the problem. To clear the cache on the agent, see [How to clear the cache](manage-clear-healthservice-cache.md). You can also try placing the object in maintenance mode for several minutes. For more information, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](manage-maintenance-mode-overview.md).  

Next, check the DNS configuration for the computer, both FQDN and DNS suffix.  

An agent can also show as not monitored because the new agent has the same NetBIOS name as a previously installed agent. When you delete the agent from Operations Manager, the grooming of the deleted agent occurs after two days. Therefore, the agent isn't immediately removed from the database. To work around this limitation, wait for three days after deleting the agent to install the new agent.  

## Next steps

- To understand how it can help you review alerts that the rules and monitors generate and are still active, review [Viewing Active Alerts and Details](manage-alert-view-alerts-details.md).  

- To understand how Operations Manager monitors the communication channel between an agent and its primary management server to ensure it's responsive and available, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).

- In the Operations console, you view monitoring data, manage monitoring configuration, create your own custom views and dashboards that are personalized for your experience, and perform management group configuration administration by [Using the Operations Manager Operations console](manage-consoles-overview.md).
