---
title: Set up data backup storage
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65b22be5-a087-4df8-b2a9-a8e9f644a158
---
# Set up data backup storage
Your [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] deployment can use the following storage options for backed up data:

-   **Tape**—Tape is generally used for long\-term storage of backed up data. DPM can also be configured to use tapes for short\-term backup of file data. Read more in [Plan for tape\-based backups](assetId:///d6fabe7f-3f0b-4086-b3b9-ba47ebb04645).

-   **Disk**—Data is stored in the DPM storage pool for short\-term backup. The storage pool is a set of disks or volume that you set up as part of the DPM server configuration. Read more in [Plan for disk\-based backups](assetId:///8e0f8d8b-8ad9-4ce6-b803-ea5ae58f9a0d).

-   **Azure**—You can back up data for some workloads using Microsoft Azure Backup.  Read more in [Plan for Azure backups](assetId:///6f34d58a-fd3c-4488-8ac3-3dc463dddaec).

You can read more about putting these storage options together in [Plan DPM storage](assetId:///651bce70-4334-44e8-88a7-84f185f8c8d8).

-   **Disk\-to\-tape \(D2T\)**—Back up directly from the disk of a protected computer directly to tape

-   **Disk\-to\-disk \(D2D\)—**—Back up from the disk of a protected computer to another hard disk for short\-term storage.

-   **Disk\-to\-disk \(D2D\) \+ cloud**—Back up from the disk of a protected computer to another hard disk and to Microsoft Azure for short\-term storage.

-   **Disk\-to\-disk\-to\-tape \(D2D2T\)**—Back up from the disk or a protected computer to another hard disk and then backup to tape for longer\-term offsite storage.

The deployment steps you need to complete depend on the storage option you want to use:

## In This Section

-   [Configure storage pools and disk storage](assetId:///a9b893b9-bf55-4eab-b03a-4abcf7923a93)

-   [Configure backup to Azure](assetId:///badf8928-9678-46c3-b444-5ab4ad01596f)

-   [Configure tape storage](assetId:///34bea8ca-10b9-493e-84be-b5db93f0251b)

