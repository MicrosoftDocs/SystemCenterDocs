---
title: Identifying the Computer Experiencing a Problem
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Identifying the computer experiencing a problem

This topic helps you answer questions such as "I see an alert that says logical disk defragmentation is high. Where is it high?"  
  
## How to identify the computer experiencing a problem  
  
1.  Select the alert in the Active Alerts view.  
  
    ![Select alert in Results pane](./media/identifying-the-computer-experiencing-a-problem/om2016-view-active-alerts.png)  
  
2.  Look in the **Details** section for the **Path**.  
  
    ![See Path in alert details](./media/identifying-the-computer-experiencing-a-problem/om2016-view-alert-details.png)  
  
    Notice that this alert also includes the affected computer in the **Description**.  
  
3.  Click **Windows Computers** to view the state of the computer.  
  
    ![Windows Computers monitoring view](./media/identifying-the-computer-experiencing-a-problem/om2016-stateview-windowscomputers.png)  
  
4.  Right-click the computer, point to **Open**, and click **Health Explorer**:  
  
    ![Open Health Explorer](./media/identifying-the-computer-experiencing-a-problem/om2016-healthexplorer-windowscomputer.png)  
  
In this illustration, you see that the logical disk fragmentation levels for C: and D: on this computer are in a warning state. Notice that the state rolls up to the **Performance** state for each disk, then to **Hardware Performance** for the computer, then to **Performance** for the computer, and finally to **Entity Health** for the computer.  
  
## Next steps
  
- To help you investigate and resolve the issues that caused the alerts, review [Viewing Active Alerts and Details](manage-alert-view-alerts-details.md)

