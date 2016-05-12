---
title: How to Create a Runbook Automation Activity Template
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f3f00f2-f9a9-407c-8974-109609988907
robots: noindex,nofollow
---
# How to Create a Runbook Automation Activity Template
After you import runbooks into [!INCLUDE[smlong12](Token/smlong12_md.md)] using the Orchestrator connector from [!INCLUDE[orchlong](Token/orchlong_md.md)], you can create a runbook automation activity template to map parameters in [!INCLUDE[orchshort](Token/orchshort_md.md)] to corresponding parameters in [!INCLUDE[smshort](Token/smshort_md.md)].

As an example, you can implement a new request offering using an [!INCLUDE[orchshort](Token/orchshort_md.md)] runbook to automate it. Then, you can go to the Runbooks view in the Library workspace, select a runbook, and create a runbook automation activity template. You can go to the templates view and verify that the template is created. You can then add the [!INCLUDE[orchshort](Token/orchshort_md.md)] activity template to a service request template and create the request offering. You then can then map the runbook template to a different runbook with the same inputs and outputs if you find that you need to fix a problem or improve the process.

> [!IMPORTANT]
> If you have extended root classes such as service request or release record, then you can map runbook activity parameter to extended properties only if the runbook activity template and service request templates are saved in same management pack where the definition extension is located.

### To create a runbook automation activity template

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, click **Runbooks**.

3.  In the **Runbooks** view, select a runbook.

4.  In the **Tasks** pane, under **<RunbookName>**, click **Create Runbook Automation Activity Template** to open the **Create Template** dialog box.

5.  In the **Name** box, type a name for the template.

6.  Optionally, in the **Description** box, type a description for the template.

7.  If necessary, select an unsealed management pack to save the template to, and then click **OK**. You will use this management pack later to retrieve the runbook automation activity template from another work item template, such as a service request template.

8.  In the Runbook Activity Template: <TemplateName> form, on the **General** tab, type information for **Title**, **Description**, **Area**, **Stage**, **Assigned To**, and **Designer**.

9. Ensure that **Is Ready for Automation** is selected.

10. Select the **Runbook** tab, and then under **Parameter Mapping**, note that the parameters from the runbook are mapped to generic properties—for example, Parameter1, Parameter2, and so on—of the runbook activity class. The **Type** column specifies whether the parameters are inputs or outputs. You can also type default values for each parameter using **Edit Mapping**.

11. For any parameter, click **Edit Mapping**.

12. Expand **Object**, and then click **Id**. This ID value will be used by the [!INCLUDE[orchshort](Token/orchshort_md.md)] runbook to find the particular runbook activity that is being executed. Click **Close**.

13. Click **OK** to close the form and create the template.


