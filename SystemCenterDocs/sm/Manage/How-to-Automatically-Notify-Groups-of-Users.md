---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Automatically Notify Groups of Users
ms.technology:  service-manager
ms.assetid:  df903459-18ba-40e7-8896-ad71e4d1a7af
---

# How to Automatically Notify Groups of Users

>Applies To: System Center 2016 Technical Preview - Service Manager

In some scenarios, you may want to use a group rather than an individual user in Service Manager as a work item stakeholder. For example, you might want to assign an incident to a team of people, such as an initial response team that routes incidents, and then notify everyone in the initial response team that an incident has been assigned to their team.

Messaging-enabled universal security groups in Microsoft Exchange Server are the key to this task. This topic describes how to accomplish this using the Exchange Server Exchange Management console for incidents. You can use the following procedures to create a messaging-enabled universal security group, create a workflow to notify stakeholders when an incident is created, and then test for success.

In Exchange Server, the **Require that all senders are authenticated** setting is enabled by default for mail-enabled universal security groups. You can modify the setting in the distribution group properties, in Mail-Flow settings, in the **Message Delivery Restrictions** dialog box. If your outgoing Simple Mail Transfer Protocol (SMTP) server specified in the Service Manager settings (Under **Administration**>**Notifications Channels**>**Edit**) is using Anonymous as the Authentication Method (either in  Service Manager or the SMTP settings), then given the above default setting in exchange, the email would not be sent out. If you have Anonymous Access configured on the SMTP side, it is necessary either to clear the **Require that all senders are authenticated** setting in exchange for the Mail Enabled Universal Security Group, or change the SMTP authentication settings (in Service Manager or the outgoing SMTP Server settings) from anonymous to Windows Integrated, so that the user is authenticated, allowing the email to be sent.

As an alternative, you can avoid using **Assigned to** and instead use **Support Group** changing as a triggering field. To set this up, create a new email notification subscription, and under additional criteria, use the following:

-   Changed from: [incident] Support Group Does not equal Tier 1

-   Changed to: [incident] Support Group equals Tier 1

Use whatever template you want, and add the recipient of the mailing distribution list for Tier 1. Now Tier 1 is notified whenever a ticket is set to them, even if it is done by means of a template at portal ticket creation.

Setting up one of these for each support group will ensure that all your groups are informed of incoming incidents that require their attention.

### To create a messaging-enabled universal security group

1.  In the Exchange Management Console, navigate to **Recipient Configuration**, right-click **Distribution Group**, and then click **New Distribution Group**.

2.  On the **Introduction** page, either choose an existing universal group or create a new group.

3.  On the **Group Information** page, select the **Security** group type.

4.  Complete the creation of the group.

5.  Add members to the group by right-clicking them, clicking **Properties**, and accessing the **Members** tab.

6.  Wait for Service Manager to sync with Active Directory Domain Services (AD DS), or perform a manual Synchronization from **Administration**>**Connectors**. (Click **AD Connector**, and then click the **Synchronize Now** task on the right-hand side).

7.  Once the Active Directory synchronization has completed, the newly created group will be available as a configuration item in Service Manager, and it can be selected in the user picker fields, such as **Affected User** and **Assigned To**.

### To create a workflow to notify stakeholders when an incident is created

1.  Navigate to **Administration**>**Workflows**>**Configuration**.

2.  Double-click **Incident Event Workflow Configuration**.

3.  Click **Add**, and then click **Next** on the **Before you Begin** page.

4.  Give the workflow a name, such as *Incident Created Email Stakeholders*.

5.  Leave the default of **When an incident is created** in the **Check for Events** drop-down list.

6.  Select one of your custom management packs (or create one) to store the workflow in, and then click **Next**.

7.  Click **Next** on the **Specify Incident Criteria** page. (We want this workflow to run when any new incident is created.)

8.  Optionally, apply a template. (In this case we are creating the workflow for notification only, so we choose **Do not apply a template**.)

9. In the **Select People to Notify** dialog box, select the **Enable notification** check box. Add the appropriate users you want to notify with the appropriate templates.

10. Click Next, and then click **Create** to complete creation of the workflow.

### To test the workflow and mail the enabled universal security group

- Create an incident and assign it to the messaging-enabled universal security group that you created earlier.
