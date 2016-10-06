---
ms.assetid: 197a4330-5b2e-4ccd-bfe2-4c93e2a6714b
title: How to Configure and Modify Report Schedules 
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Configure and Modify Report Schedules

>Applies To: System Center 2016 - Operations Manager

Operations Manager Reporting server component provides report-specific schedules to help you control processing and distribution of reports.  Once you have configured a schedule for a report, it can be managed from the Reporting workspace, under the Scheduled Reports node in the Operations console.  

## To create a report schedule

Use the following procedure to create a schedule from a saved report.  Report schedules can be created after the report open or when saved as a Favorite report.  The following steps will show you how to create a schedule from a saved report, however; the same steps for configuring the schedule can be performed from an open report by selecting **File**, **Schedule..** from the main menu.  

For more information on how to run and save a report, see [How to Run, Save, and Export a Report](how-to-run-save-export-reports.md).
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Favorite Reports**.  
  
4.  In the **Favorite Reports** pane, right-click the Availability report you saved as a favorite, and then click **Schedule**.  
  
5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:  
  
    1.  Type a description in the **Description** text box.  
  
    2.  Click the down arrow in the **Delivery method** list, and then click **Report Server File Share**.  
  
    3.  Type a file name for the report in the **File name** text box.  
  
    4.  Type a file path for the report in the **Path** text box.  Report scheduling supports Universal Naming Convention \(UNC\) file names and must not end in a backslash.  
  
    5.  Click the down arrow in the **Render Format** list, and then click the file format you want for the report.  
  
    6.  Type a user name in the **User name** text box, and then type a password in the **Password** text box.  
  
        > [!NOTE]  
        > The credentials must have Write user rights on the file share.  
  
    7.  Click the down arrow in the **Write mode** list, select the Write mode you want for subsequent files, and then click **Next**.  
  
6.  In the **Subscribe to a Report Wizard**, on the **Subscription Schedule** page, do the following:  
  
    1.  Select one of the **Generate the report** options.  
  
    2.  Type a start date and start time for the reports to be generated in  **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription expires on** list, and then click **Next**.  
  
7.  In the **Subscribe to a Report Wizard**, on the **Parameters** page, specify a span of time for the report in the **From** and **To** lists.  
  
8.  Make any other changes you need for this report, and then click **Finish**.  


## How to Email scheduled reports

The report server e-mail delivery extension is not configured by default. You must use the Reporting Services Configuration Manager to minimally configure the extension.  For additional  information on how to configure SQL Server Reporting Services for e-mail delivery, see [Configure a Report Server for E-Mail Delivery (SSRS Configuration Manager)](https://technet.microsoft.com/library/ms159155%28v=sql.120%29.aspx).


### Configure email settings in the SQL Server Report Server  

1. Verify that the Report Server Windows service has **Send As** permissions on the SMTP server.

2. Start the **Reporting Services Configuration Manager** and connect to the report server instance.

3. On the **Email Settings** page, enter the name of the SMTP server. This value can be an IP address, a UNC name of a computer on your corporate intranet, or a fully qualified domain name.

4. In **Sender Address**, enter the name an account that has permission to send e-mail from the SMTP server.

5. Click **Apply** and then click **Exit**.
 
  
### E-mail scheduled reports  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Favorite Reports**.  
  
4.  In the **Favorite Reports** pane, right-click a report you saved as a favorite, and then click **Schedule**.  
  
5.  In the Subscribe to a Report Wizard, on the **Delivery Settings** page, do the following:  
  
    1. Type a description in the **Description** text box.  
  
    2. Click the down arrow in the **Delivery method** list, and then click **Report Server E-Mail**.  
  
    3. Type an email address of the destination inbox to receive reports in the **To** text box. You can also type email addresses in the **Cc**, **Bcc**, and the **Reply To** text boxes.  
  
    4. Click the down arrow in the **Render Format** list, and then click the file format you want for the report.  
  
    5. Click the down arrow in the **Priority** list, and then select the appropriate priority.  
  
    6. Type a subject for the email in the **Subject** text box.  
  
    7. Click **Next**.  
  
6.  On the **Subscription Schedule** page, do the following:  
  
    1. Select one of the **Generate the report** options.  
  
    2. Type a start date and start time for the reports to be generated in  **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription expires on** list, and then click **Next**.  
  
7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and then click **Finish**.    

  
## Edit a scheduled report  

Use the following procedure to edit settings for scheduled reports from the **Reporting** pane in Operations Manager.
  
1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Scheduled Reports**.  
  
4.  In the **Scheduled Reports** pane, right-click the scheduled report you want to edit, and then click **Edit Schedule**.  
  
5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, if you select the **Windows File Share** as a **Delivery method**, you must type the password in the **Password** text box before you can make any other changes.  
  
6.  Type any other changes you need on the **Delivery Settings** page, and then click **Next**.  
  
7.  Type any changes you need to make on the **Subscription Schedule** page, and then click **Next**.  
  
8.  Type any changes you need to make on the **Report Parameters** page, and then click **Finish.**  

  
## Cancel a scheduled report  

Use the following procedure to cancel scheduled reports.  

1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Scheduled Reports**.  
  
4.  In the **Scheduled Reports** pane, right-click the scheduled report you want to cancel, and then click **Cancel Schedule**.  
  
5.  In the **System Center Operations Manager** dialog box, click **OK** to confirm the deletion of your schedule or click **No** to keep your schedule.  


## Schedule the delivery of a report to the SQL Report Server Cache  
  
You can create a schedule for sending reports to the cache in the SQL Server Report Server and thereby shorten the time required to retrieve a report if the report is large or accessed frequently. For more information about report caching, see [Caching Reports (SSR)](https://msdn.microsoft.com/library/ms155927.aspx).  
  
The example in this procedure uses an availability report that you have already created and saved as a favorite. 

1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.  
  
2.  In the Operations console, click **Reporting**.  
  
3.  In the **Reporting** workspace, click **Favorite Reports**.  
  
4.  In the **Favorite Reports** pane, right-click the availability report you saved as a favorite, and then click **Schedule**.  
  
5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:  
  
    1.  Type a description in the **Description** text box.  
  
    2.  Click the down arrow in the **Delivery method** list, and then click **Null Delivery Provider**.  
  
    3.  Click **Next**.  
  
6.  On the **Subscription Schedule** page, do the following:  
  
    1.  Select one of the **Generate the report** options.  
  
    2.  Type a start date and start time for the reports to be generated in **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription will end** list, and then click **Next**.  
  
7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and then click **Finish**.  

## Next steps

- [How to Run, Save, and Export a Report](how-to-run-save-export-reports.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats. 


  
