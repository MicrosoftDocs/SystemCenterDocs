---
title: Set up tape library sharing
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5eab83e-716d-4f5c-ad5f-e2c2ffc13530
---
# Set up tape library sharing
A tape library is typical a collection of tape drives that automatically mount and dismount tape media. You can share a single tape library across multiple DPM servers.

DPM can act as a tape library server or a tape library client. DPM acting as a library server has the medium changer enabled and the server library\-sharing command has been run. DPM acting as a library client doesn’t have the medium changer enabled and the client library\-sharing commands have been run. The following diagram shows the topology of a shared library.

![](/Image/dpm_LibrarySharingTopology_c.png)

Note the following before you start:

-   The tape library must be in a fibre channel storage area network \(SAN\) environment, or be a iSCSI attached so that all DPM servers that participate in library sharing have direct access to the tape drives in the library.

-   All [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] servers using a shared library must use a similar SQL Server instance for hosting [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] databases. For example, they should all use a local instance or a remote instance. You can’t have a mixture of local and remote. DPM doesn’t support sharing tape library between different DPM versions.

-   We recommend that the system configuration of the library server computer and all library client computers be as similar as possible.

-   All DPM servers sharing a tape library should be running the same version of DPM the same operating system, and the same service packs and updates.

## Set up library sharing

1.  On all DPM servers check that the SQL Server \(MSDPM2012\) and the SQL Server agent \(MSDPM2012\) services use a domain account for logon and not a local account \(default setting\). The domain account should be a member of the local Administrator group.

2.  Enable the Named Pipes protocol for the SQL Server instances on the library server and client. Then restart the SQL Server service.

3.  On the library server, enable the medium changer in Device Manager.

4.  On the library client, check that the medium changer is not enabled. Check that tape drive devices are visible and enabled.

5.  To configure DPM servers to use a shared library run the following commands on the DPM library server:

    1.  On the library server computer, run the following commands from an elevated command prompt. Run the commands for each library client. For example if three library clients are supported then run the commands three times.

        **cd  *<system drive>*:\\Program Files\\Microsoft  System Center 2012 R2\\DPM\\DPM\\Setup**

        **AddLibraryServerForDpm.exe – ShareLibraryWithDpm**
         ***<FQDN of library client>***

    2.  Close the DPM console on each library client.

6.  On each DPM library client do the following:

    1.  On the library client run the following commands from an elevated command prompt. Don’t run these commands on the library server.

    2.  **cd *<system drive>*:\\Program Files\\Microsoft  System Center 2012 R2\\DPM\\DPM\\Setup**

        **AddLibraryServerForDpm.exe –DpmServerWithLibrary*<FQDN of library server>***

        **SetSharedDpmDatabase \-DatabaseName <SqlServer\\Instance\\DatabaseName>**, where DatabaseName is the name of the library server. You can find and copy this information in the About DPM window next to the **DPM’s SQL Server**: entry.

7.  In DPM Administrator Console on the library server, perform a rescan, and then perform a rescan or refresh on each library client computer.

    The quickest way to see all media on all of the DPM servers is to perform a rescan on each, followed by a detailed inventory. Next, on any one of the servers, mark a number of media as free, and then perform a refresh on the other servers.

    After a piece of media is claimed and written to by a DPM library client it’s exclusively owned by that DPM server for all future backup jobs until that media is manually marked as free on the DPM server that owns it. After it’s marked as free, other client DPM servers can claim it for backup jobs.

After you’ve configured library sharing, you can use the shared tape library as if it were attached to each DPM server.

## Turn on auto\-refresh for the DPM server
You can set the auto\-refresh interval for the library by using the **Set\-DPMGlobalProperty** cmdlet in DPM Management Shell. The syntax for the cmdlet is as follows:

`Set-DPMGlobalProperty -DPMServerName`*<DPMServerName>* `-LibraryRefreshInterval`*<LibraryRefreshInterval>*

where *<DPMServerName>* is the computer name of the DPM server and *<LibraryRefreshInterval>* is the time interval in minutes.

You must set **LibraryRefreshInterval** to a value greater than or equal to five. If you set it to less than five it will automatically be reset to zero and the refresh won’t happen.

After you’ve run the **Set\-DPMGlobalProperty** cmdlet, close and reopen the DPM Administrator Console to apply the auto\-refresh settings.

## Promote a different DPM server to act as the library server
If the library server fails, DPM detects the failure and raises an alert. All tape jobs scheduled to run fail while the library server is down. DPM checks at 20 minute intervals to see if the library server is working again. If you can’t resolve a problem on the library server, or do not want to wait for the library server to come back online, you can promote another DPM server as the library server as follows:

1.  On each library client computer run the following commands from an elevated command prompt:

    **cd *<system drive>*:\\Program Files\\Microsoft  System Center 2012 R2\\DPM\\DPM\\Setup**

    **SetSharedDpmDatabase.exe –RemoveDatabaseSharing**

    **AddLibraryServerForDpm.exe –DpmServerWithLibrary**
     ***<FQDN of the library server>* \-remove**

    Check that the DPM Administrator Console is running as expected on each library client.

2.  On the computer that you want to promote as the new library server, do the following:

    1.  Enable the medium changer in Device Manager.

    2.  On the computer that you want to promote as the new library server, open an elevated Command Prompt window, and then run the following commands one time for each of the library client computers:

        **cd *<system drive>*:\\Program Files\\Microsoft  System Center 2012 R2\\DPM\\DPM\\Setup**

        **AddLibraryServerForDpm.exe –ShareLibraryWithDPM**
         ***<FQDN of client library>***

        where *<FQDN of client library>* is the fully qualified domain name of the library client.

3.  On each library client run the following commands from an elevated command prompt:

    1.  **cd *<system drive>*:\\Program Files\\Microsoft  System Center 2012 R2\\DPM\\Setup**

        SetSharedDpmDatabase \-DatabaseName <**SqlServer\\Instance\\DatabaseName**> \[\-DoNotMoveData\]

        where *<SQLServer\\Instance\\Databasename>* is the database name of the library server.


