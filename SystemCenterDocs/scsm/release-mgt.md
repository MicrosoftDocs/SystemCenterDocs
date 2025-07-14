---
title: Configure Release Management settings
description: Learn about how to configure Release Management settings in Service Manager.
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: 29504a71-5574-472c-b930-894d31fe2267
ms.custom: UpdateFrequency3, engagement-fy24
---

# Configure Release Management settings



As part of your initial configuration of Service Manager, you've to configure settings and workflows for release management. The settings define the ID prefix that is assigned to release records, how many files can be attached to each release record, and the maximum size of each file. You also create a workflow to notify people when a release record affects them.

## Configure settings

The Service Manager Administrator configures release management settings by using the following procedure.

> [!NOTE]
> Revising the release record prefix doesn't affect the existing release records.

### Configure release management settings

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Settings**.

3. In the **Settings** view, select **Release Management Settings**.

4. In the **Tasks** pane, in the **Release Management Settings** area, select **Properties**.

5. In the **Release Management Settings** dialog, you can make the following changes:

    1. If you want to change the prefix code, change the default value in the **Release Record ID prefix** box.

    2. If you want to change the maximum number of files that you can attach to a release record, change the default value in the **Maximum number of attached files** box. For example, enter **2**.

    3. If you want to change the maximum size of files that you attach to a release record, change the default value in the **Maximum size (KB)** box. For example, enter **300**.

6. Select **OK** to close the **Release Management Settings** dialog.

## Configure notifications

You can configure notifications for release records by completing the following procedure that sends a notification when a release record is created or updated.

### Configure a notification for updated release records

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, expand **Workflows**, and select **Configuration**.

3. In the **Configuration** pane, double-click **Release Record Event Workflow Configuration**.

4. In the **Configure Workflows** dialog, select **Add**.

5. In the **Configure workflows for objects of class Release Record** dialog, complete these steps:

    1. On the **Before You Begin** page, select **Next**.

    2. On the **Workflow Information** page, in the **Name** box, enter a name for the workflow. For example, enter **Updated Release Records**.

    3. In the **Description** box, enter a description of what the workflow does. For example, enter **This workflow notifies the assigned-to user and the created-by user when release records are updated.**

    4. In the **Check for events** list, select **When an object is created** or select **When an object is updated**, ensure that the **Enabled** checkbox is selected, and select **Next**.

    5. On the **Specify Event Criteria** page, select the **Changed to** tab. Under **Related classes**, expand **Release Record**, and then select either **Assigned To User** or **Created By User**.

    6. Under **Available properties**, select **User Name**, select **Add**, and then under **Criteria**, enter the user name of the person that you're basing the notification on. Repeat this step, as necessary.

    7. On the **Apply Template** page, clear **Apply the selected template**, and select **Next**.

    8. On the **Select People to Notify** page, select **Enable notification**, then select **Assigned To User** and select **Add**. Repeat this step for **Created By User**, and select **Next**.

    9. On the **Summary** page, review your settings, and select **Create**.

    10. On the **Completion** page, select **Close**.

## Next steps

- [Configure Desired Configuration Management to generate incidents](dcm-incidents.md).
