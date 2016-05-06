---
title: Release Notes for System Center 2012 - Orchestrator
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3687f14-8ecf-4d92-81d8-c024c90cb436
---
# Release Notes for System Center 2012 - Orchestrator
These release notes contain information that is required to successfully install [!INCLUDE[orchlong](./Token/orchlong_md.md)]. They contain information that is not available in the product documentation.

Before you install and use [!INCLUDE[orchshort](./Token/orchshort_md.md)], read these release notes. These release notes apply to [!INCLUDE[orchlong](./Token/orchlong_md.md)].

If you are looking for the Release Notes for [!INCLUDE[orchshort](./Token/orchshort_md.md)] in [!INCLUDE[sc2012sp1_long](./Token/sc2012sp1_long_md.md)], see [Release Notes for Orchestrator in System Center 2012 SP1](./Release-Notes-for-Orchestrator-in-System-Center-2012-SP1.md).

## <a name="Deployment"></a>Known Issues

### You receive a database validation error when you use a remote computer that is running SQL Server
**Description:** If you are using a remote computer that is running Microsoft SQL Server and that server has named pipes enabled \(as opposed to TCP\/IP\), you cannot successfully install [!INCLUDE[orchshort](./Token/orchshort_md.md)]. Instead, you receive a database validation error during the last phase of installation.

**Workaround:** Enable TCP\/IP for any [!INCLUDE[orchshort](./Token/orchshort_md.md)] installations that use a remote computer that is running SQL Server.

### You must uninstall older versions of [!INCLUDE[orchshort](./Token/orchshort_md.md)] before you install the [!INCLUDE[orchlong](./Token/orchlong_md.md)] runbook server
**Description:** If you try to install or deploy a [!INCLUDE[orchlong](./Token/orchlong_md.md)] runbook server on a computer that has the Opalis Action Server, the [!INCLUDE[orchshort](./Token/orchshort_md.md)] 2012 Beta, or the [!INCLUDE[orchshort](./Token/orchshort_md.md)] 2012 Release Candidate runbook server installed, it leaves the runbook server in an unusable state. You must revert the deployment of the previous version by using the **Deployment Manager**, or in Control Panel, uninstall it by using **Programs and Features** before you install the new version.

You must also manually remove the OpalisRemotingService executable program by using the following procedure:

##### To remove the OpalisRemotingService

1.  Open a command prompt with administrative credentials.

2.  Stop the service by entering the command **sc stop OpalisRemotingService**.

3.  Remove the service by entering the command **sc delete OpalisRemotingService**.

4.  Navigate to C:\\Windows\\SysWOW64.

5.  Delete the file OpalisRemotingService.exe.

### The [!INCLUDE[orchshort](./Token/orchshort_md.md)] setup wizard may crash on an unsupported operating system
**Description:** If you run the [!INCLUDE[orchshort](./Token/orchshort_md.md)] setup wizard on an unsupported operating system, then you may receive an unexpected error message or system crash.

