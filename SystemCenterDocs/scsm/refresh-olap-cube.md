---
title: Refresh OLAP data cube information
description: Explains how to refresh OLAP data cube information in Service Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 12/12/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: aeb99cdc-6d17-4979-bbf8-76f822e2636b
---

# Refresh OLAP data cube information in Service Manager

You can use the following procedures in Service Manager to refresh data in a Microsoft Online Analytical Processing \(OLAP\) data cube and then validate that it was refreshed. By default, most OLAP data cubes are refreshed every 24 hours. However, you can manually refresh the data to ensure that you're accessing the latest information from the data warehouse.  

 If necessary, you can also manually process an OLAP data cube outside of the processing job.  

## Refresh using the Service Manager console  

1. In the Service Manager console, select **Data Warehouse**, expand it, and select **Cubes**.  

2. In the **Cubes** pane, select a cube name, and then under **Tasks**, select **Process Cube**.  

3. Select **OK** to close the **Process Cube** dialog.  

### Validate refresh

- Select an OLAP data cube and verify that the date and time information under **Last Processed Date** has been updated since you processed the cube and that the cube **Status** is listed as **Processed**.  

## Next steps

- [Manage and use the analysis libraries](manage-analysis-library.md).
