---
title: How to Configure Desired Configuration Management to Generate Incidents
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12a749b4-29e4-4fcf-96ae-0a212de67ae2
robots: noindex,nofollow
---
# How to Configure Desired Configuration Management to Generate Incidents
In [!INCLUDE[smlong12](Token/smlong12_md.md)], you can import configuration baselines from System Center Configuration Manager 2007 by using a Configuration Manager connector. Then, you can configure [!INCLUDE[smshort](Token/smshort_md.md)] to create incidents for each [!INCLUDE[smshort](Token/smshort_md.md)] configuration item that is reported as noncompliant against the defined values.

You can use the following procedures to configure incident management to automatically generate desired configuration management–based incidents and validate that the desired configuration management is configured.

### To configure incident management to automatically generate desired configuration management–based incidents

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Workflows**, and then click **Configuration**.

3.  In the **Configuration** pane, double\-click **Desired Configuration Management Event Workflow Configuration**.

4.  In the **Configure Desired Configuration Management Workflows** dialog box, click **Add**.

5.  In the Add Desired Configuration Management Workflow Wizard, complete these steps:

    1.  On the **Before You Begin** page, click **Next**.

        > [!NOTE]
        > The **Next** button will be unavailable if a Configuration Manager connector has not been created.

    2.  On the **Workflow Information** page, type a name and a description for the rule. Make sure that the **Enabled** check box is selected, and then click **Next**.

    3.  On the **Select System Center Configuration Manager Configuration Items** page, expand all the configuration baselines that are listed, select the Configuration Manager 2007 configuration items that you want to include in the rule, and then click **Next**.

    4.  On the **Select Incident Template** page, click **Apply the following template**, select a template for the new incidents that will be created by this rule, and then click **Next**.

    5.  On the **Select People to Notify** page, select the **Enable notification** check box. Select the users who should be notified when an incident is created by this rule. For each user, specify the notification method and a template, and then click **Add**. Click **Next**.

    6.  On the **Summary** page, make sure that the settings contain the information you expect, and then click **Create**.

    7.  On the **Completion** page, make sure that you receive the following confirmation message, and then click **Close**:

        “Desired Configuration Management Workflow Created Successfully”

### To validate that desired configuration management is configured

1.  Import an out\-of\-compliance [!INCLUDE[smshort](Token/smshort_md.md)] configuration item that would match one of the desired configuration management rules. Then, locate the desired configuration management–based incident in [!INCLUDE[smshort](Token/smshort_md.md)].

2.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Work Items**

3.  In the **Work Items** pane, expand **Incident Management**, and then click **All Open DCM Incidents**.

4.  In the **All Open Desired Configuration Management Incidents** pane, double\-click an incident.

5.  In the **Incident** form, click the **Compliance Errors** tab.

6.  Verify that the correct configuration baseline and Configuration Manager 2007 configuration items are listed.

![](Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to create a desired configuration management workflow in [!INCLUDE[smshort](Token/smshort_md.md)], see [New\-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225354).

-   For information about how to use Windows PowerShell to retrieve the list of all DCM workflows that are defined in [!INCLUDE[smshort](Token/smshort_md.md)], see [Get\-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225321).

-   For information about how to use Windows PowerShell to update properties of a desired configuration management workflow, see [Update\-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225383).

-   For information about how to use Windows PowerShell to remove a desired configuration management workflow from [!INCLUDE[smshort](Token/smshort_md.md)], see [Remove\-SCSMDCMWorkflow](http://go.microsoft.com/fwlink/p/?LinkID=225365).


