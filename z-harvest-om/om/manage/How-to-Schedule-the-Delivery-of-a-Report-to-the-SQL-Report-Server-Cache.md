---
title: How to Schedule the Delivery of a Report to the SQL Report Server Cache
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 859a9382-b636-41e6-bb8d-017e0cf53226
author:mgoedtel
manager:cfreemanwa
---
# How to Schedule the Delivery of a Report to the SQL Report Server Cache
You can create a schedule for sending reports to the cache in the SQL Server&nbsp;Report Server and thereby shorten the time required to retrieve a report if the report is large or accessed frequently. For more information about report caching, see [Caching Reports \(SSRS\)](http://go.microsoft.com/fwlink/?LinkId=77536).  
  
The example in this procedure uses an availability report that you have already created and saved as a favorite. For more information about creating an availability report, see [How to Create an Availability Report](../../om/manage/How-to-Create-an-Availability-Report.md). For more information about saving a report as a favorite, see [How to Save a Report](../../om/manage/How-to-Save-a-Report.md).  
  
### To schedule the delivery of a report to the SQL Report Server Cache  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Favorite Reports**.  
  
4.  In the **Favorite Reports** pane, right\-click the availability report you saved as a favorite, and then click **Schedule**.  
  
5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:  
  
    1.  Type a description in the **Description** text box.  
  
    2.  Click the down arrow in the **Delivery method** list, and then click **Null Delivery Provider**.  
  
    3.  Click **Next**.  
  
6.  On the **Subscription Schedule** page, do the following:  
  
    1.  Select one of the **Generate the report** options.  
  
    2.  Type a start date and start time for the reports to be generated in **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription will end** list, and then click **Next**.  
  
7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and then click **Finish**.  
  
## See Also  
[Scheduling Reports](../../om/manage/Scheduling-Reports.md)  
[How to Create a Report Schedule](../../om/manage/How-to-Create-a-Report-Schedule.md)  
[How to Email Scheduled Reports](../../om/manage/How-to-Email-Scheduled-Reports.md)  
[How to Edit a Scheduled Report](../../om/manage/How-to-Edit-a-Scheduled-Report.md)  
[How to Cancel a Scheduled Report](../../om/manage/How-to-Cancel-a-Scheduled-Report.md)  
  
