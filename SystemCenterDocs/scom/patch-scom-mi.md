---
ms.assetid: 
title: Patch Azure Monitor SCOM Managed Instance (preview)
description: This article provides information on how to patch your Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/24/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Patch Azure Monitor SCOM Managed Instance (preview)

Azure Monitor SCOM Managed Instance (preview) offers a convenient patching experience compared to on-premesis SCOM. 

Below are the key differences:

- No concept of update roll up in SCOM Managed Instance (preview). A patch will be released as and when there are significant fixes and updates made to the product. They will be released at a cadence of as often as 2 weeks or 2 months.
- Patching is quick and convenient. Select the button and wait for the patch to complete.
- All newer patches are backward compatible with older versions. 

This article provides information on how to patch your SCOM Managed Instance (preview).

## Patch SCOM Managed Instance (preview)

To patch SCOM Managed Instance (preview), follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/) and search for **SCOM** or **SCOM Managed Instance**.
1. On the **Overview** page, under **Configuration**, select **Patching**.
1. On the **Patching** page, you will see the status of available updates for your instance.

     :::image type="Patching" source="media/patch-scom-mi/scom-mi-patching.png" alt-text="Screenshot of Patching.":::

1. Select **Update instance** to update your instance.

     :::image type="Update Instance" source="media/patch-scom-mi/update-instance.png" alt-text="Screenshot of Update Instance.":::
 
It takes 30 mins to 1 hour to successfully update the instance.

     :::image type="Instance updated" source="media/patch-scom-mi/instance-updated.png" alt-text="Screenshot of Instance updated.":::

## Next steps

> [!div class="nextstepaction"]
> [Connect the Azure Monitor SCOM managed instance (preview) to Ops console](connect-managed-instance-ops-console.md)