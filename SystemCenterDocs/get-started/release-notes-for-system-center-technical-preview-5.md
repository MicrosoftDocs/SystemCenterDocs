---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  cfreemanwa
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-08-04
title:  Release Notes for System Center Technical Preview 5
ms.assetid:  5fad5608-4cb7-48b0-aa31-35ca5cc2d560
---

# Release Notes for System Center Technical Preview 5

>Applies To: System Center 2016 Technical Preview 5

The following set of notes lists known issues and steps to mitigate the issue. These notes only apply to System Center 2016 Technical Preview 5.

## System Center Technical Preview - Data Protection Manager Release Notes

The following release notes apply to System Center Technical Preview - Data Protection Manager.

#### SQL Server Setup error

**Description:** When you specify a SQL Server while setting up System Center 2016 - Data Protection Manager you may encounter an error.

**Work around:** Specify the Fully Qualified Domain Name (FQDN) for the computer hosting SQL Server.

#### VM backup from a remote file share

**Description:** If you attempt to use System Center 2016 - Data Protection Manager to back up a virtual machine stored on a remote file share you will receive an error.

**Work around:** Add all Hyper-V compute nodes to the Backup Operators group on the Scale-out File Server (SOFS) nodes. To do this run  the following command on the SOFS nodes:  `net localgroup "Backup Operators" domainname\hypervmachinename$ /add`

#### System Center 2016 - Data Protection ManagerTP4 supports protecting workloads on Windows Server 2008 R2 SP1 and above

**Description:** Installing the DPM agent on Windows Server 2008 or Windows Server 2008 R2 is not supported by System Center 2016 - Data Protection Manager.

**Workaround:** Install SP1 on the Windows Server 2008 R2 server, and install Windows Management Framework 4.0.

#### DPM protection of a highly available VM managed by VMM will fail after migration to a new cluster

**Description:** If you migrate a virtual machine managed by VMM that you have made highly available to a new cluster, DPM backup will stop functioning on the virtual machine.

**Workaround:** Run DPM inquiry for the migrated virtual machine.

#### Setting an alternate destination recovery for a host with remote storage does not update the DPM UI

**Description:** If you set the Alternate Location Recovery for a virtual machine to a host that uses remote storage, the "Specify Alternate Recovery Location" wizard will not provide the list of available hosts.

**Workaround:** Retrieve the list of alternate recovery locations via PowerShell.

#### DPM will not protect Windows Server 2016 Nano Server

**Description:** You can't use DPM to back up Windows Server 2016 Nano Server.

#### Online recovery of SQL master database fails, after upgrading DPM to TP5

**Description:** If your DPM installation's SQL server master database is protected (i.e. backed up) to Azure, and you upgrade to System Center DPM 2016 and then attempt to restore using an online recovery point, the recovery job will fail.

**Workaround:** To recover the master SQL database, you will need to recover the database as files using SQL Server.

#### Backup fails after upgrading DPM to TP5

**Description:** If you upgrade DPM to TP5 and trigger a backup job of data already protected to Azure, the backup job fails.

**Workaround:** To avoid this problem, re-register the DPM Server with the backup vault, and modify the protection group.   

#### DPM notification message, "DPM has received an improperly formed message"

**Description:** If you protect a Sharepoint farm to Azure with DPM TP5, your initial replication jobs will be successful, but you'll receive a message, "DPM has received an improperly formed message."

**Workaround:** You can ignore this message. The recovery points are correct and work for restoration.

#### DPM notification message, "SQL is remote and agent needs to be installed."

**Description:** When protecting a SQL database with DPM, you may receive an error message that SQL is remote and the agent needs to be installed.

**Workaround:** You can ignore this message. There is no action to take. The backup jobs will work correctly.

#### Recovery point fails when Hyper-V VM is in a Saved or Paused state

**Description:** If DPM attempts to take a recovery point snapshot when the Hyper-V VM is in a paused or saved state, the recovery point fails.

**Workaround:** To avoid this problem, don't put the VM in a paused or saved state when it is being backed up. This issue only happens when online backup is enabled. Online back can be turned off by unchecking the **Backup (volume shadow copy)** in the VM settings -> Integration Services. Please note - this means backup is not going to be app consistent.

#### Recovery point volume size cannot be modified with UI

**Description:** The Recovery point volume size cannot be modified with the UI. The field **Modify disk allocation for protected datasource** is disabled and cannot be enabled.

