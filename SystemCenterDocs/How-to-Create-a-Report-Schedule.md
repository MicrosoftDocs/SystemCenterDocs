---
title: How to Create a Report Schedule
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c2e5750-f222-4642-9fc8-a22461cfc506
---
# How to Create a Report Schedule
Use the following procedure to create a schedule to save a report. Make sure that you have created an Availability report and saved it as a favorite before using this procedure. For more information about creating an Availability report, see [How to Create an Availability Report](./How-to-Create-an-Availability-Report.md) and for more information about saving a report as a favorite, see [How to Save a Report](./How-to-Save-a-Report.md).

### To create a report schedule

1.  Log on to the computer with an account that is a member of the Operations Manager Report Operators role.

2.  In the Operations console, click **Reporting**.

3.  In the **Reporting** workspace, click **Favorite Reports**.

4.  In the **Favorite Reports** pane, right\-click the Availability report you saved as a favorite, and then click **Schedule**.

5.  In the **Subscribe to a Report Wizard**, on the **Delivery Settings** page, do the following:

    1.  Type a description in the **Description** text box.

    2.  Click the down arrow in the **Delivery method** list, and then click **Report Server File Share**.

        > [!NOTE]
        > If you want to manage and distribute reports securely, you could deliver reports to Microsoft Windows SharePoint Services, which offers digital rights management. Consult your network security administrator.

    3.  Type a file name for the report in the **File name** text box.

    4.  Type a file path for the report in the **Path** text box.

        > [!NOTE]
        > Report scheduling supports Universal Naming Convention \(UNC\) file names and must not end in a backslash.

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

## See Also
[Scheduling Reports](./Scheduling-Reports.md)
[How to Edit a Scheduled Report](./How-to-Edit-a-Scheduled-Report.md)
[How to Email Scheduled Reports](./How-to-Email-Scheduled-Reports.md)
[How to Schedule the Delivery of a Report to the SQL Report Server Cache](./How-to-Schedule-the-Delivery-of-a-Report-to-the-SQL-Report-Server-Cache.md)
[How to Cancel a Scheduled Report](./How-to-Cancel-a-Scheduled-Report.md)


