---
ms.assetid: 
title: Patch Azure Monitor SCOM Managed Instance (preview)
description: This article provides information on how to patch your Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 02/13/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Patch Azure Monitor SCOM Managed Instance (preview)

Azure Monitor SCOM Managed Instance (preview) offers a convenient patching experience compared to on-premises System Center Operations Manager. 

Below are the key highlights:

- No update rollup in SCOM Managed Instance (preview). A patch will be released as and when there are significant fixes and updates made to the product. They'll be released at a frequency of as often as two weeks or two months.
- Patching is quick and convenient and happens at the click of a button.
- All newer patches are backward compatible with the older versions. 

This article provides information on how to patch your SCOM Managed Instance (preview).

## Patch SCOM Managed Instance (preview)

To patch SCOM Managed Instance (preview), follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/) and search for **SCOM Managed Instance**.
1. On the **Overview** page, under **Configuration**, select **Patching**.
1. On the **Patching** page, you'll see the status of the updates available for your instance.

     :::image type="Patching" source="media/patch-scom-managed-instance/scom-mi-patching.png" alt-text="Screenshot of Patching.":::

1. Select **Update instance** to update your instance.

     :::image type="Update Instance" source="media/patch-scom-managed-instance/update-instance.png" alt-text="Screenshot of Update Instance.":::
 
It takes 30 mins to 1 hour to successfully update the instance.

 :::image type="Instance updated" source="media/patch-scom-managed-instance/instance-updated.png" alt-text="Screenshot of Instance updated.":::

## Next steps

[Connect the Azure Monitor SCOM Managed Instance (preview) to Ops console](connect-managed-instance-ops-console.md)

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
