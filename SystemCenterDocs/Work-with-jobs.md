---
title: Work with jobs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab418c49-67ff-4405-b3c0-cf9d6afd56e6
---
# Work with jobs
You can interact with DPM jobs in a number of ways:

[View jobs](#BKMK_View)

[Retry a job](#BKMK_Retry)

[Cancel a job](#BKMK_Cancel)

[Check data protection job status](#BKMK_Status)

[Modify the jobs display](#BKMK_Display)

[Display job details](#BKMK_Details)

[Use filters](#BKMK_Filter)

## <a name="BKMK_View"></a>View jobs

1.  In the DPM Admistrator Console, go to **Monitoring** > **Jobs**:

    -   Use the **Filters** drop\-down list box to sort the list of jobs according to a selected set of parameters.

    -   Use the **Group by** drop\-down list box to group the list of jobs by protection group, computer, status, or type.

## <a name="BKMK_Retry"></a>Retry a job
If one or more jobs fail or are canceled by [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)], you can retry the jobs. If you manually cancel one or more jobs, they are deleted and can’t be retried. Retry a job as follows:

1.  In DPM Administrator Console, go to the **Monitoring** > **Jobs**.

2.  Click a job with **Failed** status, then click **Retry**. In the **Data Protection Manager** message box that appears, click **Yes**. A new job will be scheduled to run immediately. Note that Rescheduling a job doesn’t remove the entry on the **Jobs** display for the failed job.

## <a name="BKMK_Cancel"></a>Cancel a job
You can cancel single or multiple jobs as follows:

1.  In DPM Administrator Console, open **Monitoring** > **Jobs**

2.  Group by **Status**. Select the scheduled job, and click **Cancel** > **Yes**. A job you cancel is deleted. However a job that’s canceled by DPM can be run again using **Retry**.

## <a name="BKMK_Status"></a>Check data protection job status
[!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] tracks the status of data protection jobs as scheduled, completed, canceled, or failed. Check status as follows:

1.  In DPM Administrator Console, go to **Monitoring** > **Jobs**.

2.  In the **Group by** list box, select **Status**. Review a a job in **Details**. Note that DPM implements a time out for jobs. If a job exceeds the timeout limit it generates an error as is marked as **Failed**.

## <a name="BKMK_Display"></a>Modify the Jobs display
You can customize the data on the **Jobs** tab to reflect the information that you want to see, and you can create filters to save display settings, as follows:

1.  In DPM Administrator Console, go to **Monitoring** > **Jobs**.

2.  Group by **Protection Group**, **Computer**, **Status**, or **Type** to group the displayed information by these categories.

3.  To sort jobs by column, in the display pane, click **Source**, **Computer**, **Protection Group**, **Type**, **Start Time**, **Time Elapsed**, or **Data Transferred**.

    The rest of the table then resorts relative to the column title that you click.

## <a name="BKMK_Details"></a>Display job details
Jobs can be grouped by **Protection Group**, **Computer**, **Status**, or **Type**. By default they’re grouped by status. You can use end times to find all job that failed in a specific period.  Display job details as follows:

1.  In DPM Administrator Console, go to **Monitoring** > **Jobs** and select the job. Information is displayed on the **Details** pane.

2.  e **Details** pane, in the lower part of the console.

3.  Alternatively use the Quick Search or filters to find jobs.

## <a name="BKMK_Filter"></a>Use filters
You can create and manage filters to help with jobs, as follows:

1.  In DPM Administrator Console, go to **Monitoring** > **Browse** > **Create filter** > **Create**.

2.  Specify a filter name, time or data options, jobs types and status, group by protection group or computer, and select the protection members for which you want to display information. You can also filter on external media, time elapset and amount of data transferred.

3.  Click **Preview** to preview the filtered jobs display, and then **Save**. **Refresh** the filter to detect configuration changes.

