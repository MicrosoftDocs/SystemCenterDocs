---
ms.assetid: 
title: Scale Azure Monitor SCOM Managed Instance (preview)
description: This article provides information on how to scale your Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/29/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Scale Azure Monitor SCOM Managed Instance (preview)

Addition or deletion of a management server to the existing SCOM Infrastructure automatically links or delinks it from the existing Operational database, Data warehouse, and endpoints in SCOM Managed Instance (preview).

This article provides information on how to scale your SCOM Managed Instance (preview).

## Scale In/Out the management servers

To scale In/Out the management servers, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com/) and search for **SCOM** or **SCOM Managed Instance**.
1. On the **Overview** page, under **Configuration**, select **Scaling**.
     :::image type="Scaling" source="media/scale-scom-managed-instance/scaling.png" alt-text="Screenshot of Scaling.":::
1. On the **Scaling** page,
    1. **Current**: Displays the existing number of management servers that are a part of the SCOM Managed Instance (preview).
    1. **Scale In/Out management servers**:
        1. **Total Endpoints to be monitored**: Enter the total number of endpoints you would like to monitor using a specific SCOM Managed Instance (preview).
        1. **Recommended Management servers**: Depending on the number of endpoints you enter, the ideal number of management servers to be provisioned will be recommended. You can change the recommended value as desired.

           >[!Note]
           >A Management server can monitor upto 1000 endpoints. 

           :::image type="Scaling SCOM Managed Instance (preview)" source="media/scale-scom-managed-instance/scaling-scom-mi.png" alt-text="Screenshot of Scaling SCOM Managed Instance (preview).":::
 
1. Select **Save** to trigger the Scale In or Scale Out operation. 

## Next steps

[Patch SCOM managed instance (preview)](patch-scom-managed-instance.md)