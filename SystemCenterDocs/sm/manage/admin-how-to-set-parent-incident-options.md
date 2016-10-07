---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Set Parent Incident Options
ms.technology:  service-manager
ms.assetid:  220b9d62-cd3a-4e30-a465-cdd70ca736bc
---

# How to Set Parent Incident Options

>Applies To: System Center 2016 - Service Manager

Use the following procedure to set default options for parent and child incidents in Service Manager. The default options determine whether child incidents automatically resolve, whether child incidents automatically activate, and whether child incident status automatically updates.

When choosing to automatically resolve child incidents or automatically reactivate child incidents when its parent is resolved or when its parent is reactivated, you can prompt the resolving analyst for their decision. When prompted, an analyst can choose a resolution category or activation status. Otherwise, when incidents are automatically resolved or activated, the analyst is not prompted and the changes are effectively immediately using the parent incident settings.

### To automatically resolve child incidents

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Incident Settings**.

4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.

5.  In the **Incident Settings** dialog box, click **Parent Incident** and then choose one of the following actions:

    -   If you want to automatically resolve a child incident when its parent is resolved without any analyst interaction, set **Auto resolution of child incidents** to **Automatically resolve child incidents when parent incident is resolved**, and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.

    -   If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident resolution category, select **Auto resolution of child incidents** to **Let the analyst decide when resolve the parent incident** and then choose either **Same as parent incident category** or **Choose a child incident category** and a default resolution category.

    -   If you do not want child incidents to automatically resolve, select **Auto resolution of child incidents** to **Do not resolve child incidents when parent incident is resolved**.

6.  Click **OK**.

### To automatically activate child incidents

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Incident Settings**.

4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.

5.  In the **Incident Settings** dialog box, click **Parent Incident**, and then choose one of the following actions:

    -   If you want to automatically activate a child incident when its parent is activated without any analyst interaction, set **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.

    -   If you want to automatically resolve a child incident when its parent is resolved and have an analyst review and verify the incident reactivation status, select **Auto reactivation of child incidents** to **Automatically reactivate child incidents when parent incident is reactivated**, and then choose a default reactivation status.

    -   If you do not want to automatically activate child incidents, set **Auto reactivation of child incidents** to **Do not reactivate child incidents when parent incident is reactivated**.

6.  Click **OK**.

### To automatically update child incident status

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Incident Settings**.

4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.

5.  In the **Incident Settings** dialog box, click **Parent Incident**, and then choose one of the following actions:

    -   If you want to automatically update child incident status when it is linked to a parent incident, set **Status of active child incidents when linked to parent** to **Automatically change the status of active child incidents when linking to parent**, and then choose an available incident status.

    -   If you do not want to automatically update child incident status, set **Status of active child incidents when linked to parent** to **Do not change the status of child incidents**.

6.  Click **OK**.
