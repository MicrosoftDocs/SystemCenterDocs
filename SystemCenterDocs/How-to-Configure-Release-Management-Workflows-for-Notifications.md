---
title: How to Configure Release Management Workflows for Notifications
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c44fdc5f-4eca-4464-9c6a-94ed45aeeace
robots: noindex,nofollow
---
# How to Configure Release Management Workflows for Notifications
You can configure notifications for release records in [!INCLUDE[smlong12](Token/smlong12_md.md)] by completing the following procedures. The following procedure sends a notification when a release record is created or updated.

### To configure a notification for updated release records

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Workflows**, and then click **Configuration**.

3.  In the **Configuration** pane, double\-click **Release Record Event Workflow Configuration**.

4.  In the **Configure Workflows** dialog box, click **Add**.

5.  In the **Configure workflows for objects of class Release Record** dialog box, complete these steps:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **Workflow Information** page, in the **Name** box, type a name for the workflow. For example, type **Updated Release Records**.

    3.  In the **Description** box, type a description of what the workflow does. For example, type **This workflow notifies the assigned\-to user and the created\-by user when release records are updated.**

    4.  In the **Check for events** list, select **When an object is created** or select **When an object is updated**, ensure that the **Enabled** check box is selected, and then click **Next**.

    5.  On the **Specify Event Criteria** page, click the **Changed to** tab. Under **Related classes**, expand **Release Record**, and then select either **Assigned To User** or **Created By User**.

    6.  Under **Available properties**, select **User Name**, click **Add**, and then under **Criteria**, type the user name of the person that you are basing the notification on. Repeat this step, as necessary.

    7.  On the **Apply Template** page, clear **Apply the selected template**, and then click **Next**.

    8.  On the **Select People to Notify** page, select **Enable notification**, then select **Assigned To User** and then click **Add**. Repeat this step for **Created By User**, and then click **Next**.

    9. On the **Summary** page, review your settings, and then click **Create**.

    10. On the **Completion** page, click **Close**.


