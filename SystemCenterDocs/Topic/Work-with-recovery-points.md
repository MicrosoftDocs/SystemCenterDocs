---
title: Work with recovery points
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d1291f8-bb9f-4014-9b51-3dbc5e82d990
---
# Work with recovery points
[!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] relies on recovery point technology to allow you to recover your data. A *recovery point*, also referred to as a snapshot, is a point\-in\-time copy of the files and folders that are protected by the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

A *recovery point*, also referred to as a *snapshot*, is a point\-in\-time copy of a replica stored on the server for [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)]. A *replica* is a complete point\-in\-time copy of the protected shares, folders, and files for a single volume on a protected computer.

To start data protection, a full replica of the selected data must be copied to the allocated replica volume on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server.

> [!NOTE]
> With data co\-location the allocated replica volume will be shared by other data sources to include their replicas.

Thereafter, the replica is periodically synchronized with changes to the protected data. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] creates recovery points of each replica in a protection group according to a specified schedule. You can access the recovery points to recover previous versions of files in the event of data loss or corruption. You can recover data, and you can also configure end\-user recovery so that users can recover their own data.

When you select recovery point times, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] provides you with estimates for recovery range and maximum data loss. These estimates can help you specify a recovery point schedule that provides adequate data protection and meets your recovery goals. A maximum of eight recovery points can be scheduled per day.

In the **Recovery** task area, you can access recovery points to recover previous versions of files in the event of data loss or corruption. DPM administrators can recover data, or they can configure end\-user recovery so that end users can independently recover their own data.

In the **Protection** task area, you can manually create an immediate recovery point to disk or tape. You can also modify the protection options for a protection group to specify when and how often to create recovery points.

> [!NOTE]
> You can delete a recovery point only by using DPM Management Shell. You cannot delete a recovery point using DPM Administrator Console.

## In this section
[How to Create a Recovery Point](assetId:///bbecae31-8189-4f09-915e-ceb8287de091)

[How to Show All Recovery Points](assetId:///a6683e5f-0ff7-47f1-8ffc-b9e36b2a67d2)

[How to Modify a Recovery Point Schedule](assetId:///b31e11bb-8688-4767-855c-0459fcde0001)

[How to Delete a Recovery Point](assetId:///a99a8ade-6a49-4897-85fb-a3bc150dba19)

