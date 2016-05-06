---
title: Troubleshoot SharePoint Protection and Recovery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88144045-81bc-4330-a84c-edb12ed98d43
---
# Troubleshoot SharePoint Protection and Recovery
This topic documents the following known issues and resolutions relating to protection and recovery of SharePoint data protected by [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)]:

-   [Unable to search SharePoint items in the Recovery task area.](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_UnableToSearch)

-   [SharePoint farm protection fails with ID 956](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_SharePointFarmProtection956)

-   [Recovery of a SharePoint content database fails with ID 0x80070003](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_RecoveryOfDatabaseFails0x80070003)

-   [On a secondary DPM server \(DPM\-DR\), even though incremental and express full jobs happen successfully for a SQL Server database that belong to a SharePoint farm, recovery points are not displayed in Recovery task area and no alerts are triggered.](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_SecondaryDPMServer)

-   [SharePoint documents checked out or in the Recycle Bin during backup cannot be restored](./Troubleshoot-SharePoint-Protection-and-Recovery.md#CheckOutDuringBackup)

-   [DPM Protection Report shows incorrect data for SharePoint farms](./Troubleshoot-SharePoint-Protection-and-Recovery.md#ProtectionReportIncorrect)

-   [SharePoint Protection not working properly](./Troubleshoot-SharePoint-Protection-and-Recovery.md#WSSProtectionNotWorking)

-   [SharePoint site or item recovery fails when a shared folder is used as a temporary location](./Troubleshoot-SharePoint-Protection-and-Recovery.md#SharePointFailsOnSharedFolder)

-   [SharePoint farm protection fails with ID 30111](./Troubleshoot-SharePoint-Protection-and-Recovery.md#SharepointprotectionfailswithID30111)

-   [SharePoint index backups fail during profile import](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_SharePointIndexBackupsFailDuringProfileInput)

-   [ConfigureSharepoint.exe fails with error code 997](./Troubleshoot-SharePoint-Protection-and-Recovery.md#BKMK_ConfigureSharePointError997)

## <a name="BKMK_UnableToSearch"></a>Unable to search SharePoint items in the Recovery task area.
In [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)], to search for SharePoint items such as list items in the Recovery task area, follow these steps:

1.  On the **Search** tab, in the **Search** list, select **SharePoint**.

2.  In the **SharePoint search** pane, click **Search Documents**.

3.  In the **Name** list, select **Contains** as the search string.

4.  Enter the name of the list item you want to recover.

> [!NOTE]
> -   To search list items, you must select only **Contains** as the search string.
> -   Ensure that you have selected the correct SharePoint farm name.

## <a name="BKMK_SharePointFarmProtection956"></a>SharePoint farm protection fails with ID 956
This happens when in the SharePoint farm, the name of the SQL Server is not configured as a fully qualified domain name \(FQDN\), and only a NETBIOS name is provided. To resolve this issue, reconfigure the SharePoint server with the FQDN of the SQL Server by running the command **Stsadm –o renameserver** on the front\-end Web server from where you plan to protect the SharePoint farm data.

## <a name="BKMK_RecoveryOfDatabaseFails0x80070003"></a>Recovery of a SharePoint content database fails with ID 0x80070003
When rebuilding the primary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server from the secondary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server data, one of the old recovery points shows databases that were not backed up. To resolve this issue, try to recover that database from another recovery point that might be older or newer.

## <a name="BKMK_SecondaryDPMServer"></a>On a secondary DPM server \(DPM\-DR\), even though incremental and express full jobs happen successfully for a SQL Server database that belongs to a SharePoint farm, recovery points are not displayed in the Recovery task area and no alerts are triggered
In a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] primary server, if you are protecting a SQL Server database that belongs to a SharePoint farm, then ensure that you do not protect that database independently on the secondary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server. To resolve this issue, you must identify all such databases, perform Stop protection with the delete data option, and then re\-protect the SharePoint farm.

## <a name="CheckOutDuringBackup"></a>SharePoint documents checked out or in the recycle bin during backup cannot be restored
In SharePoint, if documents were checked out from the documentation library or were located in the first or second stage of the recycle bin during the time your data was backed up, they cannot be restored. To restore these documents, you must pick a point in time at which the documents were not checked out or in the recycle bin before restoring the data.

## <a name="ProtectionReportIncorrect"></a>DPM Protection Report shows incorrect data for SharePoint farms
[!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] does not calculate the expected number of recovery points correctly in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Protection Report. Therefore the percentage that shows the historical recovery point availability against the existing recovery points is incorrect.

## <a name="WSSProtectionNotWorking"></a>SharePoint protection not working properly
If you are having trouble continuing protection of a SharePoint site that is already part of a protection group after adding a content database, check to see if you have met all the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] prerequisites for protecting Microsoft SQL Server 2005. In the process of adding a content database for protection, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] may implicitly protect the back\-end SQL database without validating the prerequisites.

## <a name="SharePointFailsOnSharedFolder"></a>SharePoint site or item recovery fails when a shared folder is used as a temporary location
When a shared folder is specified as the temporary location for the recovery of a SharePoint site or item the recovery will fail. To resolve this issue, use a local folder as the temporary location for either the recovery farm or the production farm.

## <a name="SharepointprotectionfailswithID30111"></a>SharePoint farm protection fails with ID 30111
If your SharePoint farm protection is failing with the ID 30111 error on the **Jobs** tab in the **Monitoring** pane in [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, it could be because there is a volume with no mount points on the front\-end Web server of your SharePoint farm. To resolve this issue, assign a mount point or drive letter to the dismounted volume and perform a consistency check.

## <a name="BKMK_SharePointIndexBackupsFailDuringProfileInput"></a>SharePoint index backups fail during profile import
Due to constraints in SharePoint, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] cannot pause a profile import. Backups scheduled to run when a profile import is taking place will fail. The backups fail with error code 32010. 
Message: **DPM was unable to get the Content Sources of the SSP <Name of data source>; to a consistent state.**
 Recommended action:

-   Check to see that the protected SSP is online and running.

-   Check to see that the WSSCmdletWrapper DCOM component is configured correctly on the front\-end Web server hosting the protected farm.

-   Retry the operation and make sure no other application or process is trying to resume the crawl of the SSP during backup.

## <a name="BKMK_ConfigureSharePointError997"></a>ConfigureSharepoint.exe fails with error code 997
If this is happening after you have changed the administrator password, do the following to resolve the issue:

1.  From the command prompt, run **dcomcnfg**.

2.  In the DCOM Config utility, search for the WSSCmdletWrapper object. Right\-click the object and select **Properties**.

3.  On the **Identity** tab, enter the new password.


