---
title: "Downloading and Sharing Global Service Monitor Web Tests and Results | Microsoft Docs"
ms.custom: ""
ms.date: 05/18/2016
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.tgt_pltfrm: ""
ms.topic: article
applies_to: System Center 2016 - Operations Manager
ms.assetid: 47139f31-4641-42dc-95ad-9917fe197fbf
author: mgoedtel
ms.author: magoedte
manager: carmonm
---
# Downloading and Sharing Global Service Monitor Web Tests and Results
[!INCLUDE[gsmshort](../includes/gsmshort-md.md)] web tests report basic information about test performance and application availability. To investigate the results of a specific test run, you can download the actual web test result file from GSM, and share it with your Development and Operations (DevOps) teams that can open and use it in Visual Studio. This lets you directly interact with the web test result file in the same familiar Visual Studio environment in which the web test was created. You can automatically or manually download web test results for a specific web test run.  
  
> [!IMPORTANT]
>  Before you begin, you must import and configure the Alert Attachment management pack. For more information, see [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=307114) or [How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=275127). Additionally, to further integrate this workflow with your DevOps processes, you can synchronize these alerts and their attached web test results with Team Foundation Server (TFS) work items by downloading the TFS Work Item Synchronization management pack. For more information, see [How to Configure Integration with TFS in System Center 2012 R2](http://go.microsoft.com/fwlink/?LinkId=307113) or [How to Configure Integration with TFS in System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=275126)  
  
## Downloading Web Test Results  
 There are two ways to download Visual Studio web test result files. You can automatically download web test result files as attachments by configuring the Alert Attachment management pack. As soon as you configure the Alert Attachment management pack, alerts generated from Visual Studio Web Test template will download the web test result file for the test run associated with that alert. Also, you can manually download web test result files to view results for test runs not associated with an alert.  
  
> [!NOTE]
>  Access to the share where web test result files are placed is configured in the Alert Attachment management pack. If an operations administrator needs to access web test results files, make sure that their account has been granted permissions to the share where the web test files are placed.  
  
#### To automatically download and access web test results from alerts  
  
1.  Configure the Alert Attachment management pack. After you configure the Alert Attachment management pack, alerts generated from the Visual Studio Web Test template download the web test result file for the test run associated with that alert. For more information, see How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1  
  
2.  To access web test result file for a given alert, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Monitoring**, expand **Application Monitoring**, expand **Visual Studio Web Test Monitoring**, and then click **Active Alerts**.  
  
3.  Select the alert you want to investigate, and in the **Tasks** pane, in the **Alert Attachment Tasks** section, click **Open Attachment Location**. This opens the location of the folder that contains the web test results file for that alert.  
  
4.  Alerts and their attachments can be automatically or manually assigned as work items in Team Foundation Server (TFS), which makes it easy for the development team to investigate and resolve issues in their familiar development environment that were brought to your attention via GSM. For more information, see How to Configure Integration with TFS in System Center 2012 SP1  
  
#### To manually download and access web test results from alerts  
  
1.  Configure the Alert Attachment management pack. For more information, see How to Configure File Attachments for Operations Manager Alerts in System Center 2012 SP1  
  
2.  To manually download and access web test result files, in the [!INCLUDE[om12short](../includes/om12short-md.md)] console, in the navigation pane, click **Monitoring**, expand **Application Monitoring**, expand **Visual Studio Web Test Monitoring**, and then click **Test State**.  
  
3.  Select one or more tests. In the **Tasks** pane, in the **Visual Studio Web Test Monitoring Test Tasks** section, and then click **Download test result file**.  
  
4.  On the **Run Task** page, validate that you have selected the correct tests, and then click **Run**.  
  
5.  On the **Task Status** page, you can select a test and a link to the web test result file is in the **Task Output** section.  
  
6.  To open the web test result, click the link or copy the link to use later.