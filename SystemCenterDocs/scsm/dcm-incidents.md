---
title:  Configure Desired Configuration Management to generate incidents
description: Learn about how to configure Desired Configuration Management to generate incidents in Service Manager.
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  27337337-38a7-476f-974a-6ffa16027bf1
---

# Configure Desired Configuration Management to generate incidents in Service Manager

>Applies To: System Center 2016 - Service Manager

You can use the following procedure, for example, to inventory all the computers that might require an upgrade to Microsoft Exchange Server 2016. To do this, first define the appropriate configuration baseline in System Center Configuration Manager.

In Service Manager, you must create a Configuration Manager connector to import the baseline and configure incident management to automatically generate incidents based on desired configuration management. For information about how to create a Configuration Manager connector, see [About Importing Data from System Center Configuration Manager](../sm/manage/admin-about-importing-data-from-system-center-configuration-manager.md).

You can use desired configuration management in Configuration Manager to monitor software to ensure that it is compliant with defined values. For example, you can monitor software versions, security settings, and software updates. The configurations that you want to monitor are added as Configuration Manager configuration items to configuration baselines so that they can be evaluated for compliance as a group.

In Service Manager, you can import configuration baselines from Configuration Manager  by using a Configuration Manager Connector. You can then configure Service Manager to create incidents for each Service Manager configuration item that reports as noncompliant against the defined values.

Use the following procedure to configure incident management to automatically generate incidents based on desired configuration management.

In Service Manager, you can import configuration baselines from System Center Configuration Manager by using a Configuration Manager connector. Then, you can configure Service Manager to create incidents for each Service Manager configuration item that is reported as noncompliant against the defined values.

You can use the following procedures to configure incident management to automatically generate desired configuration management-based incidents and validate that the desired configuration management is configured.

## To configure incident management to automatically generate desired configuration management-based incidents

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.

3.  In the **Configuration** pane, double-click **Desired Configuration Management Event Workflow Configuration**.

4.  In the **Configure Desired Configuration Management Workflows** dialog box, click **Add**.

5.  In the Add Desired Configuration Management Workflow Wizard, complete these steps:

    1.  On the **Before You Begin** page, click **Next**.

        > [!NOTE]
        > The **Next** button will be unavailable if a Configuration Manager connector has not been created.

    2.  On the **Workflow Information** page, type a name and a description for the rule. Make sure that the **Enabled** check box is selected, and then click **Next**.

    3.  On the **Select System Center Configuration Manager Configuration Items** page, expand all the configuration baselines that are listed, select the Configuration Manager configuration items that you want to include in the rule, and then click **Next**.

    4.  On the **Select Incident Template** page, click **Apply the following template**, select a template for the new incidents that will be created by this rule, and then click **Next**.

    5.  On the **Select People to Notify** page, select the **Enable notification** check box. Select the users who should be notified when an incident is created by this rule. For each user, specify the notification method and a template, and then click **Add**. Click **Next**.

    6.  On the **Summary** page, make sure that the settings contain the information you expect, and then click **Create**.

    7.  On the **Completion** page, make sure that you receive the following confirmation message, and then click **Close**:

        `Desired Configuration Management Workflow Created Successfully`

### To validate that desired configuration management is configured

1.  Import an out-of-compliance Service Manager configuration item that would match one of the desired configuration management rules. Then, locate the desired configuration management-based incident in Service Manager.

2.  In the Service Manager console, click **Work Items**

3.  In the **Work Items** pane, expand **Incident Management**, and then click **All Open DCM Incidents**.

4.  In the **All Open Desired Configuration Management Incidents** pane, double-click an incident.

5.  In the **Incident** form, click the **Compliance Errors** tab.

6.  Verify that the correct configuration baseline and Configuration Manager configuration items are listed.

![PowerShell symbol](./media/dcm-incidents/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a desired configuration management workflow in Service Manager, see [New-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225354).

-   For information about how to use Windows PowerShell to retrieve the list of all DCM workflows that are defined in Service Manager, see [Get-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225321).

-   For information about how to use Windows PowerShell to update properties of a desired configuration management workflow, see [Update-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225383).

-   For information about how to use Windows PowerShell to remove a desired configuration management workflow from Service Manager, see [Remove-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225365).
