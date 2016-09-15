---
title: Resolving Heartbeat Alerts
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.tgt_pltfrm: na
ms.topic: article
---

# Resolving Heartbeat Alerts

The Health Service sends a heartbeat to a management server to verify that the system is still responding. When a specified number of heartbeats fail to arrive, System Center 2016 - Operations Manager displays an alert.  
  
This section shows how to investigate a Health Service Heartbeat Failure alert as an example. Different alerts have different causes and different resolutions.  
  
If you want to walk through these procedures, you can cause this alert by disabling the System Center Management service on a test system.  
  
### To cause a Health Service heartbeat failure alert for testing  
  
1.  On a computer with an agent installed, open Control Panel.  
  
2.  Double\-click **Administrative Tools**.  
  
3.  Double\-click **Services**.  
  
4.  Right\-click the **System Center Management** service, and then click **Stop**.  
  
    > [!NOTE]  
    > Use this same procedure and select **Start** in step 4 when you are done testing.  
  
## How to investigate agent heartbeat issues  

The **Monitoring** workspace displays active alerts. Looking at an alert provides information and tools to investigate with.  
  
### To investigate an active alert  
  
1.  Open the Operations console.  
  
2.  Click **Monitoring**.  
  
3.  Click **Active Alerts** to view the **Health Service Heartbeat Alert**.  
  
    > [!NOTE]  
    > Depending on the heartbeat interval and the number of missing heartbeats, a few minutes might be required to see the alert.  
  
4.  Click the alert to highlight it and read the information in the **Alert Details** area. The **Alert Details** area provides information about the alert, including a description and knowledge about the cause and resolution.  
  
## How to troubleshoot agent heartbeat issues  

Use the tasks in the **Tasks** pane to diagnose the cause of the alert. Different alerts have different tasks. For a Health Service Heartbeat Failure alert, the tasks deal with pinging the system and verifying or restarting the service.  
  
### To use the action tasks in troubleshooting  
  
1.  In the **Tasks** pane, under **Health Service Watcher Tasks**, click **Ping Computer**. The task opens a dialog box to display its progress.  
  
    > [!NOTE]  
    > If the ping fails, use standard networking troubleshooting to figure out the issue with connectivity. Verify that the system is turned on.  
  
2.  Click **Close** to close the dialog box.  
  
3.  Under **Health Service Watcher Tasks**, click **Computer Management**. A **Computer Management** dialog box for the target system opens.  
  
4.  Click **Services and Applications** to expand it.  
  
5.  Click **Services** to display services.  
  
6.  Right\-click the **System Center Management** service, and then click **Start**.  
  
    > [!NOTE]  
    > After the connection with the agent is restored, the alert will be automatically resolved and the computer status will return to healthy.  
  
These steps will fix the test failure created in this topic, as well as address a number of possible causes of a Health Service Heartbeat Failure. If an actual failure is not resolved by these steps, use standard troubleshooting techniques to figure out the cause of the issue. For instance, the alert displayed in **Active Alerts** shows how old the alert is. Check for events that happened at this time to see what might have caused an issue.  
  
A sudden increase in the number of alerts is called an alert storm. An alert storm can be a symptom of massive changes of some kind within your management group, such as catastrophic failure of networks. An alert storm can also be a symptom of configuration issues within Operations Manager. A newly imported management pack starts monitoring immediately. If you have a large number of managed computers, an unforeseen configuration issue could cause a large increase in alerts.  
  
## Next steps

- Before changing the number of missed heartbeats allowed. first review [How Heartbeats Work in Operations Manager](How-Heartbeats-Work.md)  
