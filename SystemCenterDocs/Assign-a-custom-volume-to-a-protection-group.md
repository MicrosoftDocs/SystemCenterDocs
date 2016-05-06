---
title: Assign a custom volume to a protection group
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ac8e15f-5650-48f1-a798-cc9bd2bcc491
---
# Assign a custom volume to a protection group
With DPM, you can assign a custom volume to store replicas and recovery points. This can maximize performance in DPM if you choose to keep certain volumes on separate LUNs \(Logical Unit Numbers\) to enable parallel replication onto these volumes.

After you have created and assigned a custom volume, DPM does not increase the size of this volume as it fills—the administrator must use Disk Management to perform this task. Custom volumes can be assigned only when you create a new protection group or when you add a new member to a protection group.

> [!IMPORTANT]
> You cannot create a custom volume from DPM. You must create the volume by using Disk Management.

### To assign a custom volume when creating a new protection group

1.  Use Disk Management to create a volume of the desired size and name.

2.  In DPM Administration Console, go to the **Protection** view.

3.  Click **New** on the tool ribbon. This starts the Create New Protection Group Wizard.

4.  On the Create New Protection Group page, click Next.

    > [!NOTE]
    > If you do not want DPM to display the **Welcome** page, select the **Do not show the Welcome page again** box.

5.  Select group members for the protection group, and click **Next**.

6.  Select the data protection method, and click **Next**.

7.  Select your short\-term protection objectives, and click **Next**.

8.  On the **Review Disk Allocation** page, in the **Disk space allocation for new members** pane, click **Modify**.

9. On the **DPM Server** tab, in the **Storage Type** column, select **Custom Volume** from the pull\-down menu.

    > [!IMPORTANT]
    > You can specify a custom volume only for the new members of the protection group.

10. In the **Replica Volume** column, from the pull\-down menu, select the volume that DPM will use to store the replica volume for the protection group member.

11. In the **Recovery Point** column, from the pull\-down menu, select the volume that DPM will use to store the recovery point volume for the protection group member.

12. In the **Custom Volume** column, select whether to format the disk from the drop\-down menu.

    > [!NOTE]
    > Select **Do not format** when the custom volume is used in a storage area network.

13. Click **OK**, and then click **Next**.

14. Complete the Create New Protection Group Wizard. On the **Summary** page, click **Create Group**.

### To assign a custom volume when modifying a protection group

1.  Use Disk Management to create a volume of the desired size and name.

    > [!NOTE]
    > You can assign a custom volume only for the new members of the protection group.

2.  In DPM Administration Console, go to the **Protection** view.

3.  In the display pane, select the protection group you want to modify.

4.  Click **Modify** on the tool ribbon to start the Modify Protection Group Wizard.

5.  Select group members for the protection group, and click **Next**.

6.  Select the data protection method, and click **Next**.

7.  Select your short\-term protection objectives, and click **Next**.

8.  On the **Review Disk Allocation** page, in the **Disk space allocation for new members** pane, click **Modify**.

9. On the **DPM Server** tab, in the **Storage Type** column, select **Custom Volume** from the pull\-down menu.

10. In the **Replica Volume** column, from the pull\-down menu, select the volume that DPM will use to store the replica volume for the protection group member.

11. In the **Recovery Point** column, from the pull\-down menu, select the volume that DPM will use to store the recovery point volume for the protection group member.

12. In the **Custom Volume** column, select whether to format the disk from the drop\-down menu.

    > [!NOTE]
    > Select **Do not format** when the custom volume is used in a storage area network.

13. Click **OK**, and then click **Next**.

14. Complete the Modify Protection Group Wizard. On the **Summary** page, click **Update Group**.

## See Also
[New Protection Group Wizard \[DPM2012\_Web\]](assetId:///1b3b1b30-7b8d-44ca-8137-d94176290480)
[Manage the disk storage pool](../Topic/Manage-the-disk-storage-pool.md)

