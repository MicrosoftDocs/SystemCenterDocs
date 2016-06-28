---
title: Using Runbooks in System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0863ac5-05d9-46b3-8e18-1f76e50ee07d
---
# Using Runbooks in System Center 2016 - Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

Runbooks in Service Manger are used to automate procedures. The following sections provide details about the purpose and use of runbooks.

## About Runbooks in Service Manager

To automate processes in System Center, Orchestrator uses runbooks to automate procedures. Runbooks are visual representations of the procedures. The value that runbooks have is that they help ensure that Orchestrator automation is driven and tracked from Service Manager and that Service Manager interactions with other System Center products and non-Microsoft systems are much easier to implement.

Additionally, the Orchestrator workflow authoring interface is available for your custom Service Manager scenarios. Runbooks are imported into Service Manager using the Orchestrator connector. After the connector is synchronized, imported runbooks appear in the **Library** workspace under the **Runbooks** node in the Service Manager console, where you can view them and also create runbook automation activity templates.

## About Orchestrator
System Center - Orchestrator is an automation platform for orchestrating and integrating IT tools to drive down the cost of datacenter operations, while improving the reliability of IT processes. Orchestrator enables IT organizations to automate best practices, such as those that are found in the Microsoft Operations Framework (MOF) and Information Technology Infrastructure Library (ITIL). This is achieved through workflow processes that coordinate Microsoft and other management tools to automate incident response, change and compliance, and service-life-cycle management processes.

Through its workflow designer, Orchestrator automatically shares data and initiates tasks in System Center components, including Operations Manager, Service Manager, Virtual Machine Manager, Configuration Manager, Active Directory Domain Services (AD DS), and non-Microsoft tools. Orchestrator workflow automates IT infrastructure tasks, while  Service Manager workflow provides automation of human workflow. The combined offering ensures repeatable, consistent results by removing the latency associated with manual coordination service delivery. System Center and Orchestrator enable integration, efficiency, and business alignment of datacenter IT services by:

-   Automating processes and enforcing best practices for incident, change, and service-life-cycle management.

-   Reducing unanticipated errors and service delivery time by automating tasks across responsibility groups within your IT organization.

-   Integrating System Center with non-Microsoft tools to enable interoperability across the datacenter.

-   Orchestrating tasks across systems for consistent, documented, and compliant activity.


## How to Create a Runbook Automation Activity Template

After you import runbooks into Service Manager using the Orchestrator connector from Orchestrator, you can create a runbook automation activity template to map parameters in Orchestrator to corresponding parameters in Service Manager.

As an example, you can implement a new request offering using an Orchestrator runbook to automate it. Then, you can go to the Runbooks view in the Library workspace, select a runbook, and create a runbook automation activity template. You can go to the templates view and verify that the template is created. You can then add the Orchestrator activity template to a service request template and create the request offering. You then can then map the runbook template to a different runbook with the same inputs and outputs if you find that you need to fix a problem or improve the process.

> [!IMPORTANT]
> If you have extended root classes such as service request or release record, then you can map runbook activity parameter to extended properties only if the runbook activity template and service request templates are saved in same management pack where the definition extension is located.

### To create a runbook automation activity template

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, click **Runbooks**.

3.  In the **Runbooks** view, select a runbook.

4.  In the **Tasks** pane, under **<RunbookName\>**, click **Create Runbook Automation Activity Template** to open the **Create Template** dialog box.

5.  In the **Name** box, type a name for the template.

6.  Optionally, in the **Description** box, type a description for the template.

7.  If necessary, select an unsealed management pack to save the template to, and then click **OK**. You will use this management pack later to retrieve the runbook automation activity template from another work item template, such as a service request template.

8.  In the Runbook Activity Template: <TemplateName\> form, on the **General** tab, type information for **Title**, **Description**, **Area**, **Stage**, **Assigned To**, and **Designer**.

9. Ensure that **Is Ready for Automation** is selected.

10. Select the **Runbook** tab, and then under **Parameter Mapping**, note that the parameters from the runbook are mapped to generic properties. For example, Parameter1, Parameter2, and so on of the runbook activity class. The **Type** column specifies whether the parameters are inputs or outputs. You can also type default values for each parameter using **Edit Mapping**.

11. For any parameter, click **Edit Mapping**.

12. Expand **Object**, and then click **Id**. This ID value will be used by the Orchestrator runbook to find the particular runbook activity that is being executed. Click **Close**.

13. Click **OK** to close the form and create the template.



## How to View a Runbook
After you import runbooks from Orchestrator into Service Manager, you can open the runbook in the Service Manager console to ensure that it contains the parameters you want to use in an automation activity template in Service Manager.

When you view the runbook, you can perform basic actions with the runbook, such as viewing the summary, jobs, instances, and definition of the runbook. You can also start and stop the runbook.

### To view a runbook

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, select **Runbooks**.

3.  In the **Runbooks** view, select a runbook.

4.  In the **Tasks** pane under **<RunbookName\>**, click **View Runbooks** to open the runbook in Internet Explorer.



