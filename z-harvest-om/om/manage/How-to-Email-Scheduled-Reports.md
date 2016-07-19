---
title: How to Email Scheduled Reports
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 786b7295-6591-4c26-bec6-dabf5e5f9ff9
author:mgoedtel
manager:cfreemanwa
---
# How to Email Scheduled Reports
Before you can schedule a report for email delivery, you must configure the email settings in the Report Server using the Reporting Server Configuration Manager.  
  
The example in this procedure uses an availability report that you have already created and saved as a favorite. For more information about creating an availability report, see [How to Create an Availability Report](../../om/manage/How-to-Create-an-Availability-Report.md). For more information about saving a report as a favorite, see [How to Save a Report](../../om/manage/How-to-Save-a-Report.md).  
  
### To configure email settings in the SQL Server Report Server  
  
1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, point to **Configuration Tools**, and then click **Reporting Services Configuration**.  
  
2.  In **Reporting Services Configuration Manager**, in the **Report Server Installation Instance Selection** dialog box, click **Connect**.  
  
3.  In the navigation pane, click **E\-mail Settings**.  
  
4.  In the **E\-mail Settings** pane, enter the following:  
  
    -   An email address for use as the sender address in the **Sender Address** text box.  
  
    -   The address of the SMTP server that will be used to send the email messages in the **SMTP Server** text box.  
  
5.  Click **Apply**, and then click **Exit**.  
  
### To email scheduled reports  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Favorite Reports**.  
  
4.  In the **Favorite Reports** pane, right\-click the Availability report you saved as a favorite, and then click **Schedule**.  
  
5.  In the Subscribe to a Report Wizard, on the **Delivery Settings** page, do the following:  
  
    -   Type a description in the **Description** text box.  
  
    -   Click the down arrow in the **Delivery method** list, and then click **Report Server E\-Mail**.  
  
    -   Type an email address of the destination inbox to receive reports in the **To** text box. You can also type email addresses in the **Cc**, **Bcc**, and the **Reply To** text boxes.  
  
    -   Click the down arrow in the **Render Format** list, and then click the file format you want for the report.  
  
    -   Click the down arrow in the **Priority** list, and then select the appropriate priority.  
  
    -   Type a subject for the email in the **Subject** text box.  
  
    -   Click **Next**.  
  
6.  On the **Subscription Schedule** page, do the following:  
  
    -   Select one of the **Generate the report** options.  
  
    -   Type a start date and start time for the reports to be generated in  **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription expires on** list, and then click **Next**.  
  
7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and then click **Finish**.  
  
## See Also  
[Scheduling Reports](../../om/manage/Scheduling-Reports.md)  
[How to Create a Report Schedule](../../om/manage/How-to-Create-a-Report-Schedule.md)  
[How to Edit a Scheduled Report](../../om/manage/How-to-Edit-a-Scheduled-Report.md)  
[How to Schedule the Delivery of a Report to the SQL Report Server Cache](../../om/manage/How-to-Schedule-the-Delivery-of-a-Report-to-the-SQL-Report-Server-Cache.md)  
[How to Cancel a Scheduled Report](../../om/manage/How-to-Cancel-a-Scheduled-Report.md)  
  
