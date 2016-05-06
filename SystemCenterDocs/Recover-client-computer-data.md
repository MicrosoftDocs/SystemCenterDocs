---
title: Recover client computer data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42676258-525d-495e-97e4-2161fe1e272d
---
# Recover client computer data
You can recover client computer data using the Recovery Wizard as described in this topic. You can also let end users recover their own data. For more details see [Configure end-user recovery and recover file data](Configure-end-user-recovery-and-recover-file-data.md).

1.  In [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Administrator Console, click **Recovery** on the navigation bar.

2.  Browse or search for the data you want to recover, and then, in the results pane, select the data.

3.  Available recovery points are indicated in bold on the calendar in the recovery points section. Select the bold date for the recovery point you want to recover.

4.  In the **Recoverable item** pane, click to select the recoverable item you want to recover.

5.  In the **Actions** pane, click **Recover**. [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] starts the Recovery Wizard.

6.  Review your recovery selection, and click **Next**.

7.  Specify the type of recovery you would like to perform:

    1.  **Recover to the original location**.

        > [!WARNING]
        > If a client computer is connected over a Virtual Private Network \(VPN\), the recovery will fail. We recommend that you restore the data to an alternate location \(such as a share\), and then provide that share to the end user so they can copy their data.

    2.  **Recover to an alternate location**. Click **Browse** to browse for an alternate recovery destination. On the **Specify Alternate Recovery Destination** dialog box, select the recovery destination and click **OK**.

    3.  **Copy to tape**. This option copies the volume that contains the selected data to a tape in a [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] library. Click **Next**, and on the **Specify Library** dialog box, select library details and tape options. You can also choose to compress or encrypt the data on tape.

8.  Click **Next** after you have specified one of the preceding options.

9. Specify your recovery options:

    1.  **Existing version recovery behavior**. Select **Create copy**, **Skip**, or **Overwrite**. This option is enabled only when you selected **Recover to the original location** in step 7.

    2.  **Restore security**. Select **Apply settings of the destination computer** or **Apply the security settings of the recovery point version**.

    3.  **Network bandwidth usage throttling**. Click **Modify** to enable network bandwidth usage throttling.

    4.  **Enable SAN based recovery using hardware snapshots**. Select this option to use SAN\-based hardware snapshots for quicker recovery.

        This option is valid only when you have a SAN where hardware snapshot functionality is enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server are connected to the same SAN.

    5.  **Notification**. Click **Send an e\-mail when the recovery completes**, and specify the recipients who will receive the notification. Separate the e\-mail addresses with commas.

10. Click **Next** after you have made your selections for the preceding options.

11. Review your recovery settings, and click **Recover**.

    > [!NOTE]
    > Any synchronization job for the selected recovery item will be canceled while the recovery is in progress.


