---
title: How to Save a Report
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2ff6edc-1c30-4219-9ca7-82ef5f149170
---
# How to Save a Report
When you run a report, you can save the report to **Favorite Reports** or you can save a report into an existing management pack. A report saved to **Favorite Reports** is only visible to you. Saving a report to a management pack is useful if you need to share with report users a report that uses a specific set of parameters.

The following steps outline the procedure for saving a report to a management pack:

1.  Run a report \(from the generic report library or from a management pack, such as the SQL Server management pack\). Specify the parameters you want to for the report and click **Run**.

2.  When the report renders, validate that it contains the information you need.

3.  On the **File** menu, click **Save to management pack**.

4.  Follow the instructions in the wizard to save the report.

After the wizard completes, the management pack is saved to Operations Manager and then later deployed to the report server and is made available for all report operators.

> [!NOTE]
> Be aware of the following when saving reports:
> 
> -   Reports can be saved to a management pack from **Favorite Reports**.
> -   Reports cannot be saved to a management pack from authored reports.
> 
> Management packs can be exported and imported into other management groups and the reports will work only when these management groups share the same data warehouse.
> 
> Only users with administrator authorization can save reports to management packs.

## See Also
[Using Reports in Operations Manager](Using-Reports-in-Operations-Manager.md)
[How to Create Reports in Operations Manager](How-to-Create-Reports-in-Operations-Manager.md)
[Operations Manager Reports Library](Operations-Manager-Reports-Library.md)
[How to Run a Report](How-to-Run-a-Report.md)
[Scheduling Reports](Scheduling-Reports.md)
[Operations Manager Reports Library](Operations-Manager-Reports-Library.md)
[How to Troubleshoot Reports that Return No Data](How-to-Troubleshoot-Reports-that-Return-No-Data.md)


