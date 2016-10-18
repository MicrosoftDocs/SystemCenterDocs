---
title: Running Runbooks
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce5772aa-dec1-4158-ba54-c58f4e019633
ms.author: cfreeman
ms.date: 10/12/2016
author: cfreemanwa
manager: cfreeman
---
# Running Runbooks

> Applies To: System Center 2016 - Orchestrator

This topic describes the process for starting runbooks, viewing the results, and stopping a job in the Runbook Designer.  

#### To start a runbook  

1.  In the Runbook Designer, in the **Connections** pane, click the **Runbooks** folder to see the available runbooks.  

2.  In the Design workspace, click a runbook tab.  

3.  If the runbook is Checked Out, select the **Check In** button.  

4.  In the Design workspace, right-click the runbook tab and select **Run**.  

5.  In the **Start Runbook** dialog box, go to **Available Runbook Server\(s\)** box and select the applicable server.  

6.  Click the Arrow button so that the server name is now in the **Selected Runbook Servers\(s\)** box.  

7.  Click **Start**.  

#### To find events  

1.  Click **Start**, point to **All Programs**, click **Administrative Tools**, and then click **Event Viewer** to open a session.  

2.  On the **Event Viewer** menu, double\-click **Windows Logs**, and then on the menu, click **Application**.  

#### To stop a job from the Runbook Designer  

1.  In **Runbook Designer**, click the **Monitor Runbook** tab.  

2.  On the toolbar, click **Stop**.  

## See Also  
[Deploy and Start Runbooks](../deploy/deploy-and-start-runbooks.md)  
