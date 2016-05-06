---
title: Set up system state or BMR protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0aa6cb6e-34a0-4c18-b70a-406770833940
---
# Set up system state or BMR protection
You can back up system state data and data to allow a bare metal recovery \(BMR\)

## Before you start

-   Note that application data isn’t backed up as part of a system state or BMR backup. If an application is installed on a critical volume you’ll be to restore the application after BMR.

-   We recommend you run a BMR backup rather than a system state backup, for optimum protection. A BMR backup includes a system state backup.

## Set up protection

1.  **Deploy DPM**—Verify that DPM is installed and deployed correctly. If you haven’t see:

    -   [System requirements for DPM](assetId:///179c6de2-77c7-4a3f-aaaf-8196dd185961)

    -   [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4)

    -   [Supported and unsupported scenarios in DPM](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc)

    -   [Install DPM](assetId:///d373e205-a09d-466a-bc43-9023d94c788f)

2.  **Set up storage**—Check that you have storage set up. Read more about your options in:

    -   Learn about short\-term storage to disk and storage pools in [Plan for disk backups](assetId:///8e0f8d8b-8ad9-4ce6-b803-ea5ae58f9a0d)

    -   For storage to Azure with Azure Backup, see [Plan for Azure backups](assetId:///6f34d58a-fd3c-4488-8ac3-3dc463dddaec)

    -   For long\-term storage to tape, [Plan for tape\-based backups](assetId:///d6fabe7f-3f0b-4086-b3b9-ba47ebb04645)

3.  **Set up the DPM protection agent**—The agent needs to be installed on the server you want to protect with system state or BMR backup. Read [Plan for protection agent deployment](assetId:///3ad6fd02-f511-4be5-9b5a-03e92409f59e), and then [Set up the protection agent](assetId:///93a339b5-1ace-4982-a280-5464004d4886).

4.  **Set up a protection group**—In the **Select Group Members** page of the **Create New Protection Group wizard** BMR will appear as a data source under the **System Protection** node or you can select to back up system state only. Read about protection groups in:

    1.  You can’t protect BMR and system state for the same computer on different protection groups.

    2.  When you select BMR, system state gets selected.

    3.  If you stop protection for BMR, system state protection is not stopped automatically. You need to specifically clear the **System State** check box to stop it.

    Read more in:

    -   [Plan for protection groups](assetId:///85cae9ee-0d7c-410a-b8c1-c62a9c4e2fb9)

    -   [Plan for protection group long\-term and short\-term protection](assetId:///f2df4e26-7911-4839-b4fe-e86567b32a6c)

    -   Then follow the instructions in [Create and manage protection groups](assetId:///2ce48037-9d6e-43a0-b3ac-cb3bb429dabd).

5.  After you create the protection group initial replication of the data occurs. Backup then takes place in line with the protection group settings. To recover see [Recover system state or BMR](../Topic/Recover-system-state-or-BMR.md).

