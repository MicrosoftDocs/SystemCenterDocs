---
title: Building a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17d8d1d1-2326-4925-84a0-c83e82cf7806
---
# Building a Runbook
This topic describes the basic process for building a [!INCLUDE[orchlong](../Token/orchlong_md.md)] runbook.

> [!NOTE]
> For a list of topics that contain more details about the information covered here, see [Runbook data processing](../Topic/Building-a-Runbook.md#BMK_Runbookdataprocessing).

|Step|Description|
|--------|---------------|
|1. Create a runbook.|Create an empty runbook in the Runbook Designer.|
|2. Add activities.|Click and drag activities from the **Activities** pane into the runbook. Include a start point and an end point for the runbook.|
|3. Link activities.|Create and configure smart links between each of the activities to create a complete workflow.|
|4. Configure runbook properties.|Configure the properties for the runbook.|
|5. Check in the runbook.|Save your changes and check in the runbook.|

#### To create a new runbook

1.  On the computer where the Runbook Designer is installed, click **Start**, point to **All Programs**, click **[!INCLUDE[orchlong](../Token/orchlong_md.md)]**, and then click **Runbook Designer**.

2.  In Runbook Designer, in the **Connections** pane, click the **Runbooks** folder.

3.  In the **Connections** pane, click the **Create a new runbook** icon.

4.  In the **Runbook Designer** Design workspace, right\-click the **Runbook** tab, and then select **Rename**.

5.  In the **Confirm Check out** dialog box, click **Yes**.

6.  Enter a name for the runbook, such as **Sample Runbook**, and press Enter.

#### To add and configure activities to your runbook

1.  In the **Activities** pane, drag an activity to the Design workspace of your runbook.

2.  In the **Activities** pane, double\-click an activity to open the **Properties** dialog box for that activity.

    > [!NOTE]
    > For information about specific properties of standard activities, see the [Runbook Activity Reference for System Center 2012 - Orchestrator](../Topic/Runbook-Activity-Reference-for-System-Center-2012---Orchestrator.md).

#### To add and configure links in a runbook

1.  To create a link, click and drag the arrow of an activity to another activity.

2.  On the newly created link, double\-click the link to open the **Link Properties** dialog box.

    > [!NOTE]
    > For information about the properties of links, see the [Runbook Activity Reference for System Center 2012 - Orchestrator](../Topic/Runbook-Activity-Reference-for-System-Center-2012---Orchestrator.md).

#### To define the properties of a runbook

1.  Right\-click the **Runbook** tab to select **Properties**. The **Runbook Properties** dialog box opens.

2.  Configure the settings on the **General** tab. The following tables provide the configuration instructions.

3.  Click **Finish** to save your settings.

#### To check in your runbook

-   In Runbook Designer, click the **Check In** icon on the toolbar.

## <a name="BMK_Runbookdataprocessing"></a>Runbook data processing

-   [Data Manipulation](../Topic/Data-Manipulation.md)

-   [Published Data](../Topic/Published-Data.md)

## Other resources for this product

-   TechNet Library main page for [Orchestrator_1](../Topic/Orchestrator_1.md)

-   [Using Runbooks in System Center 2012 - Orchestrator](../Topic/Using-Runbooks-in-System-Center-2012---Orchestrator.md)

-   [Designing a Runbook](../Topic/Designing-a-Runbook.md)

-   [How to Test a Runbook](../Topic/How-to-Test-a-Runbook.md)