**Workaround:** See [System Requirements](assetId:///aabe0348-a207-46e4-87df-24aa993df984) for details on operating systems supported by [!INCLUDE[orchshort](./Token/orchshort_md.md)].

### The computer restarts after you deploy Runbook Designer
**Description:** When you deploy a Runbook Designer to localhost through the Deployment Manager, the computer will restart.

**Workaround:** None.

### Authorization cache performance
**Description:** In the Release Candidate for System Center 2012 \- Orchestrator, permission changes to runbooks and runbook folders were immediately propagated to the [!INCLUDE[orchshort](./Token/orchshort_md.md)] web service and the Orchestration console. If you added, imported, or deleted a runbook or a runbook folder, or changed the permissions on a runbook or runbook folder from the Runbook Designer, the changes were immediately visible in the Orchestration console.

The authorization cache table is included in the release version of [!INCLUDE[orchshort](./Token/orchshort_md.md)]. This table is cleared and [!INCLUDE[orchshort](./Token/orchshort_md.md)] re\-computes the permissions every 10 minutes. You cannot view any runbook or runbook folder changes until the cache is refreshed. After 10 minutes, you can refresh the Orchestration console and see the changes.

**Workaround:** It is not recommended to reduce the refresh interval of the authorization cache table because of the time required to re\-compute the cache. If you require assistance in modifying the refresh interval of the authorization cache table, please contact customer support.

### Certain automatic log purge settings do not work
**Description:** When you select **Purge the logs** from the **Log History** tab of a runbook, all of the logs for that runbook are deleted.The automatic log purge that occurs daily and that can be triggered manually by right clicking on the **Server** in the **Connection** pane generates an error. If you configure the **Log Purge Options** to **Keep most recent entries**, an error occurs and the log purge does not occur.  If the error occurs during the scheduled daily log purge, the error is written to log history.

**Workaround:** Use the **If the number of entries exceeds X delete the entries older than Y** option.

### Certain log purge settings for runbooks may not work
**Description:** In some scenarios, log purge settings do not work. This occurs most commonly when you use the Invoke Runbook activity.

The following settings are affected:

-   **Keep Last X entries**

    [!INCLUDE[orchshort](./Token/orchshort_md.md)] cannot determine the relationship between Id and ParentId so the setting fails when you try to delete an Id that is also a ParentId.

-   **Keep entries for last X days**

    [!INCLUDE[orchshort](./Token/orchshort_md.md)] cannot determine the relationship between Id and ParentId so the setting fails when you try to delete an Id that is also a ParentId.

-   **If number of entries exceed X, delete entries older than Y days**

    The current behavior for this setting is identical to **If total number of entries is greater than X, delete entries older than Y days**.

**Workaround:** None.

### Standard date\/time variable format is yyyy\-MM\-ddTHH:mm:ss
**Description:** The standard date\/time format used by [!INCLUDE[orchshort](./Token/orchshort_md.md)] is a 24\-hour time format displayed as yyyy\-MM\-ddTHH:mm:ss. This date\/time format conforms with ISO 8601.

> [!IMPORTANT]
> The variable string for the date\/time format is case sensitive. If you use yyyy\-MM\-ddThh:mm:ss as the variable string, the wrong date\/time is output.

**Workaround**: Use the format yyyy\-MM\-ddTHH:mm:ss.

### The date\/time format displayed in a property textbox is not always displayed in the locale\-specific format
**Description:** Changes to the formatting of the date\/time string can cause the date\/time format in a property textbox to use a different format from the locale\-specific format.

This occurs because an [!INCLUDE[orchshort](./Token/orchshort_md.md)] deployment can have a span of control that crosses different locales. You can choose to display dates using your locale\-specific format. However, internally, [!INCLUDE[orchshort](./Token/orchshort_md.md)] uses a static format to ensure that the proper dates and times are used for activity property values.

The standard date\/time format used by [!INCLUDE[orchshort](./Token/orchshort_md.md)] is a 24\-hour time format displayed as yyyy\-MM\-ddTHH:mm:ss. This date\/time format conforms with ISO 8601.

**Example**: You set your formatting to United Kingdom with a date format of DD\/MM\/YY. When you click the ellipsis button next to a date\/time property in an activity, the date displayed is in DD\/MM\/YY format. When you click **OK** to save your changes, the date\/time information displayed in the property is in the format YYYY\-MM\-DDTHH:MM:SS.

**Workaround**: If you have a runbook that contains activity properties configured with the older date\/time formatting of MM\/DD\/YYYY HH:MM:SS AM, [!INCLUDE[orchshort](./Token/orchshort_md.md)] uses the old format. The runbook is properly interpreted by [!INCLUDE[orchshort](./Token/orchshort_md.md)] when the activity runs. If you change a property from the default date\/time format, the date\/time format changes to the new format.

### Use UTC time when you filter on published date\/time
**Description:** In your runbook workflow, use **Activity end time UTC** instead of **Activity end time** to filter on events. **Activity end time UTC** is the uniform time across your entire [!INCLUDE[orchshort](./Token/orchshort_md.md)] deployment. **Activity end time** represents the local time of the management server.

The standard date\/time format used by [!INCLUDE[orchshort](./Token/orchshort_md.md)] is a 24\-hour time format displayed as yyyy\-MM\-ddTHH:mm:ss. This date\/time format conforms with ISO 8601.

**Workaround:** None.

### Registration of an integration pack fails if you first attempt to register an Opalis 6.3 integration pack
**Description:** If you attempt to register an Integration Pack for Opalis 6.3, you get an unexpected failure because these integration packs are not supported in [!INCLUDE[orchlong](./Token/orchlong_md.md)]. If you then attempt to register a valid integration pack for [!INCLUDE[orchlong](./Token/orchlong_md.md)], you receive the same error.

**Workaround:** You must close and restart Deployment Manager before registering a valid [!INCLUDE[orchlong](./Token/orchlong_md.md)] integration pack.

### An integration pack must be registered and deployed before importing a runbook that uses it.
**Description:** If you import a runbook that uses an activity from an integration pack that is not registered and deployed, the activities from that integration pack will be marked with a question mark \(?\). Even after the integration pack is installed and registered, the activities will not work correctly.

**Workaround**: Import the runbook again after the integration pack is deployed and registered.

### Different date\/time formats between versions of integration packs
**Description:** The release candidate versions of integration packs for System Center 2012 use a different format for date\/time published data values than the format used by the released version of integration packs for System Center 2012. Normally, you do not encounter this difference since it is only an issue if you subscribe to a date\/time value property of a release candidate version of a System Center integration pack activity.

**Workaround:** If you encounter problems with date\/time properties published with the System Center 2012 integration packs, use the [Format Date and Time](./Format-Date-and-Time.md) activity to translate between the two formats. The [Format Date and Time](./Format-Date-and-Time.md) activity has a **Details** pane with an **Input** section and **Output** section where you can specify a date format. You can enter an input and output format based on your translation requirements.

The formats are as follows:

-   System Center 2012 Orchestrator integration packs for System Center 2012 Components RC:  yyyy\-MM\-ddThh:mm:ss

-   System Center 2012 integration packs for pre\-System Center 2012 Products RC: M\/d\/yyyy h:m:s tt

### [!INCLUDE[om12long](./Token/om12long_md.md)] integration pack

#### ManagementGroup and ManagementGroupId filters
**Description:** The ManagementGroup and ManagementGroupId filters in the [Get Alert \[Orch12\_IP\_SCOM12\]](assetId:///8ceb9a9d-2b32-4898-9c3a-351d9f4a6b68) and [Monitor Alert \[Orch12\_IP\_SCOM12\]](assetId:///7964ad52-92dc-4733-9b86-0edb28fd9750) activities do not work.

**Workaround:** None.

## See Also
[Orchestrator_1](./Orchestrator_1.md)


