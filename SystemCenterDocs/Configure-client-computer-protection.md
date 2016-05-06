---
title: Configure client computer protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a6734d7-245c-4522-b7c3-bccd64909efa
---
# Configure client computer protection
DPM can back up client computer file data.

## Before you start
Read through the [Back up client computers with DPM](../Topic/Back-up-client-computers-with-DPM.md) before you set up protection.

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

3.  **Set up the DPM protection agent**—The agent needs to be installed on client computers you want to protect.  Read [Plan for protection agent deployment](assetId:///3ad6fd02-f511-4be5-9b5a-03e92409f59e), and then [Set up the protection agent](assetId:///93a339b5-1ace-4982-a280-5464004d4886).

4.  **Set up a protection group**—Set up a protection group that includes the client computers you want to protect.

    Read more about protection groups in:

    -   [Plan for protection groups](assetId:///85cae9ee-0d7c-410a-b8c1-c62a9c4e2fb9)

    -   [Plan for protection group long\-term and short\-term protection](assetId:///f2df4e26-7911-4839-b4fe-e86567b32a6c)

    -   [Back up and restore server system state and bare metal recovery &#40;BMR&#41;](../Topic/Back-up-and-restore-server-system-state-and-bare-metal-recovery--BMR-.md)

    -   Then follow the instructions in [Create and manage protection groups](assetId:///2ce48037-9d6e-43a0-b3ac-cb3bb429dabd). Note that when you run the New Protection Group Wizard you’ll be able to configure Exchange\-specific settings the wizard.

    Note the following:

    -   On the **Select Group Members** page of the **Create New Protection Group wizard**. Click **Add Multiple Computers** to add the client computers you want to protect. You must enter each computer in the file on a new line. We recommend that you provide the FQDN target computers. For example, enter multiple computers in a .txt file as follows:

        -   Comp1.abc.domain.com

        -   Comp2.abc.domain.com

        -   Comp3.abc.domain.com

        If [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] can’t find any of the computers that you specified in the .txt file or that you entered in the **Text file location** box, the failed set of computers is placed in a log file. Click the **Failed to add machines** link at the bottom of the page to open the log file.

    -   On the **Specify Inclusions and Exclusions** page, specify the folders to include or exclude for protection on the selected computers. To select from a list of well\-known folders, such as **Documents**, click the drop\-down list. Note that:

        -   When you exclude a folder, and then specify a separate inclusion rule for a subfolder, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] doesn’t back up the subfolder. The exclusion rule overrides the inclusion rule.

        -   When you include a folder, and then specify a separate exclude rule for a subfolder, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] backs up the entire folder, except for the excluded subfolder.

        -   When you include a well\-known folder such as **Documents**, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] locates the **Documents** folder for all users on the computer, and then applies the rule. For example, if the user profile for computer **Comp1** contains the **Documents** folder for both User1 and User2, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] will back up both folders.

    -   In the **Folder** column you type the folder names using variables such as *programfiles*, or you can use the exact folder name. Select **Include** or **Exclude** for each entry in the **Rule** column.

    -   You can select **Allow users to specify protection members** to give your end users the choice to add more folders on the computer that they want to back up. However, the files and folders you have explicitly excluded as an administrator cannot be selected by the end user.

    -   Under **File type exclusions** you can specify the file types to exclude using their file extensions.

5.  On the Allocate Storage page we recommend that you co\-located multiple client data sources to one replica volume if you have a large number of client computers. You won’t be able to protect 1000 or more client computers with one [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server without co\-locating your data. We recommend that you do not co\-locate if you have less than ten client computers in a protection group. Select **Automatically grow the volumes** to automatically increase size when more disk space is required for protecting data on the client computers.

6.  After you create the protection group initial replication of the data occurs. Backup then takes place in line with the protection group settings.

7.  To add new client computers to an existing protection group you right\-click the group name and select **Add client computers**.

## Set up monitoring
After the protection group’s been created the initial replication occurs and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups. You can monitor the Exchange data in a couple of ways:

-   Using default DPM monitoring can set up notifications for proactive monitoring. by publishing alerts and configuring notifications. You can send notifications by e\-mail for critical, warning, or informational alerts, and for the status of instantiated recoveries.

-   If you use Operations Manager you can centrally publish alerts.

#### Set up monitoring notifications

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  Click **SMTP Server**, type the server name, port, and email address from which notifications will be sent. The address must be valid.

3.  In **Authenticated SMTP server** , type a user name and password.The user name and password must be the domain account name of the person whose “From” address is described in the previous step; otherwise, notification delivery fails.

4.  To test the SMTP server settings, click **Send Test E\-mail**, type the e\-mail address where you want DPM to send the test message, and then click **OK**. Click **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients** type the e\-mail address for each recipient to whom you want DPM to send copies of the notifications.

5.  To test the SMTP server settings, click **Send Test Notification** > **OK**.

#### Publish alerts for Operations Manager

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  In Options click **Alert Publishing** > **Publish Active Alerts**.

3.  After you enable **Alert Publishing** all existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

