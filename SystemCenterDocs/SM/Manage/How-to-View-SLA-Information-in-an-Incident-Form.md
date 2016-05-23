---
title: How to View SLA Information in an Incident Form
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2014c9a-bb98-445e-b5fa-194cbb3d4634
---
# How to View SLA Information in an Incident Form
As you are working with incidents, it is easy to tell when an incident’s service level is about to or has been breached by viewing incidents in the **Assigned To Me** view and then looking for information in the **Service Level Target** column.

If you are already in an incident form and an incident is about to breach, a notification bar is displayed in the form while on the **General** tab stating that **One or more Service Level Objectives are about to breach.** You can view additional information about the service level status on the corresponding tab and see that the status shown is a warning.

When an incident has already been breached, no notification bar is displayed in the form while you are on the **General** tab. However, you will see breached status while you are on the **Service Level** tab if that incident’s service level objective has breached.

### To view warning SLA information in an incident form

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Work Items**.

2.  In the **Work Items** pane, expand **Incident Management**, and then click **Incidents with Service Level Warning**.

3.  In the **Incidents with Service Level Warning** list, select an incident, and then in the **Tasks** pane, under **\<IncidentID\-IncidentName\>**, click **Edit**.

4.  In the **\<Incident IncidentID\-IncidentName – Status\>** form, observe the **One or more Service Level Objectives are about to breach** warning.

5.  Click the **Service Level** tab, and observe the status of the incident as **Warning**. You can also see other information about the incident, most notably **Time Before SLA Breached**.

6.  Click **OK** to close the incident.

### To view breached SLA information in an incident form

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], click **Work Items**.

2.  In the **Work Items** pane, expand **Incident Management**, and then click **Incidents with Service Level Breached**.

3.  In the **Incidents with Service Level Breached** list, select an incident, and then in the **Tasks** pane, under **\<IncidentID\-IncidentName\>**, click **Edit**.

4.  Click the **Service Level** tab, and observe the status of the incident as **Breached**.

5.  Click **OK** to close the incident.


