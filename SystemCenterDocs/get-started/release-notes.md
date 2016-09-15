---
description: Release Notes for System Center 2016
manager:  cfreemanwa
ms.topic:  article
author:  cfreemanwa
ms.prod:  system-center-threshold
keywords:
ms.date:  2016-08-30
title:  Release Notes for System Center 2016
ms.assetid:  5fad5608-4cb7-48b0-aa31-35ca5cc2d560
---

# Release Notes for System Center 2016

>Applies To: System Center 2016

**The following set of notes lists known issues and steps to mitigate the issue. These notes only apply to System Center 2016.**


## System Center 2016 - Data Protection Manager Release Notes

The following release notes apply to System Center 2016 - Data Protection Manager.


#### Silent Installation of System Center DPM with SQL Server 2008
**Description**: You cannot silently install DPM 2016 RTM on SQL Server 2008.

**Workaround**: Deploy DPM 2016 RTM on a version of SQL Server higher than 2008, or use the DPM 2016 Setup wizard to install SQL Server.

#### Hyper-V VMs are protected twice on VM upgrade
**Description**: If you upgrade your Hyper-V VM from Windows Server 2012 R2 to Windows Server 2016 to enable Resilient Change Tracking (RCT), a new VM representing the upgraded VM may appear in the **Create Protection Group Wizard**. The 2016 version of the VM may appear in addition to the 2012 R2 version of the VM.

**Workaround**: For the VMs that have not been upgraded, stop protection with **Retain Data**. After upgrading the VM, create a new protection group, Then, refresh the data sources and protect the VMs. This protects the VMs using Resilient Change Tracking (RCT).

#### Agent installation fails on Windows Server 2008, Windows Server 2008 R2
**Description**: If you are trying to protect Windows Server 2008, or Windows Server 2008 R2, agent installation may fail.

