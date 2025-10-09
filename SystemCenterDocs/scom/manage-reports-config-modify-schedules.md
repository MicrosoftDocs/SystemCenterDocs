---
ms.assetid: 197a4330-5b2e-4ccd-bfe2-4c93e2a6714b
title: Configure and Modify Report Schedules
description: This article describes how to configure and modify custom report schedules in Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Configure and modify report schedules



Operations Manager Reporting server component provides report-specific schedules to help you control the processing and distribution of reports. Once you've configured a schedule for a report, it can be managed from the Reporting workspace under the Scheduled Reports node in the Operations console.  

## Create a report schedule

Use the following procedure to create a schedule from a saved report. Report schedules can be created after the report opens or when saved as a Favorite report. The following steps will show you how to create a schedule from a saved report; however, the same steps for configuring the schedule can be performed from an open report by selecting **File**, **Schedule..** from the main menu.  

For more information on how to run and save a report, see [How to Run, Save, and Export a Report](manage-reports-run-save-export.md).

1.  Sign in to the computer with an account that is a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, select **Favorite Reports**.  

4.  In the **Favorite Reports** pane, right-click the Availability report you saved as a favorite, and select **Schedule**.  

5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:  

    1.  Enter a description in the **Description** text box.  

    2.  Select the down arrow in the **Delivery method** list, and select **Report Server File Share**.  

    3.  Enter a file name for the report in the **File name** text box.  

    4.  Enter a file path for the report in the **Path** text box. Report scheduling supports Universal Naming Convention (UNC) file names and must not end in a backslash.  

    5.  Select the down arrow in the **Render Format** list, and select the file format you want for the report.  

    6.  Enter a user name in the **User name** text box, and enter a password in the **Password** text box.  

        > [!NOTE]  
        > The credentials must have Write user rights on the file share.  

    7.  Select the down arrow in the **Write mode** list, select the Write mode you want for subsequent files, and select **Next**.  

6.  In the **Subscribe to a Report Wizard**, on the **Subscription Schedule** page, do the following:  

    1.  Select one of the **Generate the report** options.  

    2.  Enter a start date and start time for the reports to be generated in the **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in the **The subscription expires on** list, and select **Next**.  

7.  In the **Subscribe to a Report Wizard**, on the **Parameters** page, specify a span of time for the report in the **From** and **To** lists.  

8.  Make any other changes you need for this report, and select **Finish**.  


## Email scheduled reports

The report server email delivery extension isn't configured by default. You must use the Reporting Services Configuration Manager to minimally configure the extension. For more  information on how to configure SQL Server Reporting Services for email delivery, see [Configure a Report Server for E-Mail Delivery (SSRS Configuration Manager)](/sql/reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager).


### Configure email settings in the SQL Server Report Server  

1. Verify that the Report Server Windows service has **Send As** permissions on the SMTP server.

2. Start the **Reporting Services Configuration Manager** and connect to the report server instance.

3. On the **Email Settings** page, enter the name of the SMTP server. This value can be an IP address, a UNC name of a computer on your corporate intranet, or a fully qualified domain name.

4. In **Sender Address**, enter the name of an account that has permission to send email from the SMTP server.

5. Select **Apply** and select **Exit**.


### Email scheduled reports  

1.  Sign in to the computer with an account that is a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, select **Favorite Reports**.  

4.  In the **Favorite Reports** pane, right-click a report you saved as a favorite, and select **Schedule**.  

5.  In the Subscribe to a Report Wizard, on the **Delivery Settings** page, do the following:  

    1. Enter a description in the **Description** text box.  

    2. Select the down arrow in the **Delivery method** list, and select **Report Server E-Mail**.  

    3. Enter an email address of the destination inbox to receive reports in the **To** text box. You can also enter email addresses in the **Cc**, **Bcc**, and the **Reply To** text boxes.  

    4. Select the down arrow in the **Render Format** list, and select the file format you want for the report.  

    5. Select the down arrow in the **Priority** list, and then select the appropriate priority.  

    6. Enter a subject for the email in the **Subject** text box.  

    7. Select **Next**.  

6.  On the **Subscription Schedule** page, do the following:  

    1. Select one of the **Generate the report** options.  

    2. Enter a start date and start time for the reports to be generated in  **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription expires on** list, and select **Next**.  

7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and select **Finish**.


## Edit a scheduled report  

Use the following procedure to edit settings for scheduled reports from the **Reporting** pane in Operations Manager:

1.  Sign in to the computer with an account that is a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, select **Scheduled Reports**.  

4.  In the **Scheduled Reports** pane, right-click the scheduled report you want to edit, and select **Edit Schedule**.  

5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, if you select the **Windows File Share** as a **Delivery method**, you must enter the password in the **Password** text box before you can make any other changes.  

6.  Enter any other changes you need on the **Delivery Settings** page, and select **Next**.  

7.  Enter any changes you need to make on the **Subscription Schedule** page, and select **Next**.  

8.  Enter any changes you need to make on the **Report Parameters** page, and select **Finish.**  

## Cancel a scheduled report  

Use the following procedure to cancel scheduled reports:

1.  Sign in to the computer with an account that's a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, select **Scheduled Reports**.  

4.  In the **Scheduled Reports** pane, right-click the scheduled report you want to cancel, and select **Cancel Schedule**.  

5.  In the **System Center Operations Manager** dialog, select **OK** to confirm the deletion of your schedule or select **No** to keep your schedule.  


## Schedule the delivery of a report to the SQL Report Server Cache  

You can create a schedule for sending reports to the cache in the SQL Server Report Server and thereby shorten the time required to retrieve a report if the report is large or accessed frequently. For more information about report caching, see [Caching Reports (SSR)](/sql/reporting-services/report-server/caching-reports-ssrs).  

The example in this procedure uses an availability report that you've already created and saved as a favorite.

1.  Sign in to the computer with an account that's a member of the Operations Manager Report Operators role.  

2.  In the Operations console, select **Reporting**.  

3.  In the **Reporting** workspace, select **Favorite Reports**.  

4.  In the **Favorite Reports** pane, right-click the availability report you saved as a favorite, and select **Schedule**.  

5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:  

    1.  Enter a description in the **Description** text box.  

    2.  Select the down arrow in the **Delivery method** list, and select **Null Delivery Provider**.  

    3.  Select **Next**.  

6.  On the **Subscription Schedule** page, do the following:  

    1.  Select one of the **Generate the report** options.  

    2.  Enter a start date and start time for the reports to be generated in **The Subscription is effective beginning** list. You can also enter the date when this subscription will end in **The subscription will end** list, and select **Next**.  

7.  On the **Parameters** page, specify a span of time for the report in the **From** and **To** lists, make any other changes you need for this report, and select **Finish**.  

## Next steps

[Run, Save, and Export a Report](manage-reports-run-save-export.md) walks you through how to preview your reports, save them with specific report parameters to minimize repeated entry of information or to simplify the experience for your report users, and how to export the report to different file formats.
