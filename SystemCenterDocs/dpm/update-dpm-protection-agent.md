---
description: This article describes how to update protection agents for both connected and disconnected client computers.
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.service: system-center
ms.date: 04/22/2025
title: Update the DPM Protection Agent
ms.subservice: data-protection-manager
ms.assetid: 
ms.custom: na
---

# Update the DPM protection agent

If you want to upgrade a protection agent installed on a computer that isn't connected to the network, you can't perform a connected agent upgrade from within DPM Administrator Console. You must perform the upgrade in an inactive domain environment. The DPM server shows that the protection agent update is pending until the client computer is connected to the network.

This article describes how to update protection agents for both connected and disconnected client computers.

## Update a protection agent for a connected client computer

To update a protection agent for a connected client computer, follow these steps:

1. In the DPM Administrator Console, select **Management** and then select the **Agents** tab.

2. Select the client computers on which you want to update the protection agent.

     >[!NOTE]
     >The **Agent Updates** column indicates the protection agent updates available for each protected computer. The **Update** action in the **Actions** pane isn't enabled when a protected computer is selected unless updates are available.

3. To install updated protection agents on selected computers, select **Update** in the **Actions** pane.

## Update a protection agent for a disconnected client computer

To update a protection agent on a disconnected client computer, follow these steps:

1. In DPM Administrator Console, select **Management** and then select the **Agents** tab.

2. Select the client computers on which you want to update the protection agent.

     >[!NOTE]
     >The **Agent Updates** column indicates the protection agent updates available for each protected computer. The **Update** action in the **Actions** pane isn't enabled when a protected computer is selected unless updates are available.

3. To install updated protection agents on selected computers, select **Update**.

      For client computers that aren't connected to the network, **Update Pending** appears in the **Agent Status** column until the computer is connected to the network.

      After a client computer is connected to the network, **Updating** appears on the **Agent Updates** column for the client computer.