**Workaround**: Upgrade the Windows Management Framework (WMF) on the production server to 4.0. Download the WMF from [https://www.microsoft.com/en-in/download/details.aspx?id=40855](https://www.microsoft.com/en-in/download/details.aspx?id=40855). Install WMF and then install the agent.

#### Restoring a previous version of an upgraded Hyper-V VM causes future recovery points to fail.

**Description**: If you upgrade a protected 2012 R2 Hyper-V VM to the 2016 version, then stop protecting the VM (but retain data), and then re-enable protection if you then recover a 2012 R2 copy at the original location, further backups may fail.

**Workaround**: To prevent future backups from failing, after creating a 2012 R2 recovery point for a 2016 VM, change the version of the recovery point to 2016 and run consistency check before the next scheduled backup.


#### Adding DPM Volumes without Drive Letters
**Description:** If you try to add a volume without access path/drive letter as valid volumes to storage, DPM does not add them, throwing an error.

**Work around:** Assign drive letters to the volumes that are being added to DPM Storage.

#### Rescan of large-scale storage configurations
**Description:** For large-scale storage configurations, if you use the Disks Storage, Rescan feature to detect new volumes, the DPM UI may appear to "hang" while it is re-scanning.

**Work around:** Wait for the scan to complete. If required, you can open another instance of the Administrator Console while the first instance completes rescanning for new volumes.

#### Secondary Protection of SQL DB with high Synchronization Frequency
**Description:** If a SQL Database is protected by a primary and secondary DPM server with a high synchronization frequency (for example, primary = 15 mins, secondary = 1 hour), the backup jobs may fail with the following warning: <br/>
On the Primary DPM Server: The job completed successfully with the following warning: The storage involving the current operation could not be read from or written to. (ID 40003) <br/>
On the Secondary DPM Server: The job completed successfully with the following warning: The synchronization job failed due to an internal error. (ID 117)


**Workaround:** When no job is running on the primary DPM server, stop the msdpm service by running the following command from the command line with Admistrator privileges:

```
net stop msdpm
```

Then delete the file in the folder:
*DPM_install_path*\DPM\Config\VolumeManagerState_*DPMServerName*


#### Consistency Checks on Upgrade of Primary and Secondary DPM Servers to DPM 2016
**Description:** After upgrading a primary and secondary DPM server from Data Protection Manager 2012 R2 to System Center Data Protection Manager 2016, consistency check jobs fail on the secondary DPM.

**Workaround:** During the process of creating or modifying a Protection Group on the secondary DPM server, on the **Select Group Members** screen, select the Primary DPM Server and click **Refresh**. After this, consistency check jobs will succeed.

#### Searching for Files or Folders during the Recovery process doesn't return expected results
**Description:** If you **Search** for a file, folder, or volume in the recovery pane under **Files and Folders**, you may not get the relevant results.

**Workaround:** Use the **Browse** feature instead of **Search** to find the file, folder, or volume.

#### Protecting Hyper-V VMs with an ISO in DVD Drive
**Description:** If you protect a Hyper-V VM with an ISO in the DVD drive, backups may fail with the following messages:

During initial replication: <br/>
`
DPM failed to communicate with [DPMServerName] because of a communication error with the protection agent. (ID 53 Details: Not implemented (0x80000001))
`

During subsequent backups: <br/>
`
An unexpected error occurred while the job was running. (ID 104 Details: Internal error code: 0x80990E54)
`

**Workaround:** Eject the ISO and trigger the backup process again.

#### Deleting Storage Volumes with backups
**Description:** If the backups of a data source are stored on a volume, and the volume is deleted, the Protection Group goes into an error state.

**Workaround:** To fix the error state, use Delete Data to stop protection on the affected data sources, then protect the data source again.

#### Concurrent Incremental and Tape Backups
**Description:** If you create a policy that triggers synchronization and tape backup jobs at the same time on the same data source, tape backup jobs may fail sometimes.

**Workaround:** If the tape backup jobs fail, retry the tape backup. To avoid this scenario, configure the backup policy so that incremental and tape backups don’t conflict.

#### Bare Metal Recovery protection failures

**Description:** If you configure Bare Metal Recovery (BMR) protection, the BMR protection job may fail with the message that the replica size is not sufficiently large.

**Workaround:** Use PowerShell to increase the replica size:
```
$dpm = Connect-DPMServer -DpmServerName <name of DPM>
$pg = Get-DPMProtectionGroup -DpmServerName <name of DPM>
$ds = Get-DPMDatasource -ProtectionGroup $pg[0] # choose the right PG here
$ds1 = $ds[0] # choose the right DS here
$dpm.Proxy.ResizeReplica($ds1.DatasourceId, $ds1.ReplicaSize * 2)
```


#### Re-protecting DPM DB after Upgrade to DPM 2016
**Description:** When you upgrade from System Center DPM 2012 R2 to System Center Data Protection Manager 2016, the DPM database name can change in some scenarios.

**Workaround:** To prevent a potentially renamed database from impacting protection, if you are protecting the DPM 2012 R2 database, be sure to enable protection for the DPM 2016 database. Once you have upgraded DPM and have validated protection works correctly, you can remove protection for the DPM 2012 R2 database.

#### Recovering a database of DPM Servers after upgrading to 2016 from Azure
**Description:** If your DPM installation's SQL server master database is backed up to Azure, and you upgrade to System Center DPM 2016, and then attempt to restore using an online recovery point, the recovery job will fail.

**Workaround:** To recover the master SQL database, you must use SQL Server to recover the database as files.

#### Incorrect Space Usage Reported
**Description:** Incorrect Space Usage Reported

**Workaround:** There is no workaround for this. Overall space usage can found from the filesystem directly.

#### DPMSync fails after deletion or corruption of Modern DPM Storage Folders
**Description:** If the Modern DPM Storage folders are deleted or corrupted, running DPMSync.exe with **ReallocateReplica** fails with the following error:

`
The storage involving the current operation could not be read from or written to.
`

**Workaround:** There is no workaround.

#### Excluded Hyper-V VHDs continue to be protected
**Description:** While protecting Hyper-V VMs, the excluded VHDs continue to be protected.

**Workaround:** None.



## System Center 2016 - Operations Manager Release Notes
**The following release notes apply to System Center 2016 - Operations Manager.**

#### SharePoint integration with Operations Manager has to be recreated
**Description:** While using SharePoint to view Operations Manager data, the existing Web Console Dashboard URLs provided will not work and these Web parts have to be recreated with the below steps.

**Workaround:** Follow the below steps to setup SharePoint to view Operations manager data:
1.	Create a new page on SharePoint in which you want to display the Dashboard.
2.	Open the page and click edit and insert a new Web Part.
3.	In Web Part, under categories select “Media and Content” and under that select “Page Viewer” and click add.
4.	Edit the Web Part and select Web Page and enter the URL of the SCOM Web Console dashboard.
5.	Append “&disabletree=true” at the end of the dashboard URL for disabling the tree view getting displayed on the SharePoint page
6.	Configure the appearance, layout, and Advance attribute of the SharePoint page.


#### In Web Console, Windows Computer Tasks is not displayed sometimes
**Description:** In Web Console, when you go to Windows computers view and select a computer, the tasks pane may not display Windows computer tasks.
Likelihood of occurrence: Medium

**Workaround:** None.

#### In Web Console, Navigation view is not displayed in the tasks pane for state views
Description:  In Web Console, when you go to State View and select an entity in the list, the tasks pane does not display the Navigation View section of the selected entity.

**Workaround:** None.

#### In Web Console, functionality in My Workspace tab does not work .
**Description:** In Web Console, none of the links/views in My Workspace tab work.

**Workaround:** None.

#### Web Console might not work due to IIS becoming corrupt
**Description:** Web Console might throw an error **“Could not load type ‘System.ServiceModel.Activation.HttpModule”**.

**Workaround:** Add “HTTP Activation” to the role services of the OS.  Then,
On Server 2008 R2 – run the following in an elevated CMD:  “C:\Windows\Microsoft.NET\Framework64\v4.0.30319>aspnet_regiis.exe -i -enable”.
On Server 2012 – run the following in an elevated CMD:  “C:\Windows\Microsoft.NET\Framework64\v4.0.30319>aspnet_regiis.exe -r”.

#### Anomalies in handling tables and bullets in the Knowledge Articles
**Description:** If the tables are inserted in the knowledge article then while re-editing the knowledge article the borders are not applied to the table. Similarly, if bullets are added in the knowledge article it gets converted to numeric bullets while re-editing. And, if there is a single bullet in the article then the article doesn’t gets saved in the MP and the console throws error.

**Workaround:** None.

#### MSI based installation does not work for Nano agent
**Description:** MSI based installation is not supported for Nano agent. The agent can be installed from discovery wizard\PowerShell installer scripts.

**Workaround:** None.

#### Issues with uninstallation of Nano agent
**Description:** Uninstalling an update to Nano agent is not possible.

**Workaround** Only option is to uninstall the Nano-agent, then install the RTM version + desired update.

#### Issues with updates of Nano agent
**Description:** Updates to Nano agent will not be pushed from WU. To update Nano-agent you
Will need to either download the available updates and install using the PowerShell update scripts; or trigger a repair from an updated Management server.

**Workaround:** None.


#### Unable to override the path or folder for Nano agent installation
**Description:** Nano agent is always installed to the agent folder: ‘%SystemDrive%\Program Files\Microsoft Monitoring Agent’, the agent installation folder cannot be overridden.

**Workaround:** None.

#### Inconsistencies in push install experience of Nano agent
**Description:** Push install: the status dialog (which shows that installation in progress etc.) closes but agent stays in pending state in console for some time till installation fails\passes. Installation may fail, and log file will need to be checked for the same.

**Workaround:** None.

#### Inconsistencies in push uninstall experience of Nano agent
**Description:** Push uninstall: the status dialog (which shows that uninstallation in progress\completed) shows uninstall success for Nano-agent, but agent uninstalls only after sometime. Uninstallation may fail, and log file will need to checked for same.

**Workaround:** None.

#### ACS is not working for Nano agent
**Description:** ACS is not working for Nano agent, in all the cases. There are issues in certain scenarios.

**Workaround:** None.

#### Client-side monitoring (CSM) alerts might stop flowing from the System Center Operations Manager management server host
**Description:** The update sequence of System Center Operation Manager management server may cause an issue with the client-side monitoring alerts collection from the management server host. System Center Operations Manager agents are not affected. Likelihood of occurrence: Medium.

**Workaround:** Restart the "Microsoft Monitoring Agent" service on System Center Operations Manager management server host.

#### After updating System Center Operations Manager server or agent, Application performance monitoring (APM) events, client-side monitoring (CSM) events, and APM alerts might stop flowing from the monitored hosts
**Description:** The update sequence of System Center Operations Manager agent may cause an issue with the following:

•	Client-side monitoring (CSM) events and alerts collected on the host.

•	Application Performance Monitoring (APM) events and alerts collected on the host.
System Center Operations Manager management server is not affected.


**Workaround:** Restart the "Microsoft Monitoring Agent" service on the System Center Operations Manager agent host that is experiencing the issue.

#### Application performance monitoring (APM) for Windows services is not supported in System Center - Operations Manager on hosts where Application Insights Status Monitor is installed.
**Description:** Application performance monitoring (APM) workflow fails to process monitoring configuration for .NET Windows services on the hosts if Application Insights Status Monitor and the System Center - Operations Manager agent are both installed.

**Workaround:** Uninstall Application Insights Status Monitor.

#### Namespace values for performance tracking will be ignored
**Description:** Setting the Namespace value for performance tracking when tracking a custom namespace in .NET Applications Performance Monitoring (APM) will be ignored.

**Workaround:** Set both the exception tracking and performance tracking settings to include the same custom namespaces.

#### Using sudo elevation with Solaris operating systems requires a configuration change if sudo executable is not in an expected path
**Description:** If you want to use sudo elevation on a computer running Solaris, and the sudo executable is not in an expected path, you need to create a link to the correct path. Operations Manager will look for the sudo executable in the path /opt/sfw/bin, and then in the path /usr/bin. If sudo is not installed in one of these paths, a link is required.

**Workaround:** The UNIX and Linux agent installation script creates the symbolic link /etc/opt/Microsoft/scx/conf/sudodir to the folder expected to contain sudo. The agent uses this symbolic link to access sudo. The installation script automatically creates the symbolic link, so no action is needed for standard UNIX and Linux configurations. However if sudo is installed in a non-standard location, you should change the symbolic link to point to the folder where sudo is installed. If you change the symbolic link, its value is maintained for uninstall, re-installation, and upgrade operations with the agent.

#### Operations Manager Console will stop responding if you attempt to resolve a dependency while  importing a Management Pack
**Description:** When you click **Import Management Packs** from the Administration section of the Operations Manager console, the console will display the **Resolve** button if the Management Pack is dependent on another Management Pack. If you click  Resolve you will see the **Dependency Warning**. If you click the **Resolve** button in the warning the Operations Manager console will stop responding.

**Workaround:** Install the Update for System Center 2016 - Operations Manager. See the Knowledge Base article [3117586](https://support.microsoft.com/en-us/kb/3117586) for specific instructions.

#### Client-side monitoring (CSM) alerts might stop flowing from the System Center Operations Manager management server host
**Description:**The update sequence of System Center Operation Manager management server may cause an issue with the client-side monitoring alerts collection from the management server host. System Center Operations Manager agents are not affected.
Likelihood of occurrence: Medium

**Workaround:** Restart the "Microsoft Monitoring Agent" service on System Center Operations Manager management server host.

#### Application performance monitoring (APM) events, client-side monitoring (CSM) events, and application performance monitoring (APM) alerts might stop flowing from the System Center Operations Manager agent hosts
Description:  The update sequence of System Center Operations Manager agent may cause an issue with the following:

-   Client-side monitoring (CSM) events and alerts collected on the host.

-   Application Performance Monitoring (APM) events and alerts collected on the host.

System Center Operations Manager management server is not affected.

**Workaround:** Restart the "Microsoft Monitoring Agent" service on the System Center Operations Manager agent host that is experiencing the issue.

#### Application performance monitoring (APM) for Windows services is not supported in System Center - Operations Manager on hosts where Application Insights Status Monitor is installed.
**Description:** Application performance monitoring (APM) workflow fails to process monitoring configuration for .NET Windows services on the hosts if Application Insights Status Monitor and the System Center - Operations Manager agent are both installed.

**Workaround:** Uninstall Application Insights Status Monitor.

#### Telemetry data may be erroneously sent when the "Usage and Connectivity Data" setting is set to "False"
**Description:**If two operators have Operations Manager consoles open and one sets the Usage and Connectivity Data setting to "Do not send data" data may continue to flow to Microsoft until the second user closes and reopens their instance of the Operations manager console.

**Workaround:** Restart all Operations Manager console sessions after making changes to the Usage and Connectivity setting.

**Description:**When a new component such as a management server or gateway server are added to an existing SCOM environment, usage information about the setup process is sent to Microsoft even though the Usage and Connectivity Data setting is set to "Do not send data". After the component is added, no further usage data will be sent to Microsoft from the component.

**Workaround:** None

#### Using sudo elevation with Solaris operating systems requires a configuration change if sudo executable is not in an expected path
**Description:** If you want to use sudo elevation on a computer running Solaris, and the sudo executable is not in an expected path, you need to create a link to the correct path. Operations Manager will look for the sudo executable in the path /opt/sfw/bin, and then in the path /usr/bin. If sudo is not installed in one of these paths, a link is required.

**Workaround:** The UNIX and Linux agent installation script creates the symbolic link /etc/opt/Microsoft/scx/conf/sudodir to the folder expected to contain sudo. The agent uses this symbolic link to access sudo. The installation script automatically creates the symbolic link, so no action is needed for standard UNIX and Linux configurations. However if sudo is installed in a non-standard location, you should change the symbolic link to point to the folder where sudo is installed. If you change the symbolic link, its value is maintained for uninstall, re-installation, and upgrade operations with the agent.

#### Namespace values for performance tracking will be ignored
**Description:** Setting the Namespace value for performance tracking when tracking a custom namespace in .NET Applications Performance Monitoring (APM) will be ignored.

**Workaround:** Set both the exception tracking and performance tracking settings to include the same custom namespaces.

#### Operations Manager web console is not compatible with Microsoft Edge web browser
**Description:** When you open the Operations Manager web console from the Windows 10Start Menu the console will open in the Microsoft Edge web browser. This will result in an error.

**Work around:** Open the Operations Manager web console with Internet Explorer. Internet Explorer is available from  Windows Accessories sub-menu.

#### Launching the Operations Manager Web Console may result in a blank screen
**Description:** When you first open the Operations Manager web console you may encounter a blank screen.

**Work around:** To resolve the issue:

1. Click on "Configure" button.
2. When prompted to Run or Save SilverlightClientConfiguration.exe, click Save.
3. Run SilverlightClientConfiguration.exe.
4. Open the file properties of exe (right-click) and open the Digital Signatures tab.
5. Select the certificate with Digest Algorithm as sha256 and click on Details.
6. In the Digital Signature Details dialog box, Click on View Certificate.
7. In the dialog box which appears next, click on Install Certificate.
8. In the Certificate Import Wizard, Set store location as - Local Machine. Click Next.
9. Select the option - "Place all certificates in the following store" Browse to Trusted Publishers.
10. Click Next and then Finish.
11. Refresh the Browser

## System Center 2016 - Orchestrator and Service Management Automation Release Notes
**The following release notes apply to System Center Technical Preview - Orchestrator and Service Management Automation .**

#### Sending telemetry data for SMA and SPF to Microsoft can only be turned off via PowerShell
**Description:** The default  telemetry data setting is to send data to Microsoft. Since Service Management Automation and Service Provider Foundation do not provide a user interface, you can only change this setting for Service Management Automation or Service Provider Foundation with a  PowerShell cmdlet.

**Work around:** See  [Knowledge Base article 3096505](http://go.microsoft.com/fwlink/?LinkID=708446&clcid=0x409) for detailed instructions on how to stop sending telemetry data to Microsoft for Service Management Automation or Service Provider Foundation.

#### Orchestrator Web Console is not compatible with the Microsoft Edge web browser
**Description:** You cannot open the Orchestrator web console with the Microsoft Edge web browser.

**Work around:** Open the Orchestrator web console with Internet Explorer.

#### Orchestrator 2016 does not have associated Integration packs available.

**Description:** Orchestrator 2016 Integration packs have not been published.

**Workaround:** Use Orchestrator 2012 R2 Integration packs for evaluation purposes.


## System Center 2016 - Service Manager Release Notes
**The following release notes apply to System Center 2016 - Service Manager.**

#### Service Manager might perform slowly with SQL Server 2014 Cardinality Estimation
**Description:** If your Service Manager database is running on SQL Server 2014 with the cardinality estimator set to the SQL Server 2014 version you may experience slow performance.

**Workaround:** Switch the Cardinality Estimator (CE) for the SQL Server to use the SQL Server 2012 version. See the following article for more information on changing the Cardinality Estimator: [New functionality in SQL Server 2014 - Part 2 - New Cardinality Estimation](https://blogs.msdn.microsoft.com/saponsqlserver/2014/01/16/new-functionality-in-sql-server-2014-part-2-new-cardinality-estimation/).

#### The Create Exchange Connector Wizard Might Crash
**Description:** When you run the Create Exchange Connector wizard, the wizard crashes when you click **Test Connection**.

**Workaround:** To work around this issue, avoid clicking **Test Connection** when you run the wizard. Instead, click **Next**, which internally tests the connection and does not crash the wizard.

If the crash has already occurred, you can restart the wizard and use this workaround.

#### Operations Manager CI Connectors do not Sync Properly
**Description:** In Service Manager 2016, if you use the Operations Manager CI connector connected to Operations Manager 2016, then the following issues occur:
1.  Newly created OM CI connectors will not sync properly. However, Operations Manager CI connectors created with previous releases continue to work properly.
2.  Newly created Distributed Applications and Business Services with Operations Manager do not import.

**Workaround:** See [https://www.microsoft.com/download/details.aspx?id=51955](https://www.microsoft.com/download/details.aspx?id=51955) to work around this problem.

#### Service Manager Setup Stops When Upgrading the Self Service Portal on a Management Server
**Description:** This problem occurs when you try to conduct an in-place upgrade of the Service Manager 2012 R2 Self Service portal (for both the Silverlight and HTML versions) to the Self Service portal in Service Manager 2016, when the Self Service portal and Management Server are installed on the same server.

**Workaround:** See [Upgrade to Service Manager](../sm/deploy/Upgrade-to-Service-Manager-Technical-Preview.md) for information about deploying the Self Service portal.

#### Manual steps to configure remote SQL Server 2014 Reporting Services
**Description:** During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you are prompted to follow a procedure in the Deployment Guide to prepare the server. However, if you use SQL Server 2014, you should instead use the following information to prepare the remote computer to host SSRS.

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-   Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you did not use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS12.<INSTANCE_NAME>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

**To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file**

1.  On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2.  For SQL Server 2014, locate the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3.  Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4.  In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located previously.

**To add a code segment to the rssrvpolicy.config file**

1.  On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the following folder:

    - For SQL Server 20014, locate \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer.

2.  Using an XML editor of your choice (such as Notepad), open the rssrvpolicy.config file.

3.  Scroll through the rssrvpolicy.config file and locate th code segments. The following code shows an example of a segment.

    ```

       class="UnionCodeGroup"
       version="1"
       PermissionSetName="FullTrust">
       <IMembershipCondition
          class="UrlMembershipCondition"
          version="1"
          Url="$CodeGen$/*"
       />

    ```

4.  Add the following segment in its entirety in the same section as the other segments.

    ```

       class="UnionCodeGroup"
       version="1"
       PermissionSetName="FullTrust"
       Name="Microsoft System Center Service Manager Reporting Code Assembly"
       Description="Grants the SCSM Reporting Code assembly full trust permission.">
       <IMembershipCondition
          class="StrongNameMembershipCondition"
          version="1"
          PublicKeyBlob="0024000004800000940000000602000000240000525341310004000001000100B5FC90E7027F67871E773A8FDE8938C81DD402BA65B9201D60593E96C492651E889CC13F1415EBB53FAC1131AE0BD333C5EE6021672D9718EA31A8AEBD0DA0072F25D87DBA6FC90FFD598ED4DA35E44C398C454307E8E33B8426143DAEC9F596836F97C8F74750E5975C64E2189F45DEF46B2A2B1247ADC3652BF5C308055DA9"
    />

    ```

5.  Save the changes and close the XML editor.

##### To add an Extension tag to the Data segment in the rsreportserver.conf file

1.  On the computer hosting SSRS, locate the file rsreportserver.config in the following folder:

    -   For SQL Server 2014, locate \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer.

2.  Using an XML editor of your choice (such as Notepad), open the rsreportserver.config file.

3.  Scroll through the rsreportserver.config file and locate the code segment. There is only one code segment in this file.

4.  Add the following **Extension** tag to the code segment where all the other **Extension** tags are:

    ```
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />
    ```

5.  Save the changes and close the XML editor.


#### Service Manager console installed on a VMM Server causes VMM connector failure
**Description:** If the Service Manager console is installed on the same server as VMM, then you cannot use that Service Manager console to create a VMM connector to that VMM server.

**Workaround:** None, however you can use a different Service Manager console to create the VMM connector.


#### Data Warehouse Setup Might Fail if the Database or Log Path Includes a Single Quotation Mark Character
**Description:** During Setup, if you specify a database or log path that includes a single quotation mark character ('), Setup might fail.

**Workaround:** None. The path that you specify cannot include a single quotation mark character.

#### Setup Might Fail if the Service Manager Authoring Tool Has Been Installed
**Description:** Setup might fail if you have previously installed any version of the Service Manager Authoring Tool.

**Workaround:** Remove the Service Manager Authoring Tool, and then retry Setup.

#### Setup Does Not Install the Report Viewer Language Pack
**Description:** Setup includes a prerequisite checker that checks for and - if necessary, installs - the Microsoft Report Viewer. However, Setup does not install the Report Viewer Language Pack, which makes the Microsoft Report Viewer compatible with Windows operating systems that are configured to use languages other than English.

**Workaround:** If your system is configured to use a language other than English, you should manually install the Report Viewer Language Pack for that language.

#### Service Manager Setup Fails if a SQL Server Instance Contains a $ Character
**Description:** If you attempt to install Service Manager using a named Structured Query Language (SQL) instance that contains a dollar sign ($) character, Setup fails.

**Workaround:** Use a SQL instance that does not contain the $ character in its name.

#### Orchestrator Connector Account Password Cannot Contain $ Characters
**Description:** If the Orchestrator connector account password contains a $ character, the sync job completes, however runbooks are not updated in the Service Manager database.

**Workaround:** If your Orchestrator connector account password contains a $ character, change the password to one that does not include the $ character.

#### Information Linked from Setup Might Not Display Localized Content
**Description:** Information that is linked from Setup to the Setup log and to technical documentation might not display localized content. Setup logs in Service Manager are available in English only. Technical documentation is available in a variety of localized languages. Where available, localized technical documentation is displayed on TechNet; however, not all languages are available.

**Workaround:** None.


#### Errors Might Occur When You Modify or Delete Service Request Template Items
**Description:** When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround:** When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.

#### Double-Byte Characters Might Not Display Correctly if a Knowledge Article Is Created from a TXT File
**Description:** If you create a knowledge article using a TXT file that contains double-byte characters, the characters might not display correctly.

**Workaround:** If this problem affects you, do not use TXT files to create knowledge articles. Instead, use RTF files.


#### Configuring the Reporting Server Might Take a Long Time
**Description:** When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround:** None.


#### Sorting Knowledge Articles by Date Does Not Work
**Description:** When you try to sort knowledge articles by date, sorting does not work.

**Workaround:** None.

#### Do not change Active Directory group expansion selection after upgrade until the connector has run at least one time.
**Description:** When upgrading from System Center 2012 R2 - Service Manager to System Center 2016 - Service Manager, do not change the AD group expansion selection value in any AD connector (if it is OFF, let it remain OFF, if it is ON, let it remain ON), until the connector has run at least one time after the upgrade.

**Workaround:** None.

## System Center 2016 - Virtual Machine Manager Release Notes
**The following release notes apply to System Center 2016 - Virtual Machine Manager.**

#### Upgrading a cluster's functional level does not refresh the platform information for a File Server
**Description:** If you upgrade the functional level for a cluster that includes a file server the new platform information will not be automatically updated in the VMM database.

**Workaround:** After upgrading the cluster's functional level, refresh the storage provider for the File Server. This will refresh the platform information.

#### Adding a cluster the VMM Administrative console may result in an error
**Description:** When you add a cluster as a resource in the VMM Administrative console you may receive an error stating "There were no computers discovered based on your inputs".

**Workaround:** Select OK, close the error dialog box, and retry adding the cluster.

#### Creating a tiered file share in a Storage Spaces Direct configuration will fail
**Description:** If you attempt to create tiers of storage (one tier for solid state drives and another for hard disk drives) that are managed by VMM using Storage Spaces Direct, you will receive an error.

**Workaround:** Set the Write Cache Size Default to 0 using the command
Set-StoragePool pool1 -WriteCacheSizeDefault 0

#### SAN migration fails for Nano host
**Description:** If you attempt to do a SAN migration between two stand-alone Nano Server hosts, you will receive an error.

**Workaround:** Perform a network migration instead of a SAN migration.

#### Shielding a VM may result in an error

**Description:** If you shield an existing non-shielded VM or if you create a shielded VM from a non-shielded template, the job might fail with the error: *Error (1730) The selected action could not be completed because the virtual machine is not in a state in which the action is valid.*

The failure happens at the last step of the job in which the VM is shutdown after the shielding is completed, the VM gets shielded properly and is usable.

**Workaround:** Repair and ignore the job.

#### Storing a VM in VMM Library fails if you change the default port for BITS(443) while configuring the VMM Server
**Description:** Storing a VM in VMM Library will fail with the error below if you change the default port for BITS (443) while configuring the VMM Server.
*Error (2940) VMM is unable to complete the requested file transfer. The connection to the HTTP Server \<name> could not be established.*

**Workaround:** Manually add the new port number to the Windows Firewall exceptions list of the Nano host using the below command:
netsh advfirewall firewall add rule name="VMM" dir=in action=allow localport=<port no.> protocol=TCP

#### Bare Metal Deployment of Nano Server-based Compute & Storage clusters may fail
**Description:** Bare metal deployment of Nano Server-based Compute & Storage clusters using VMM may fail.

**Workaround:** Skipping the cluster validation while deployment typically works, if it does not work for you, do bare metal deployment of Nano Server-based individual hosts and then create a cluster out of the hosts.

#### Service deployments from Service templates will fail if you include "Desktop Experience" & other GUI related features in your service template
**Description:** Deploying a Service template that has "Desktop Experience" & other GUI related features included will fail as these options are no longer supported in Windows Server.

**Workaround:** There is no workaround, do not include these features in your service template.

#### Deployment of Service and servicing of a service on Server Core or Nano Server-based hosts will fail if the host has Guest Integration Services disabled
**Description:** If you try to deploy a service or service a service on a Server Core/Nano Server host that has Guest Integration Services disabled, it will fail.

**Workaround:** For the host (Server Core/Nano Server), use a VHD that has Guest Integration Services enabled to workaround the issue.

#### Attempting to join a Nano Server VM to a domain during deploying the VM will fail, the VM gets deployed but does not join the domain
**Description:** While deploying a Nano Server VM, if you try to join the VM to a domain by specifying the domain join information on the OS Configuration page of the VM deployment Wizard, VMM will deploy the VM but will not join it to the specified domain.

**Workaround:** After the VM is deployed, create an offline domain join blob and run the djoin cmdlet to join the VM to the domain

#### VMM throws an error when you start a VM configured for Start Ordering
**Description:** Windows Server 2016 has a new functionality called VM Start Ordering which can be used to define the order in which dependent VMs will get started. This functionality is not exposed through VMM today. However, if you have configured VM start ordering outside of VMM, VMM does honor the order in which the VMs will start. It however throws the below false positive error which should be ignored *Error (12711)
VMM cannot complete the WMI operation on the server <servername> because of an error: [MSCluster_ResourceGroup.Name=<name>] The group or resource is not in the correct state to perform the requested operation.
The group or resource is not in the correct state to perform the requested operation (0x139F)

Recommended Action
Resolve the issue and then try the operation again.*

**Workaround:** Ignore the error as the VMs will start in the correct order.

#### Bare metal deployment of hosts may fail after VMM in an HAVMM setup is upgraded from VMM 2012 R2 to VMM 2016
**Description:** In a Highly Available (HA) VMM environment, after a VMM upgrade, VMM may incorrectly update the Windows Deployment Services (WDS) registry key, HKLM\SYSTEM\CCS\SERVICES\WDSSERVER\PROVIDER\WDSPXE\PROVIDES\VMMOSDPROVIDER, to 'HOST/VIRT-VMM-1' instead of 'SCVMM/VIRT-VMM-1'. This will lead to failure of bare metal deployment of hosts & clusters.

**Workaround:** Manually change the registry entry for HKLM\SYSTEM\CCS\SERVICES\WDSSERVER\PROVIDER\WDSPXE\PROVIDES\VMMOSDPROVIDER to 'SCVMM/VIRT-VMM-1' and then try bare metal deployment of hosts & clusters.

#### Trying to import a Console add-in as a non-administrator to VMM will fail
**Description:** If you are not an administrator and you try to import a console add-in to VMM, the console will crash. This is because the console add-in is stored at location “C:\Program Files\” which only administrators have access to.

**Workaround:** Store the console add-in at a location where the user has write access, for example “C:\user\<username>\”, and then try importing the add-in.

#### WinRM error blocks setting the static IP on the backend NIC of the SLB MUX VM
**Description:** If you try to assign a static IP address to one or more of Software Load Balancer MUX Virtual Machines during the SLB deployment, a WinRM error blocks the operation.

**Workaround:** Re-try the operation.

#### Teamed Software Defined Network Switch deployment fails on Nano hosts
**Description:** You can't deploy a teamed switch on Nano hosts using VMM 2016 TP5.

**Workaround:** Deploy an SDN switch on any single physical NIC adaptor of the host.

#### Inconsistent Network Address Translation user interface
**Description:** The existing NAT connections will not be visible when you close the network connectivity wizard and reopen it. Additionally, UI doesn't allow you to choose the IP Address from the pool for creating NAT connection.

**Workaround:** User can still add the NAT connections through UI. To see the existing NAT connections, user can leverage Powershell cmdlets
Get-SCNATConnection

#### vNIC connected to Network Controller managed network must be restarted on IP Address change
**Description:** If there is a change in assigned IP address on any of the vNICs that are connected to a Network Controller managed VM Network, you need to manually restart the associated vNIC(s).

**Workaround:** No workaround.

#### IPV6 configuration is not supported for Network Controller managed infrastructure
**Description:** IPV6 configurations are not supported with System Center 2016 TP5 - VMM.

**Workaround:** Use IPV4 configuration with VMM 2016 TP5.

#### User needs to disable "Register this connection's address in DNS" option for Frontend and Backend IPs Software Load Balancer MUX VMs
**Description:** For Front End and Back End IPs assigned to Software Load Balancer MUX Virtual Machines you need to uncheck the option for 'Register this connection's address in DNS'. Having this option checked may cause issues with the connectivity over these IP addresses.

**Workaround:** No workaround

#### Adding a host to VMM with Storage Spaces Direct enabled will result in a warning
**Description:**When hosts are added to a cluster with storage spaces direct enabled, a warning "Multipath I/O is not enabled for known storage arrays on host <\hostname>" is generated.

**Workaround:** None, you can ignore the warning.

#### In Storage Spaces Direct, the Create Volume UI does not support creation of tiered volume with Solid-state drive (SSD) user-interface
**Description:** If you are creating a storage tier in the Storage Spaces Direct user interface, you will be limited to tiers using Hard Disk Drive (HDD) storage.

**Workaround:** You can create tiered volumes with SSD storage via PowerShell.

#### Deploying Scale out File Server on a Storage Spaces Direct configuration through SCVVM RTM fails
**Description:** If you deploy Scale out File Server (SoFS) on a Storage Spaces Direct configuration, the following error occurs:
Error 25305: "Unable to execute the task because of error: Unable to cast object of type 'System.String' to type 'System.IO.FileInfo' " 

**Workaround:** Deploy the Scale Out File Server using VMM PowerShell with [-SkipClusterValidation] or deploy the same out of band and bring it under VMM management.

#### VM deployment on Scale Out File Server using fast file copy completes with warning
**Description:** If you deploy a VM on a Scale Out File Server using fast file copy, the action completes successfully with the following warning:
"VMM could not transfer the file <source location> to <destination location> using fast file copy. The VMM agent on <host> returned an error.
The user name or password is incorrect (0x8007052E)

**Workaround:** None

#### In VMM UI, cluster validation is always performed during creation of a hyperconverged Storage Spaces Direct enabled cluster
**Description:**  If you create a hyperconverged Storage Spaces Direct enabled cluster using VMM UI, cluster validation is always performed.

**Workaround:**  To skip cluster validation when creating a cluster, use VMM PowerShell to create the cluster with the -skipClusterValidation option.

#### When adding a node to a cluster using VMM, cluster validation is always performed even when the skip cluster validation option is specified
**Description:** If you add a node to an existing hyperconverged cluster using Storage Spaces Direct technology using VMM, cluster validation is always performed.

**Workaround:** To skip cluster validation when adding a node to the cluster, use Windows PowerShell to add the node with the appropriate skip cluster validation option.

#### When managing Storage Replica using VMM, a critical exception is generated when the read storage provider operation is performed after storage replication is enabled or a failover is performed.
**Description:** If you perform the read storage provider operation after enabling storage replication OR performing failover, the job will fail with critical exception ‘dictionary key cannot be null’  for the recovery site provider.

**Workaround:** Restart the storage cluster for recovery site provider from failover cluster manager, wait for some time as cluster service may take time to update the objects even after restart. Then, retry the read storage provider operation.
