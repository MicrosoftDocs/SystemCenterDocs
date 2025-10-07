---
title: include file
description: include file that summarizes the release notes for Operations Manager 2019.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 09/02/2020
ms.service: system-center
ms.assetid: 56adc06e-4317-4622-83f2-cc44a5f40c78
ms.subservice: operations-manager
ms.topic: include
---

## Operations Manager 2019 release notes

The following sections summarize the release notes for Operations Manager 2019, and include the known issues and workarounds.
Also see [2019 UR1](#operations-manager-2019-ur1-release-notes) and [2019 UR2](#operations-manager-2019-ur2-release-notes) release notes.

### Health Service with Log on type as *Service* by default

**Description**:
With Operations Manager 2019, *Log on as a Service* feature is enabled by default. This change impacts all the service accounts and Run As accounts; they must have *Log on as a Service* permission.  

**Workaround**: Enable log on as a service permission for these accounts. [Learn more](../scom/enable-service-logon.md).

### User experience changes in maintenance mode

**Description**: The following are the user experience changes with Operations Manager 2019 maintenance mode. These changes are applicable to both Windows and Linux\Unix monitoring:

- As an entity enters the maintenance mode, monitor-based active alerts on it will be automatically resolved. In earlier releases, these alerts get automatically resolved when the entity exits the maintenance mode.

- On-demand monitors and regular monitors now behave similarly when the target entity enters and exits the maintenance mode.

**Workaround**: None.

### Support for x64 components

**Description**:  Operations Manager 2019 supports only x64 components; x86 components aren't supported.
If you try to push install the agent from the console to a x86 computer, the following error message appears:

*The system cannot find the path specified*.

**Workaround**: None.

### Upgrade to reporting server fails the prerequisites check

**Description**: While attempting to do an upgrade of System Center 2016/1801/1807 - Operations Manager reporting server to version 2019, the prerequisites check reports the following error: 

*Management Server Upgraded Check - The management server to which this component reports, has not been upgraded. and the upgrade cannot proceed*.

This error occurs in a distributed management group scenario, where the reporting server is on a server that is different from one or more management servers in the management group.

**Workaround**: Install the System Center 2016/1801/1807 - Operations Manager Operations console on the server that's hosting the reporting server role, and then retry upgrading the reporting server role to version 2019. Once the upgrade is successful, you can uninstall the upgraded Operations console from the reporting server.

### Internet Explorer compatibility view

**Description**: The HTML5 Web console doesn't support Internet Explorer compatibility View.  

**Workaround**: None.

### OpenSSL 1.1.0 version support

**Description**: On Linux platforms, OpenSSL 0.9.8 support is dropped.

**Workaround**: We've added support for OpenSSL 1.1.0.

### Performance monitoring for VMM server fails with Access denied message
**Description**: Service users don't have the permission to access VirtualMachineManager-Server/Operational event log.
**Workaround**: Change the Security Descriptor for operational event log registry with the command below, and then restart event log service and health log service.

```
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WINEVT\Channels\Microsoft-VirtualMachineManager-Server/Operational /v ChannelAccess /t REG_SZ /d O:BAG:SYD:(D;;0xf0007;;;AN)(D;;0xf0007;;;BG)(A;;0xf0007;;;SY)(A;;0x7;;;BA)(A;;0x3;;;NS)(A;;0x1;;;IU)(A;;0x1;;;SU)"
```

This command will add the service user to the list of allowed users who can access VirtualMachineManager-Server/Operational event log.

### Operations Manager 2019 doesn't support HPUX library  

**Description**: Operations Manager 2019 doesn't support HPUX. However, HPUX library is available in the list of management packs delivered for Operations Manager 2019.

**Workaround**: Ignore this. HPUX is removed from the latest pack on the DLC, [here]( https://www.microsoft.com/download/details.aspx?id=58208&WT.mc_id=rss_windows_allproducts).


### Previous AD rules don't work after upgrading to Operations Manager 2019
**Description**:  After you upgrade to Operations Manager 2019 from Operations Manager 2016 (or 2016 URs earlier to UR7), 1801 or 1807, previous AD rules don't work due to the change in Active Directory rules' format. Upgrade to Operations Manager 2019 from Operations Manager 2016 UR7 and UR8 doesn't have this issue.

**Workaround**: To resolve this, use the following steps:

1.	After you upgrade to 2019, export the default management pack to a folder.
2.	Open **Microsoft.SystemCenter.OperationsManager.DefaultUser.xml** from the exported folder.
3.	Rename all the AD rules to use *\<NetBIOS Domain Name of Management Server\>* instead of *\<FQDN of Management Server\>*, example below.

    >[!NOTE]
    > Domain name is case-sensitive.

    **Example**:

    Before: Rule ID="_smx.net_MS1_contoso.com" Enabled="true"

    After: Rule ID="_SMX_MS1_contoso.com" Enabled="true"

4.	Import the updated management pack.

    The rules are now visible on the console.

    For detailed information about this issue, see [update an active directory integration with Operations Manager](https://techcommunity.microsoft.com/t5/system-center-blog/update-on-active-directory-integration-with-scom/ba-p/1226768).

    >[!NOTE]
    >This issue is fixed in 2019 UR2.


### REST API in Operations Manager doesn't return required values for classes

**Description**: When called from Operations Manager 2019, REST API doesn't return className, path and fullname, information returned is empty.
Also, ID is returned as className.

**Workaround**: None.

>[!NOTE]
>This issue is fixed in 2019 UR2.

## Operations Manager 2019 UR1 release notes
The following sections summarize the release notes for Operations Manager 2019 UR1, and include the known issues and workarounds.

For the problems fixed in UR1 and the installation instructions for UR1, [see the KB article](https://support.microsoft.com/help/4533415/update-rollup-1-for-system-center-operations-manager-2019).

### Pending management after patching

**Description**: After you apply the 2019 update rollup (UR1), the agents to be updated aren't listed in **Pending Management** console view.

**Workaround**: You need to identify the agents and update them manually. To do this, go to **Administration**> **Device Management**>**Agent Managed**, and update the agents that are of the older version. To view the correct version of the agent, after applying the management server patch, import the management pack as mentioned in the KB article for Operations Manager 2019 UR1.

### Version display

**Description**: Version display doesn't show **UR1** in areas such  **Help**>**About** and **Device Management** view.

**Workaround**: To check if the Operations Manager components are successfully updated for UR1, see the version number of respective components in **Administration**> **Operations Manager Products**.

### Error while exporting reports post gMSA migration
**Description**: Post migration to gMSA, while exporting a report in Word, PowerPoint, or Excel format, You may encounter the following error:
*An error occurred during rendering the report*.

This is observed for SQL Server Reporting Services on SQL Server 2017. This error appears to be a persistent issue with SSRS in SQL Server 2017.

**Workaround**: To resolve this, use the following steps:

- Grant admin access to *Execution* account on the report server
- Restart the reporting service and wait for 5 minutes
- Try to export the reports again

>[!NOTE]
>
>From SQL Server Reporting Services (SSRS) 2017 version 14.0.600.1274 and later, the default security settings don't allow resource extension uploads. This leads to **ResourceFileFormatNotAllowedException** exceptions in Operations Manager during the deployment of reporting components.
>
>To fix this, open SQL Management Studio, connect to your Reporting Services instance, open **Properties**>**Advanced**, and add \*.\* to the list for *AllowedResourceExtensionsForUpload*. Alternatively, you can add the full list of Operations Manager's reporting extensions to the *allow list* in SSRS.

### Replacement of previously used service accounts with gMSA fails

**Description**:  Replacement of previously used Operation Manager's service accounts with gMSA fails, leading to Operations Manager's console issues (Console fails to open). This occurs if the data access service isn't initialized.

**Workaround**:

1.	Add the account running the SDK service to *builtin\Windows Authorization Access Group*.

2.	Run the PowerShell script as detailed [here](https://support.microsoft.com/help/4519161/operations-manager-2019-and-1807-reports-fail-to-deploy).

3. If this is a fresh installation of Operations Manager, wait for 24 hours, and then apply the Update Rollup. This is applicable to all the roles in Operations Manager.

>[!NOTE]
> Ensure that DW and DR accounts are members of the Operations Manager Report Security Administrators group, so the issue doesn't recur. For more information, see [gMSA accounts](../scom/support-group-managed-service-accounts.md).

## Operations Manager 2019 UR2 release notes
No known issues in Operations Manager 2019 UR2.

For the problems fixed in UR2 and the installation instructions for UR2, [see the KB article](https://support.microsoft.com/help/4558752).


## Operations Manager 2019 UR4 release notes
The following sections summarize the release notes for Operations Manager 2019 UR4, and include the known issues and workarounds.

For the problems fixed in UR4 and the installation instructions for UR4, see [the KB article](https://support.microsoft.com/topic/update-rollup-4-for-system-center-operations-manager-2019-07ad0ef3-a330-4373-92f6-2dda3821bee5).

### Three columns in Authoring > Groups aren't localized

**Description**: In Operations Manager console **Authoring** > **Groups** new columns (**Management Pack**, **Sealed** and **Members**) appear in English, not displayed in the language as set in the computer accessing this view. 

**Workaround**: None.

## Operations Manager 2019 UR5 release notes
The following section summarizes the release notes for Operations Manager 2019 UR5, and includes the known issues and workarounds.

For the problems fixed in UR5 and the installation instructions for UR5, see [the KB article](https://support.microsoft.com/topic/788c571b-1887-4376-8b2f-c7881e797835).

### Web console security vulnerabilities

>[!NOTE]
> Ensure to take the backup of *Web.config* files before you apply this update rollup.

**Description**: Operations Manager 2019 Web console has security vulnerabilities.

**Workaround**: With Operations Manager 2019 UR5, several Web console security vulnerabilities are fixed. Because of these fixes, the *Web.config* files of both `HTMLDashboard` and `MonitoringView` web apps will be replaced. Any earlier settings of these apps will be lost, and you will need to redo the changes.
