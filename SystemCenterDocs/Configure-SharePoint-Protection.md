---
title: Configure SharePoint Protection
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92263bcb-8d17-4bfe-9e41-b7f52da896ae
---
# Configure SharePoint Protection
This topic describes how to configure protection for SharePoint data with [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)], or DPM 2012 R2.

## Before you start
Read through the [Prerequisites for SharePoint protection](./Prerequisites-for-SharePoint-protection.md) before you set up protection.

## Set up protection

1.  **Deploy DPM**—Verify that DPM is installed and deployed correctly. If it isn’t see:

    -   [System requirements for DPM](assetId:///179c6de2-77c7-4a3f-aaaf-8196dd185961)

    -   [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4)

    -   [Supported and unsupported scenarios in DPM](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc)

    -   [Install DPM](assetId:///d373e205-a09d-466a-bc43-9023d94c788f)

2.  **Set up storage**—Check that you have storage set up. Read more about your options in:

    -   Learn about short\-term storage to disk and storage pools in [Plan for disk backups](assetId:///8e0f8d8b-8ad9-4ce6-b803-ea5ae58f9a0d)

    -   For storage to Azure with Azure Backup, see [Plan for Azure backups](assetId:///6f34d58a-fd3c-4488-8ac3-3dc463dddaec)

    -   For long\-term storage to tape, [Plan for tape\-based backups](assetId:///d6fabe7f-3f0b-4086-b3b9-ba47ebb04645)

3.  **Set up the DPM protection agent**—The agent needs to be installed on the SQL Server.  Read [Plan for protection agent deployment](assetId:///3ad6fd02-f511-4be5-9b5a-03e92409f59e), and then [Set up the protection agent](assetId:///93a339b5-1ace-4982-a280-5464004d4886). The agent should be installed on every server in the SharePoint farm, including SQL Servers.

4.  **Configure the SharePoint VSS Writer service \(WSS Writer service\)**—You’ll need to start and configure this before you can protect SharePoint. You run the ConfigureSharePoint.exe to do this. After the DPM agent is installed it’s located in the <DPM Installation Path>\\bin folder on the front\-end Web server This tool provides the protection agent with the credentials for the SharePoint farm. You run it on a single WFE server. If you have multiple WFE servers select just one when you configure a protection group.

    1.  On the WFE server, at a command prompt, go to *<DPM installation location>*\\bin\\.

    2.  Run **ConfigureSharePoint \-EnableSharePointProtection**.

    3.  Enter the farm administrator credentials. This account should be a member of the local Administrator group on the WFE server. If the farm administrator isn’t a local admin grant the following permissions on the WFE server:

        -   Grant the WSS\_Admin\_WPG group full control to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] folder \(%Program Files%\\Microsoft Data Protection Manager\\DPM\).

        -   Grant the WSS\_Admin\_WPG group read access to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Registry key \(HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\).

    After running ConfigureSharePoint.exe to begin protection you’ll need to rerun it if there’s a change in the SharePoint farm administrator credentials. See more details about the tool in [Using ConfigureSharePoint](http://go.microsoft.com/fwlink/p/?LinkId=234748).

5.  Set **Set up a protection group**—In the **Select Group Members** page of the **Create New Protection Group wizard**. When you select resources to protect in the group you’ll see the SharePoint icon.  For each SharePoint server you can also select to do a system state backup or full bare metal backup \(which includes the system state. This in useful if you want the ability to recover your entire server and not just data.Read about protection groups and bare metal backup in:

    -   [Plan for protection groups](assetId:///85cae9ee-0d7c-410a-b8c1-c62a9c4e2fb9)

    -   [Plan for protection group long\-term and short\-term protection](assetId:///f2df4e26-7911-4839-b4fe-e86567b32a6c)

    -   [Back up and restore server system state and bare metal recovery &#40;BMR&#41;](./Back-up-and-restore-server-system-state-and-bare-metal-recovery--BMR-.md)

    -   Then follow the instructions in [Create and manage protection groups](assetId:///2ce48037-9d6e-43a0-b3ac-cb3bb429dabd).

6.  After you create the protection group initial replication of the data occurs. Backup then takes place in line with the protection group settings.

## Set up monitoring
After the protection group’s been created the initial replication occurs and DPM starts backing up and synchronizing the SharePoint data. DPM monitors the initial synchronization and subsequent backups. You can monitor the SharePoint data in a couple of ways:

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


