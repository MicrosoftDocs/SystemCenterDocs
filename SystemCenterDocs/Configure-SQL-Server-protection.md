---
title: Configure SQL Server protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d173806c-042f-44d1-a4a2-1e9dbbd0ff53
---
# Configure SQL Server protection
This topic provides the information that you should consider when you’re planning to protect a Microsoft SQL Server database by using Data Protection Manager \(DPM\).

## Which SQL Server versions and functionality does DPM support?
**Versions**

-   SQL Server 2005

-   SQL Server 2008

-   SQL Server 2008 R2

-   SQL Server 2012

-   SQL Server 2014

**Functionality**

-   **SQL clustering**

    In a SQL Server clustering deployment that is protected by a DPM server, when the instance of SQL Server fails over to another node, the DPM server will continue to protect the primary node of the SQL Server cluster without intervention from backup administrators.

    DPM is cluster aware when it is protecting a SQL cluster. DPM is aware of the cluster’s identity in addition to the nodes in the cluster. In a SQL clustering scenario, if the instance of SQL Server is changed to a different node, DPM will continue to protect the SQL cluster without any intervention from backup administrators.

-   **SQL mirroring**

    When a DPM server is protecting a SQL Server database that is mirrored, the DPM server is aware of the mirrored database and correctly protects the shared dataset.

-   **SQL log shipping**

    In scenarios in which SQL Server log shipping is being used, DPM will automatically discover that log shipping is being used and will auto\-configure itself to coexist. This makes sure of correct SQL protection.

-   **SQL AlwaysOn**

    When DPM is protecting SQL AlwaysOn, it will automatically detect availability groups. It will also detect a failover occurrence and will continue to protect the database.

    For more information about SQL protection prerequisites, go to this page [SQL Server prerequisites](./SQL-Server-prerequisites.md). We recommend that you read through the SQL Server prerequisites page before you set up your SQL protection.

## Prepare DPM before you configure SQL Server protection
Before you set up SQL Server protection, you should make sure that you follow these steps:

1.  **Deploy DPM**—Verify that DPM is installed and deployed correctly. If you do not have DPM deployed, go to the following links for guidance:

    -   [System requirements for DPM](assetId:///179c6de2-77c7-4a3f-aaaf-8196dd185961)

    -   [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4)

    -   [Supported and unsupported scenarios in DPM](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc)

    -   [Install DPM](assetId:///d373e205-a09d-466a-bc43-9023d94c788f)

2.  **Set up storage**—Check that you have storage set up. Read more about your options in the following articles:

    -   Learn about short\-term storage to disk and storage pools in [Plan for disk backups](assetId:///8e0f8d8b-8ad9-4ce6-b803-ea5ae58f9a0d).

    -   For storage to Azure with Azure Backup, see [Plan for Azure backups](assetId:///6f34d58a-fd3c-4488-8ac3-3dc463dddaec).

    -   For long\-term storage to tape, see [Plan for tape\-based backups](assetId:///d6fabe7f-3f0b-4086-b3b9-ba47ebb04645).

3.  **Set up the DPM protection agent**—The agent has to be installed on the instance of SQL Server. Read [Plan for protection agent deployment](assetId:///3ad6fd02-f511-4be5-9b5a-03e92409f59e), and then [Set up the protection agent](assetId:///93a339b5-1ace-4982-a280-5464004d4886).

## Set up a protection group for the instance of SQL Server

1.  In the DPM console click **Protection**

2.  Click **New** to start the **Create New Protection Group** wizard.

3.  On the **Select Group Members** page of the **Create New Protection Group** wizard, under **Available members**, expand your instance of SQL Server.

4.  The instances of SQL Server on that server will be shown. You have the option of selecting protection at the instance level or protection of individual databases. Continue through the rest of the wizard to complete the setup of your SQL protection.

More information about creating protection groups can be found in this article [Create and manage protection groups](assetId:///2ce48037-9d6e-43a0-b3ac-cb3bb429dabd).

**Note:** When you are protecting at the instance level, any database that is added to that instance of SQL Server will automatically be added to DPM protection. See the following screen shot for an example of auto\-protection at the instance level and of individual database protection.

**Note:** If you are using SQL Server AlwaysOn availability groups, you can create a protection group that contains the availability groups. The DPM server detects the availability groups and will display them under **Cluster Group**. Select the whole group to protect it so that any databases that you add to the group are protected automatically. You can also select individual databases instead of the whole group.

For each instance of SQL Server, you can also run a system state backup or full bare metal backup \(this includes the system state\). This in useful if you want to be able to recover your whole server and not just data. More information about protection groups and bare metal backup can be found in the following articles:

1.  [Plan for protection groups](assetId:///85cae9ee-0d7c-410a-b8c1-c62a9c4e2fb9)

2.  [Plan for protection group long\-term and short\-term protection](assetId:///f2df4e26-7911-4839-b4fe-e86567b32a6c)

3.  [Back up and restore server system state and bare metal recovery &#40;BMR&#41;](./Back-up-and-restore-server-system-state-and-bare-metal-recovery--BMR-.md)

4.  Then follow the instructions in [Create and manage protection groups](assetId:///2ce48037-9d6e-43a0-b3ac-cb3bb429dabd)

After you create the protection group, initial replication of the data occurs. Backup then occurs in line with the protection group settings.

## Monitoring notifications
After the protection groups are created, the initial replication occurs, and DPM starts backing up and synchronizing the SQL Server data. You can use DPM to monitor the initial synchronization and successive backups in the following ways:

-   Using default DPM monitoring can set up notifications for proactive monitoring by publishing alerts and configuring notifications. You can send notifications by email for critical, warning, or informational alerts, and for the status of instantiated recoveries.

-   If you have System Center Operations Manager \(SCOM\) deployed in the organization, you can use SCOM for deeper DPM monitoring and management. DPM monitoring and management in SCOM is sufficient in meeting your SQL protection monitoring needs. For more information, see this article: [Manage and Monitor DPM](assetId:///27003e8a-6ced-4dc2-881c-8200acdf7c4a).

#### Set up monitoring notifications

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  Click **SMTP Server**, and then type the server name, port, and email address from which notifications will be sent. The address must be valid.

3.  In **Authenticated SMTP server** , type a user name and password. The user name and password must be the domain account name of the person whose “From” address is described in the previous step. Otherwise, notification delivery fails.

4.  To test the SMTP server settings, click **Send Test E\-mail**, type the email address to which you want DPM to send the test message, and then click **OK**.

5.  Click **Options** > **Notifications**, and then select the kinds of alerts about which recipients want to be notified. In **Recipients**, type the email address of each recipient to whom you want DPM to send copies of the notifications.

6.  To test the SMTP server settings, click **Send Test Notification** > **OK**.


