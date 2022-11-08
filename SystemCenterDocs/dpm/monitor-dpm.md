---
description: This article describes the way that you can monitor DPM.
manager: carmonm
ms.topic: article
author: jyothisuri
ms.prod: system-center
keywords:
ms.date: 11/08/2022
title: Monitor DPM
ms.technology: data-protection-manager
ms.assetid: 99901174-76d4-4eb7-a72b-3ec300f1fa0b
ms.author: jsuri
---

# Monitor DPM

::: moniker range=">= sc-dpm-1801 <= sc-dpm-1807"

[!INCLUDE [eos-notes-data-protection-manager.md](../includes/eos-notes-data-protection-manager.md)]

::: moniker-end

You can monitor a single System Center Data Protection Manager (DPM) server from the DPM Administrator console, multiple DPM servers from the Central Console, or monitor DPM activity with Operations Manager.

## Monitor with the DPM console
To monitor DPM in the console, you should be logged on to the DPM server with a local admin account. Here's what you can monitor:

-   On the **Alerts** tab, you can monitor errors, warnings, and general information for a protection group, for a specific protected computer, or by message severity.  You can view active and inactive alerts and [set up email notifications](#configure-email-for-dpm).

-   On the **Jobs** tab, you can view jobs initiated by DPM for a specific protected computer or protection group. You can  follow job progress or check resources consumed by jobs.

-   In the **Protection** task area, you can check the status of volumes and shares in protection group, and check configuration settings such as recovery settings, disk allocation, and backup schedule.

-   In the **Management** task area, you can view the **Disks, Agents**, and **Libraries** tab to check the status of disks in the storage pool, deployed DPM agent status, and the state of tapes and tape libraries.

::: moniker range="sc-dpm-2022"

### Configure Email for DPM

**Use on-premises SMTP server to configure email for DPM**

Follow the below steps to configure email for DPM using on-premises SMTP server:

1. In the DPM console, select **Actions** > **Options** and then select the **SMTP Server**.
1. In **SMTP Server**, do the following:
    1. **SMTP server name**: Enter the fully qualified domain name of the SMTP server.
    1. **SMTP server port**: Enter the fully qualified domain name of the server port. 
    1. **"From" address**: Configure the **From** address, should be a valid email address on the SMTP server. 
    1. **Authenticated SMTP server**: Enter the domain user e.g., **domain\username** and password to authenticate to the SMTP server.  
1. Select **Send Test E-mail** to verify if the setup is working.
1. Select **OK** to save the details.

    :::image type="SMTP Server" source="media/monitor-dpm/smtp-server.png" alt-text="Screenshot of SMTP server tab.":::

**Use O365 SMTP to configure email for DPM**

DPM supports O365 without a relay agent. 

Use *office365 smtp server: smtp.office365.com* on ports 25 and 587 to configure email for alerts and reports. If you use O365, ensure to use the username and password for O365 instead of the domain user.
    
::: moniker-end

## Monitor DPM in the Central Console
Central Console is a System Center Operations Manager console that you can deploy to manage and monitor multiple DPM servers from a single location. In the Central Console you can monitor and track the status of multiple DPM servers,  jobs, protection groups, tapes, storage, and disk space.

-   In **View Jobs**, you can get a list of jobs running on all DPM server monitored by Central Console.

-   In **Alert View**, you can get a list of all DPM alerts that require action. You can using the **Troubleshoot** option to get more details for an alert.

    You can consolidate alerts in the console.  You can display a single alert for repeated alerts, or display a single alert for multiple alerts that have the same root cause. If you're using a ticketing system, you can generate a single ticket only for repeated alerts.

-   In **State View**, you can get information about the state of  DPM objects.

## Monitor DPM in the Azure console

>[!NOTE]
> For the backed up items to be visible in the Azure portal, the DPM version must be 1807 (5.1.378.0) or 2019 (version 10.19.58.0 or later) .

You use the Dashboard to get a quick overview of the state of your System Center - Data Protection Manager (DPM) backups in Windows Azure Backup. The Dashboard provides a centralized gateway to view servers protected by backup vaults, as follows:

-   **Usage Overview** shows how you are using the backup vault. You can select a vault and see how much storage is being consumed by the vault, versus the amount of storage provided by your subscription. You can also see the number of servers registered to the vault.

-   **Quick Glance** displays crucial configuration information about the backup vault. It tells you whether the vault is online, which certificate is assigned to it, when the certificate expires, the geographic location of the storage servers, and subscription details for the service.

From the dashboard you can download the Backup agent for installation on a server, modify settings for certificates uploaded to the vault, and delete a vault if necessary.

::: moniker range="sc-dpm-2019"

##	Central Monitoring
All DPM-A customers (customer connected to Azure) have the flexibility of using Central Monitoring, a monitoring solution provided by Microsoft Azure Backup. You can monitor both on premise and cloud backups, using Log Analytics with Central Monitoring. You can use this monitoring solution to monitor your key backup parameters such as backups jobs, backup alerts, and cloud storage across all your recovery service vaults & subscriptions. You can also create alert notifications and open tickets using webhooks or ITSM integration.

> [!NOTE]
> You must have a valid Azure subscription to be able to centrally monitor.

**Enable central monitoring**

1.	Logon to Azure portal.
2.	[Create a Recovery Service vault](/azure/backup/backup-azure-vms-first-look-arm#back-up-from-azure-vm-settings), or if you already have one, select the same.
3.	Select **Diagnostic Settings** under **Monitoring** section.
    ![Diagnostics settings](./media/monitor-dpm/diagnostic-settings.png)
4. Click **Turn on Diagnostic Settings**.
5. In the **Diagnostic settings** window, give a valid setting name, select **Send to Log Analytics**, select the relevant log analytics workspace or [create one](/azure/azure-monitor/learn/quick-create-workspace), select the relevant log, *AzureBackupReport*, and click **Save**.

    > [!NOTE]
    > Choose the same workspace for all the vaults to get a centralized view in the workspace. Allow 24 hours for initial data push to complete post completing the configuration.


    Here is a sample backup report:

    ![backup report](./media/monitor-dpm/azure-backup-report.png)

**Monitor Backup Data**
1.	Select your Log Analytics workspace.
2.	Click **OMS Portal**.
    The solution dashboard is displayed and provides you with all the backup information as shown below:

    Sample 1:

    ![Backup report dashboard](./media/monitor-dpm/monitor-backup-image1.png)

    Sample 2:

    ![Backup jobs report](./media/monitor-dpm/monitor-backup-image2.png)

3. You can also monitor active alerts, current data sources being backed-up and cloud storage as shown below:

    ![Azure backup report](./media/monitor-dpm/monitor-backup-image3.png)

4. You can also specify the desired time range for monitoring the backup parameters.

    ![Timeframe for monitoring](./media/monitor-dpm/specify-timeframe.png)

**Create Custom Alerts**
1.	Click any values in the above graph to view more details in the Logs window.
2.	Click **Alert** icon.
3.	Select **Take me to Azure Alerts**.
4.	In Log Analytics workspace, click **New Alert Rule**.
5.	Define the **alert condition**, **alert details** and **action group**.
6.	[Learn more](/azure/azure-monitor/learn/tutorial-response#create-alerts) about how to configure new alerts.

::: moniker-end

::: moniker range=">= sc-dpm-1807"

## Backup items in Recovery Services vault

You can monitor the backed-up items using Recovery Services vault. From the Recovery Services vault, navigate to **Backup items** to view the number of items backed-up for each workload type, associated with the vault. Click the workload item to view the detailed list of all items backed-up for the selected workload.

Here is a sample view:

![Recovery vault backup items](./media/monitor-dpm/back-up-items-view.png)

- To view the list of backup items, select *DPM* or *Azure Backup Server* under **Backup Management Type**.   

  ![Backup items list](./media/monitor-dpm/back-up-items-list.png)

  >[!NOTE]
  > - The Latest Recovery Point will always display the latest disk recovery point available for the backup item.
  > - Some datasources in the Backup items (DPM) view from recovery service vault in Azure portal, are not getting refreshed/updated. Check the workarounds to fix this [known issue](./dpm-release-notes.md?#dpm-datasources-not-being-reflected-on-recovery-services-vault).
  > - For the items backed-up to Azure using DPM, the list will show all the data sources protected (both disk and online) using the DPM server. If the protection is stopped for the datasource with backup data retained, the datasource will be still listed in the portal. You can go to the details of the data source to see if the recovery points are present in the disk, online or both. Also, datasources for which the online protection is stopped but data is retained, billing for the online recovery points continue, until the data is completely deleted.
  > - Currently, datasources backed-up directly to tape don't appear in the Recovery Services vault. To make it appear, we recommend you to back up the data to disk for a short term, and then to Azure or tape as required.

- Click the *backup item* to view more details such as latest, oldest and total number of recovery points for disk and cloud, if online protection is enabled.

  ![Backup item details](./media/monitor-dpm/back-up-items-details.png)

> [!NOTE]
> - The *Backup items* view continues to display a datasource even after the protection is stopped. From the datasource details, you will be able to check the available recovery points for online/disk backups. This display continues until you manually remove the existing backup data for the datasource, for which the protection has been stopped.   
>
> - Also, datasources for which the online protection is stopped but data is retained, billing continues for the online recovery points until the data is completely deleted.


::: moniker-end

## Monitor DPM in Operations Manager
You can use monitor and report on the health and status of DPM servers using System Center Operations Manager Management Packs for DPM. DPM provides the following management packs, use these as applicable for the DPM version you are using:

-   **Reporting management pack** (Microsoft.SystemCenter.DataProtectionManager.Reporting.mp) - Collects and displays reporting data from all DPM servers, and exposes a set of Operations Manager warehouse views for DPM. You can query these views to generate custom reports.

-   **Discovery and monitoring management pack** (Microsoft.SystemCenter.DataProtectionManager.Discovery.mp)

-   **Library management pack** - (Microsoft.SystemCenter.DataProtectionManager.Library)


Using these packs you can:

-   Centrally monitor the health and status of DPM servers, protected servers and computers, and backups.

-   View the state of all roles on DPM servers and protected data sources.
    Monitor, identify, action, and troubleshoot alerts.

-   Use Operations Manager alerts to monitor DPM server memory, CPU, and disk resources, and database.

-   Monitor resource usage and performance trends on DPM servers.

### Prerequisites

-   To use the DPM Management Packs, you need a System Center Operations Manager server running. The Operations Manager Data Warehouse must be up and running.

-   If you're running a previous version of the Discover and Library Management Packs obtained from the DPM installation media, you should remove them from the DPM server and install the new versions from the download page.

-   You can only run one language version of the Management Pack at one time. If you want to use the pack in a different language uninstall the pack in the existing language and then install it with the new language.

-   If any previous versions of a DPM Management Pack are installed on the Operations Manager server, remove them before installing the new pack.

### Set up the Management Packs
Install the Operations Manager agent on each DPM server you want to monitor.
Then obtain the Management Packs, import the Discovery and Library Management Packs, install the DPM Central Console, and import the Reporting Management Pack

#### Install the agent and obtain the Management Packs

1.  For agent installation options read [Operations Manager Installation Methods](../scom/deploy-overview.md?preserve-view=true&view=sc-om-1807).
    If you need to obtain the latest version of the agent see [Microsoft Monitoring Agent](/services-hub/health/mma-setup) in the Download Center.

2.  Download the packs from the [Download Center](https://www.microsoft.com/download/details.aspx?id=9296).
    The download places the Discovery and Library Management Packs in the C:\Program Files\System Center Management Packs folder. The reporting management pack is placed in a separate folder inside that folder.

#### Import the Management Packs
Import the Discovery and Library Management Packs
Log on to the Operations Manager server with an account that is a member of the Operations Manager Administrators role.
Remember to remove any previous versions of the Library or Discover Management Packs running on the server.

1.  In the Operations console, click **Administration**. Right-click **Management Packs** > **Import Management Packs**.
     Select **Microsoft.SystemCenter.DataProtectionManagerDiscovery.MP** > **Open** and then **Microsoft.SystemCenter.DataProtectionManagerLibrary.MP** > **Open**

2.  Follow the instructions in the Import Management Packs wizard. You can get more information about running this wizard in [How to Import an Operations Manager Management Pack](/previous-versions/system-center/system-center-2012-R2/hh212691(v=sc.12)).

#### Set up Central Console
You'll need to install the DPM Central Console on the Operations Manager server. This console is used to manage multiple DPM servers in Operations Manager.

1.  In the **Setup** screen of Operations Manager, select the following:

    -   Select **Install Central Console Server and Client side Components** if you want to monitor DPM servers with the Management Pack and you want to use the Central Console to manage settings and configuration on the DPM servers.

    -   Select **Install Central Console Server side Components** if you only want to monitor DPM servers with the Management Pack, but don't want to use Central Console to manage settings and configuration on the DPM servers.

2.  DPM adds firewall exceptions for port 6075 for the console. You should also open ports for SQL Server.exe and SQL browser.exe

#### Import the Reporting Manager Pack


1.  Log on to the Operations Manager server with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**. Right-click **Management Packs** > **Import Management Packs**.

3.  Select **Microsoft.SystemCenter.DataProtectionManagerReporting.MP** > **Open**.
    Follow the instructions in the Import Management Packs wizard.

#### Tweaking Management Pack settings

After you import the management packs, they discover and monitor data without requiring any additional configuration. You can optionally tweak settings like monitors and rules for your environment. For example, if you find that performance-measuring rules that are enable degrade server performance with slow WAN links, you can disable them. For instructions, see [How to enable or disable a rule or monitor](/previous-versions/system-center/system-center-2012-R2/hh212818(v=sc.12)).