**Workaround:** It is possible to use PowerShell to edit the recovery point volume size. Use the following command to edit the size:

```
Edit-DPMDiskAllocation -Datasource <Datasource object> -ShadowCopySize <new size>
```

## System Center Technical Preview - Operations Manager Release Notes

The following release notes apply to System Center Technical Preview - Operations Manager.

#### Operations Manager Console will stop responding if you attempt to resolve a dependency while  importing a Management Pack

**Description:** When you click **Import Management Packs** from the Administration section of the Operations Manager console, the console will display the  **Resolve** button if the Management Pack is dependent on another Management Pack. If you click  Resolve you will see the **Dependency Warning**. If you click the **Resolve** button in the warning the Operations Manager console will stop responding.

**Workaround:** Install the Update for System Center 2016 - Operations Manager. See the Knowledge Base article [3117586](https://support.microsoft.com/en-us/kb/3117586) for specific instructions.

#### Client-side monitoring (CSM) alerts might stop flowing from the System Center Operations Manager management server host

**Description:** The update sequence of System Center Operation Manager management server may cause an issue with the client-side monitoring alerts collection from the management server host. System Center Operations Manager agents are not affected.
Likelihood of occurrence: Medium

**Workaround:** Restart the "Microsoft Monitoring Agent" service on System Center Operations Manager management server host.

#### Application performance monitoring (APM) events, client-side monitoring (CSM) events, and application performance monitoring (APM) alerts might stop flowing from the System Center Operations Manager agent hosts

**Description:**  The update sequence of System Center Operations Manager agent may cause an issue with the following:

-   Client-side monitoring (CSM) events and alerts collected on the host.

-   Application Performance Monitoring (APM) events and alerts collected on the host.

System Center Operations Manager management server is not affected.

**Workaround:** Restart the "Microsoft Monitoring Agent" service on the System Center Operations Manager agent host that is experiencing the issue.

#### Application performance monitoring (APM) for Windows services is not supported in System Center - Operations Manager on hosts where Application Insights Status Monitor is installed.

**Description:** Application performance monitoring (APM) workflow fails to process monitoring configuration for .NET Windows services on the hosts if Application Insights Status Monitor and the System Center - Operations Manager agent are both installed.

**Workaround:** Uninstall Application Insights Status Monitor.

#### Telemetry data may be erroneously sent when the "Usage and Connectivity Data" setting is set to "False"

**Description:** If two operators have Operations Manager consoles open and one sets the Usage and Connectivity Data setting to "Do not send data" data may continue to flow to Microsoft until the second user closes and reopens their instance of the Operations manager console.

**Workaround:** Restart all Operations Manager console sessions after making changes to the Usage and Connectivity setting.

**Description:** When a new component such as a management server or gateway server are added to an existing SCOM environment, usage information about the setup process is sent to Microsoft even though the Usage and Connectivity Data setting is set to "Do not send data". After the component is added, no further usage data will be sent to Microsoft from the component.

**Workaround:** None

#### Using sudo elevation with Solaris operating systems requires a configuration change if sudo executable is not in an expected path

**Description:** If you want to use sudo elevation on a computer running Solaris, and the sudo executable is not in an expected path, you need to create a link to the correct path. Operations Manager will look for the sudo executable in the path /opt/sfw/bin, and then in the path /usr/bin. If sudo is not installed in one of these paths, a link is required.

**Workaround:** The UNIX and Linux agent installation script creates the symbolic link /etc/opt/Microsoft/scx/conf/sudodir to the folder expected to contain sudo. The agent uses this symbolic link to access sudo. The installation script automatically creates the symbolic link, so no action is needed for standard UNIX and Linux configurations. However, if sudo is installed in a non-standard location, you should change the symbolic link to point to the folder where sudo is installed. If you change the symbolic link, its value is maintained for uninstall, re-installation, and upgrade operations with the agent.

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

## System Center Technical Preview - Orchestrator and Service Management Automation Release Notes

The following release notes apply to System Center Technical Preview - Orchestrator and Service Management Automation.

#### Sending telemetry data for SMA and SPF to Microsoft can only be turned off via PowerShell

**Description:** The default  telemetry data setting is to send data to Microsoft. Since Service Management Automation and Service Provider Foundation do not provide a user interface, you can only change this setting for Service Management Automation or Service Provider Foundation with a  PowerShell cmdlet.

**Work around:** See  [Knowledge Base article 3096505](http://go.microsoft.com/fwlink/?LinkID=708446&clcid=0x409) for detailed instructions on how to stop sending telemetry data to Microsoft for Service Management Automation or Service Provider Foundation.

#### Orchestrator Web Console is not compatible with the Microsoft Edge web browser

**Description:** You cannot open the Orchestrator web console with the Microsoft Edge web browser.

**Work around:** Open the Orchestrator web console with Internet Explorer.

#### Orchestrator 2016 TP5 does not have associate Integration packs available.

**Description:** Orchestrator 2016 Integration packs have not been published.

**Workaround:** Use Orchestrator 2012 Integration packs for evaluation purposes.

## System Center Technical Preview - Service Manager Release Notes

The following release notes apply to System Center Technical Preview - Service Manager.

#### The Create Exchange Connector Wizard Might Crash

**Description:** When you run the Create Exchange Connector wizard, the wizard crashes when you click **Test Connection**.

**Workaround:** To work around this issue, avoid clicking **Test Connection** when you run the wizard. Instead, click **Next**, which internally tests the connection and does not crash the wizard.

If the crash has already occurred, you can restart the wizard and use this workaround.

#### Operations Manager CI Connectors do not Sync Properly

**Description:** In Service Manager 2016, if you use the Operations Manager CI connector connected to Operations Manager 2016 TP5, then the following issues occur:

1.  Newly created OM CI connectors will not sync properly. However, Operations Manager CI connectors created with previous releases continue to work properly.

2.  Newly created Distributed Applications and Business Services with Operations Manager do not import.

**Workaround:** See [https://www.microsoft.com/download/details.aspx?id=51955](https://www.microsoft.com/download/details.aspx?id=51955) to work around this problem.

#### Service Manager Setup Stops When Upgrading the Self Service Portal on a Management Server

**Description:** This problem occurs when you try to conduct an in-place upgrade of the Service Manager 2012 R2 Self Service portal (for both the Silverlight and HTML versions) to the Self Service portal in Service Manager 2016 TP5, when the Self Service portal and Management Server are installed on the same server.

**Workaround:** See [Upgrade to Service Manager Technical Preview](../sm/deploy/Upgrade-to-Service-Manager-Technical-Preview.md) for information about deploying the Self Service portal.

#### Manual steps to configure remote SQL Server 2014 Reporting Services

**Description:** During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you are prompted to follow a procedure in the Deployment Guide to prepare the server. However, if you use SQL Server 2014, you should instead use the following information to prepare the remote computer to host SSRS.

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-   Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you did not use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS12.<INSTANCE_NAME>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

##### To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file

1.  On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2.  For SQL Server 2014, locate the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3.  Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4.  In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located previously.

##### To add a code segment to the rssrvpolicy.config file

1.  On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the following folder:

    1.  For SQL Server 20014, locate \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer.

2.  Using an XML editor of your choice (such as Notepad), open the rssrvpolicy.config file.

3.  Scroll through the rssrvpolicy.config file and locate the code segments. The following code shows an example of a segment.

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

#### Self-Service Portal is not compatible with the Microsoft Edge web browser

**Description:** You cannot open the Self-Service Portal with the Microsoft Edge web browser.

**Workaround:** Use Internet Explorer to open Self-Service Portal.

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

#### Full Text Search Does Not Work for Some Turkish Language Characters

**Description:** Full text search in the Self-Service Portal works only if you have a licensed non-Microsoft word breaker installed. However, full text search does not work for some characters of the Turkish language even if you have a licensed non-Microsoft Turkish word breaker installed.

**Workaround:** Load a licensed non-Microsoft word breaker that enables full-text search to function. For more information, see the following links for the version of SQL Server that you are using:

-   [SQL Server 2014](http://msdn.microsoft.com/library/ms142509(v=sql.120))

-   [SQL Server 2012](http://msdn.microsoft.com/library/ms142509(v=sql.110))

-   [SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=205557)

-   [SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=205800)

#### Unassigned Virtual Machines Appear in Reporting Information

**Description:** All virtual machines appear in Microsoft Online Analytical Processing (OLAP) cube data and the sample Microsoft Excel report, regardless of whether a virtual machine is assigned to a cloud. Reporting information is designed to show unassigned virtual machines as rows without price sheet data.

**Workaround:** None.

#### Virtual Machine Component Aggregation Is Misleading

**Description:** The SystemCenterVmmCloudChargebackCube OLAP cube contains aggregated values for virtual machine components. However, values for the components should not be expressed in the cube using any manner other than a daily count.

**Workaround:** None. However, you should ignore any aggregated time values for virtual machine components other than daily values.

#### Reassigned Virtual Machine Values Might Be Erroneously Calculated

**Description:** When you remove and then reassign a virtual machine from one cloud object to another, erroneous calculated values might appear for both clouds where the virtual machine was assigned. This condition might occur only for the same date when values for the virtual machine are not removed from the cloud that the virtual machine was initially assigned to. Data for the next day is accurate.

**Workaround:** None.

#### Values in Price Sheets Are Effective Starting on the Next Day

**Description:** When you type a value in a price sheet, the value becomes effective on the following day. For example, if you modify a calculated price today, the updated price will not immediately appear in OLAP cube data or the sample chargeback Excel report. Instead, the old price continues to appear in OLAP cube data and the sample chargeback Excel report. This behavior is expected; you can use it to update prices throughout your business day without the prices going into effect until the next business day.

**Workaround:** None.

#### After the Display Language Is Changed, the Wizard Text Might Display an Incorrect Language

**Description:** After you change the display language using the **Language** menu in the Service Manager console, wizard text might be displayed in your previously selected language.

**Workaround:** If this problem affects you, do the following:

1.  Close the Service Manager console.

2.  On the **Start** menu, click **Run**, type **%temp%**, and then click **OK**.

3.  Navigate up to the parent LOCAL folder.

4.  Open \Microsoft\System Center Service Manager 2010\<ServerName>\<VersionNumber>, and then delete the contents of the folder.

5.  Open the Service Manager console. The wizard text should appear in the language that you selected previously.

#### Errors Might Occur When You Modify or Delete Service Request Template Items

**Description:** When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround:** When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.

#### Double-Byte Characters Might Not Display Correctly if a Knowledge Article Is Created from a TXT File

**Description:** If you create a knowledge article using a TXT file that contains double-byte characters, the characters might not display correctly.

**Workaround:** If this problem affects you, do not use TXT files to create knowledge articles. Instead, use RTF files.

#### Configuring the Reporting Server Might Take a Long Time

**Description:** When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround:** None.

#### Double-Byte Characters Are Sent Incorrectly to Search Provider

**Description:** When you perform a knowledge search and you type double-byte characters in the **Search Provider** box, they are not sent correctly to the search website. Instead, erroneous characters are sent.

**Workaround:** None.

#### Sorting Knowledge Articles by Date Does Not Work

**Description:** When you try to sort knowledge articles by date, sorting does not work.

**Workaround:** None.

#### Service Manager AD group expansion feature of the Active Directory connector works best with SQL Server 2012 Cardinality Estimation

**Description:** If you use the AD Group expansion capability of the Active Directory Connector, you may experience slow performance if your SQL Server database is SQL Server 2014.

**Workaround:** Switch the Cardinality Estimator (CE) for the SQL Server to use the SQL Server 2012 version. See the following article for more information on changing the Cardinality Estimator: [New functionality in SQL Server 2014 - Part 2 - New Cardinality Estimation](http://blogs.msdn.com/b/saponsqlserver/archive/2014/01/16/new-functionality-in-sql-server-2014-part-2-new-cardinality-estimation.aspx).

## System Center Technical Preview - Virtual Machine Manager Release Notes

The following release notes apply to System Center Technical Preview - Virtual Machine Manager.

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

#### You cannot create a shielded VM if the Guarded Host and the VMM management server are in separate domains that do not have a two-way trust relationship.

**Description:** For the TP5 release of Windows Server 2016 and System Center 2016 the Guarded Host and the VMM Management Server must either be in the same domain, or in domains with a two-way trust relationship.

**Workaround:**  None

#### Removing the Host Guardian Service from a host will produce an error even though the job succeeds.

**Description:** If you remove the Host Guardian Service by modifying the Host properties for a host managed by VMM, you will receive error (20593)
While the Host Guardian Service URLs were being set on the host, the following error was received: Object reference not set to an instance of an object.

**Workaround:** Make sure the host is responding, and try the operation again.  

#### Shielding a VM by setting its properties to either shielded or encrypted may result in an error.

**Description:** If you shield an existing non-shielded VM by changing its properties to be either shielded or encrypted supported, or if you create a shielded VM from a non-shielded template, the job might fail with the error: Error (1730) The selected action could not be completed because the virtual machine is not in a state in which the action is valid. The failure happens at the last step of the job in which the VM is shut down after the shielding is completed, the VM gets shielded properly and is usable.

**Workaround:** Repair and ignore the job.

#### Storing a VM in the VMM Library fails if change the default port for BITS (443) while configuring the VMM Server running on Nano Server.

**Description:** Storing a VM in VMM Library will fail with the error below if you change the default port for BITS 443 while configuring the VMM Server running on a Nano Server installation.
Error 2940 VMM is unable to complete the requested file transfer. The connection to the HTTP Server \<name> could not be established.

**Workaround:** Manually add the new port number to the Windows Firewall exceptions list of the Nano host using the below command:
netsh advfirewall firewall add rule name="VMM" dir=in action=allow localport=<port no.> protocol=TCP

#### Bare Metal Deployment of Nano Server-based hosts & clusters fails

**Description:** Bare metal deployment of Nano Server-based hosts, compute & storage clusters using VMM will fail.

**Workaround:** Install Nano Server on bare computers out of band and add it to VMM's management

### WinRM error blocks setting the static IP on the backend NIC of the SLB MUX VM
**Description:** If you try to assign a static IP address to one or more of Software Load Balancer MUX Virtual Machines during the SLB deployment, a WinRM error blocks the operation.

**Workaround:** Re-try the operation.


### vNIC connected to Network Controller managed network must be restarted on IP Address change
**Description:** If there is a change in assigned IP address on any of the vNICs that are connected to a Network Controller managed VM Network, you need to manually restart the associated vNIC(s).

**Workaround:** No workaround

### IPV6 configuration is not supported for Network Controller managed infrastructure
**Description:** IPV6 configurations are not supported with System Center 2016 TP5 - VMM.

**Workaround:** Use IPV4 configuration with VMM 2016 TP5.

### User needs to disable "Register this connection's address in DNS" option for Frontend IPs Software Load Balancer MUX VMs
**Description:** For Front End and Back End IPs assigned to Software Load Balancer MUX Virtual Machines you need to uncheck the option for 'Register this connection's address in DNS'. Having this option checked may cause issues with the connectivity over these IP addresses.

**Workaround:** No workaround

### Users Can't migrate Virtual Machines connected to one connected SDN networks.
**Description:** With VMM 2016 RTM, Users can't migrate Virtual Machines that are connected to one connected SDN networks. This is applicable in the scenarios - for live migration within the cluster and move VM operation across clusters
**Workaround:** No Workaround.

### Users are unable to delete NAT connection from UI in an NC managed Network.
**Description:**  ID you enabled NAT connection in an NC managed Network, then disabled the NAT checkbox, you will observe that NAT connections will persist in the UI even after disabling NAT connection.
**Workaround:** This issue will not appear in the Powershell query.

###  SCVMM identifies a Nano SET switch as Internal
**Description:** If you configured SET on Nano Servers outside of VMM and then on boarded the Nano set up into VMM< SCVMM will the see the team as 'Internal' even though you initially specified teaming type as 'External'
**Workaround:** No workaround, the switch, although identified as Internal, continues to provide connectivity as earlier. This is merely a UI bug.

### LACP team non-functional for Logical Switch after Upgrade
**Description:** During Rolling Upgrades, if you have one or more Logical Switches with LACP team port profile, these switches will fail LACP based negotiations post Upgrade
**Workaround:** Remove and re-add one or more member NIC adaptors manually to workaround this issue



#### Creating a template from a Generation 1 virtual machine on a Nano Server-based host will fail

**Description:** This is not a supported scenario for System Center 2016 TP5 - VMM.

**Workaround:** Instead of creating a template from a Gen 1 VM, you can create a VM template from scratch.


#### Adding a host to VMM with Storage Spaces Direct enabled will result in a warning  

**Description:** When hosts are added to a cluster with storage spaces direct enabled, a warning "Multipath I/O is not enabled for known storage arrays on host <\hostname>" is generated.


**Workaround:** None, you can ignore the warning.

#### In Storage Spaces Direct, the Create Volume UI does not support creation of tiered volume with Solid-state drive (SSD)
user-interface

**Description:** If you are creating a storage tier in the Storage Spaces Direct user interface, you will be limited to tiers using Hard Disk Drive (HDD) storage.

**Workaround:** You can create tiered volumes with SSD storage via PowerShell.
