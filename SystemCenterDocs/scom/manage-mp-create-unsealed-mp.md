---
ms.assetid: 102761c5-25f3-4fd4-8e5b-a68ea622e921
title: How to Create a Management Pack for Overrides
description: This article describes how to create a writeable management pack to save overrides to in Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 08/04/2020
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# How to create a management pack for overrides



In System Center - Operations Manager, in a number of wizards and dialog boxes, you select a destination management pack in which to store the settings. You can select any unsealed management pack file in your management group or create a new one.  

Management packs can be sealed or unsealed. A sealed management pack can't be modified directly. Any changes to the workflows in the sealed management pack, such as an override for a monitor, must be saved to an unsealed management pack. The unsealed management pack references the sealed management pack that it modifies.  

::: moniker range="sc-om-2019"
>[!NOTE]
> With Operations Manager 2019 UR2, you can track the changes done in management packs. [Learn more](management-pack-change-tracking.md).

::: moniker-end

::: moniker range="sc-om-2022"
>[!NOTE]
> You can track the changes done in management packs. [Learn more](management-pack-change-tracking.md).

::: moniker-end

The following illustration shows the unsealed management packs that are installed with Operations Manager.  

![Illustration of the Dropdown menu for selecting management pack.](./media/manage-mp-create-unsealed-mp/om2016-save-override-to-mp.png)  

Never use the management packs that are installed with Operations Manager to save any settings that you change or elements that you create. When you've to select a destination management pack, always select a management pack that you create.  

You select a destination management pack when you create an override or disable a rule, monitor, or object discovery. You also select a destination management pack when you create or configure the following elements:  

-   A folder in the **Monitoring** workspace  

-   A unit, aggregate, or dependency monitor  

-   An attribute  

-   A group  

-   A rule  

-   A task  

-   A Run As profile  

-   Monitoring by using a management pack template  

-   Monitoring of a distributed application  

-   Tracking of service level objectives  

## Saving overrides  

As a best practice, save all overrides for each sealed management pack to an unsealed management pack that is named *ManagementPack*\_Override, where *ManagementPack* is the name of the sealed management pack to which the overrides apply. For example, overrides to the management pack Microsoft.SQLServer.2012.Monitoring.mp would be saved to Microsoft.SQLServer.2012.Monitoring\_Overrides.xml.  

When you want to remove a sealed management pack, you must first remove any other management packs that reference it. If the unsealed management packs that reference the sealed management pack also contain overrides or elements that apply to a different sealed management pack, you lose those overrides and elements when you remove the unsealed management pack.  

In the following image, overrides for management packs 1, 2, and 3 are all saved to a single unsealed management pack. If you want to remove management pack 1, you must first remove the unsealed management pack. As you can see, you would also remove all overrides for management packs 2 and 3.  

![Diagram showing Overrides saved to single management pack.](./media/manage-mp-create-unsealed-mp/om2016-mp-reference-example.png)  

The recommended method is to create an unsealed management pack for each sealed management pack that you want to override, as shown in the following image. Removing management pack 1 and its unsealed management pack doesn't affect the other management packs.  

![Diagram showing Save overrides to respective management packs.](./media/manage-mp-create-unsealed-mp/om2016-mp-reference-best-practice.png)  

## How to create a management pack for overrides  
You can create a management pack for overrides before you configure an override or as part of the override procedure.  

### To create a management pack  

-   In the **Administration** workspace, in the navigation pane, right\-click, and select **Create Management Pack**.  

    \-or\-  

-   In the **Override Properties** dialog for a rule or monitor, in the **Select destination management pack** section, select **New**.  

## Next steps

- To understand what an Operations Manager management pack is and how it helps you proactively monitor your services and applications, see [What Is in an Operations Manager Management Pack?](manage-overview-management-pack.md).

- To perform common administrative tasks with management packs in your management group, see [How to Import, Export, and Remove an Operations Manager Management Pack](manage-mp-import-remove-delete.md).

- If you want to create your own custom knowledge for specific alerts generated by rules or monitors from a sealed management pack, review [How to Add Knowledge to a Management Pack](manage-mp-add-knowledge.md).
