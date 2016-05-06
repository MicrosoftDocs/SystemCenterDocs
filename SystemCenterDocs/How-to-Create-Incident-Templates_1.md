---
title: How to Create Incident Templates_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55515ea2-65c2-4cba-ab13-a34f8208c0d8
robots: noindex,nofollow
---
# How to Create Incident Templates_1
Use the following procedures to create two incident templates in [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)]. The first you use to create email\-related incidents, and the second you use with the Incident Change workflow for printer\-related problems.

### To create an email\-related incident template

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Templates**.

3.  In the **Tasks** pane, in the **Templates** area, click **Create Template**.

4.  In the **Create Template** dialog box, complete these steps:

    1.  In the **Name** box, type a name for the incident template. For example, type **E\-mail Incident**.

    2.  In the **Description** box, type a description for the incident template. For example, type **Use this template to start all email\-related incidents**.

    3.  Click **Browse** to choose a class.

    4.  In the **Choose Class** dialog box, click **Incident**, and then click **OK**.

    5.  In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and then click **OK**.

5.  In the incident template form, complete these steps:

    1.  Leave the **Affected user** box empty.

    2.  Leave the **Alternate contact information** box empty. Alternate contact information for the affected user is entered when the incident is created.

    3.  In the **Title** box, type a title for the template. Or, type a preface, such as **Email:**.

    4.  In the **Classification Category** box, select the category that reflects the problem to report. For example, select **E\-mail Problems**.

    5.  Leave the **Source** box empty. The **Source** box is automatically populated when the incident is created.

    6.  In the **Impact** box, select a value. For example, select **High**.

        In the **Urgency** box, select a value. For example, select **High**.

    7.  In the **Support Group** box, select a tier. For example, if you want all email\-related issues to be assigned to the tier 2 support group, select **Tier 2**.

    8.  Click **OK**.

### To create a new printer\-related incident template

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Templates**.

3.  In the **Tasks** pane, click **Create Template**.

4.  In the **Create Template** dialog box, complete these steps:

    1.  In the **Name** box, type a name for the incident template. For example, type **Escalate Printer Problems to Tier 2**.

    2.  In the **Description** box, type a description for the incident template. For example, type **Use this template to assign high\-urgency printer\-related problems to tier 2**.

    3.  Click **Browse** to choose a class.

    4.  In the **Choose Class** dialog box, click **Incident**, and then click **OK**.

    5.  In the **Management Pack** list, select **Service Manager Incident Management Configuration Library**, and then click **OK**.

5.  In the incident template form, follow these steps:

    1.  In the **Support Group** box, select a tier. For example, if you want all printer\-related issues to be assigned to the tier 2 support group, select **Tier 2**.

    2.  Click **OK**.

    3.  Press F5 to refresh the **Templates** pane.

### To validate that the new incident template was created

-   Verify that the new incident templates are listed in the **Templates** pane.


