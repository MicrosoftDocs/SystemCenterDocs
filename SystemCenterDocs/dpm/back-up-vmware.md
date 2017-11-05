---
description: Use DPM to back up VMware VM.
manager:  carmonm
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 11/08/2017
title:  Back up VMware Virtual Machines
ms.technology:  data-protection-manager
ms.assetid:
ms.author: markgal
monikerRange: 'sc-dpm-1711'
---

# Use DPM 1711 to back up VMware virtual machines

This article explains how to use Data Protection Manager (DPM) 1711 to back up virtual machines running on the 5.5 and 6.0 versions of VMware vCenter and vSphere Hypervisor (ESXi).

## Supported VMware features

DPM 1711 provides the following features when backing up VMware virtual machines:

- Agentless backup: DPM 1711 does not require an agent to be installed on the vCenter or ESXi server, to back up the virtual machine. Instead, just provide the IP address or fully qualified domain name (FQDN), and login credentials used to authenticate the VMware server with DPM.
- Cloud Integrated Backup: DPM protects workloads to both disk and cloud. DPM's backup and recovery workflow helps you manage long-term retention and offsite backup.
- Detect and protect VMs managed by vCenter: DPM detects and protects VMs deployed on a VMware server (vCenter or ESXi server). As your deployment size grows, use vCenter to manage your VMware environment. DPM also detects VMs managed by vCenter, allowing you to protect large deployments.
- Folder level auto protection: vCenter lets you organize your VMs in VM folders. DPM detects these folders and lets you protect VMs at the folder level and includes all sub-folders. When protecting folders, DPM not only protects the VMs in that folder, but also protects VMs added later. DPM detects new VMs on a daily basis and protects them automatically. As you organize your VMs in recursive folders, DPM automatically detects and protects the new VMs deployed in the recursive folders.
- DPM protects VMs stored on a local disk, network file system (NFS), or cluster storage.
- DPM protects VMs migrated for load balancing: As VMs are migrated for load balancing, DPM automatically detects and continues VM protection.
- DPM can recover files/folders from a Windows VM without recovering the entire VM. This helps recover necessary files faster.

## Prerequisites and Limitations

Before you start backing up a VMware virtual machine, review the following list of limitations and prerequisites.

- If you have been using DPM to protect a VMware server as a Windows Server, you cannot use the same fully qualified domain name (FQDN) or static IP. If you used a FQDN to identify your VMware VM, then use a static IP address to identify your VMware server. If you used a static IP address to identify your VMware VM earlier, then use a FQDN to identify your VMware VM. You cannot use a dynamic IP address.
- If you use vCenter to manage ESXi servers in your environment, add vCenter (and not ESXi) to the DPM protection group.
- DPM cannot protect VMware VMs to tape or a secondary DPM server.
- You cannot back up user snapshots before the first DPM backup. Once DPM completes the first backup, then you can back up user snapshots.
- DPM cannot protect VMware VMs with pass-thru disks and physical raw device mappings (pRDM).
- DPM cannot detect or protect VMware vApps.
- DPM cannot protect VMware VMs with existing snapshots.

## Configure DPM to protect VMware

The following information details how to configure VMware for DPM protection. To establish communication between DPM and the VMware server, configure the VMware credentials and establish a secure connection between DPM and the VMware vCenter Server or VMware vSphere Hypervisor (ESXi) server. If you use both vCenter Server and ESXi server, configure only the vCenter Server to work with DPM. You don't need to add ESXi servers to DPM. To manage a VMware server, DPM needs valid credentials to access VMware servers.

### Credential management

DPM does not use an agent to communicate with a VMware server. Instead, DPM uses a user name and password credential to authenticate its remote communication with the VMware server. Each time DPM communicates with a VMware server, DPM must be authenticated. As it can be necessary to change credentials, and a data center can have multiple vCenter servers requiring unique credentials, tracking these credentials can be a problem. However, DPM has a Manage VMware Credentials feature to securely store and manage credentials.

Note the following details about credentials:

- One credential can be used to authenticate multiple VMware servers.
- Once credential details such as: Description, User name or Password are updated, DPM uses these credentials to communicate with all VMware servers.
- A credential can be deleted only if it is not being used to authenticate a VMware server.

#### To open the Manage VMware Credentials feature

1. In the DPM Administrator Console, click **Management**.

    ![steps to open ](./media/open-vmware-mgmt.png)

2. In the list of assets to manage, click **Production Servers**.
3. In the tool ribbon, click **Manage VMware Credentials**.
    The **Manage Credentials** dialog opens. Using the **Manage Credentials** dialog, you can add, update, or delete credentials.
   ![open Manage Credentials dialog](./media/manage-credentials-dialog.png)

   See the following sections for detailed information on adding, updating, or deleting credentials.

#### Add VMware server credentials

You add a credential to the DPM server so you can pair it up with credential on the VMware server. Remember, the credential on the DPM server must be identical to the credential on the VMware server. To add a credential, in the **Manage Credentials** dialog:

1. Click **Add** to open the Add Credential dialog.
  ![open Add Credentials dialog](./media/add-credentials-dialog.png)

2. Type your information in the **Name**, **Description**, **User name**, and **Password** fields. Once you've added text in the required fields, the **Add** button becomes active.
   - **Name** is what appears in the **Credential** column of the Manage Credentials dialog. **Name** is a required field and is the identifier for the credentials. This field cannot be edited later. If you want to change the name of a credentials, you must add a new credential.
   - **Description** is descriptive text or an alternate name so you can recognize or distinguish the credentials in the Manage Credentials dialog. The **Description** text is an optional field and appears in the **Description** column of the Manage Credentials dialog.
   - **User name** and **Password** are the user name and password for the user account used to access the server. Both field are required.
3. Click **Add** to save your new credentials. Once you have created credentials, you can use them to authenticate with a VMware server.

#### Update VMware server credentials

Most organizations need to update credentials due to security reasons or personnel changes. When VMware server credentials are changed, the credentials used by DPM also need to be updated. If a VMware server's credentials have changed - that is, the user name and password have been changed, you must add matching credentials in DPM.

Once you have matching credentials in DPM, update the VMware server credentials using the following steps:

1. In the DPM Administrator console, click **Management**.
2. In the list of assets to manage, click **Production Servers**.
3. In the list of computers, select the VMware server whose credentials need to be updated.
   In the example image, *demovcenter1.Contoso.com* is the VMware server with broken credentials.
   ![open Add Credentials dialog](./media/broken-credentials.png)
4. On the Administrator console tool ribbon, click **Change Settings**.
    The Change Settings dialog opens. It displays all credentials on the DPM server. In the example image, *demovcenter_002* is the DPM credential to pair with demovcenter1.Contoso.com.
   ![open Add Credentials dialog](./media/change-settings-dialog.png)
5. From the list, select the credential on the DPM server to match the VMware credential and click **Update**.
    In the image, notice demovcenter_002 authenticates a production server, and demovcenter1.Contoso.com is now protected.
   ![open Add Credentials dialog](./media/update-server-credential.png)

#### Delete VMware server credentials

When you delete credentials, you are removing the credential from the list on the DPM server. To prevent accidentally breaking authentication between DPM and VMware, DPM won't allow you to delete a credential being used to authenticate a production server.

To delete a credential

1. In the DPM Administrator Console, click Management, click Production Servers, and in the tool ribbon, click Manage VMware Credentials.
2. In the Manage Credentials dialog, select the credential. Make sure the credential is not associated with any Production Servers.
3. Click **Delete** to remove the credential from the list. 

### Set up secure communication between DPM and a VMware server

DPM communicates with the VMware server securely over an HTTPS channel. To create the secure communication, install a trusted certificate on both the VMware server and DPM server. If the connection to your vCenter is not secure, you can secure it by installing a certificate on the DPM server. Use the same certificate to make a secure connection with the VMware server.

To verify there is a secure communication channel between DPM and vCenter, open a browser on the DPM server and access the VMware server. If you are using Chrome, and you do not have a valid certificate you will see the strikethrough in the URL, like this:

![no secure communication channel ](./media/no-secure-communication-chrome.png)

Or if you are using Internet Explorer, and you don't have a valid certificate, you will see this message when you access the URL:

![no secure communication channel ](./media/no-secure-communication-ie.png)

To fix the error, install a valid certificate on the DPM server and the VMware server. In the previous images, the DPM server has a valid certificate, but the certificate is not in the trusted root certification authority store. To fix this situation we need to add the certificate to the VMware server.

1. On the Certificate dialog, on the **Certification Path** tab, click **View Certificate**.

   ![open View Certificate dialog ](./media/certification-path-add-certificate.png)

2. In the new Certificate dialog, click the **Details** tab, and then click **Copy to File** to open the Certificate Export Wizard.

   ![open View Certificate dialog ](./media/add-new-certificate.png)

3. In the **Certificate Export Wizard**, click **Next**, and on the **Export File Format** screen, select **DER encoded binary X.509 (.CER)**, then click **Next**.
4. On the **File to Export** screen, type a name for your certificate and click **Next**.
5. Click **Finish** to complete the **Certificate Export Wizard**.
6. Go to the location where you exported the certificate, and right-click the certificate and select **Install Certificate** to open the **Certificate Import Wizard**.
   ![click install Certificate ](./media/install-certificate.png)
7. In the **Certificate Import wizard**, click **Local Machine** and then click **Next**.
8. On the **Certificate Store** screen, click **Place all certificates in the following store** and click **Browse** to find the location where you want to place the certificate.
9. In the **Select Certificate Store** dialog, select **Trusted Root Authority Certificate** and click **OK**.
  ![click install Certificate ](./media/trusted-authority-store.png)
10. Click **Next** and then click **Finish** to import the certificate successfully.
11. Once you have added the certificate, sign into your vCenter server to verify the connection is secure.
  ![click install Certificate ](./media/secure-communication-established.png)

### Add a new user accout in VMware server

DPM uses your user name and password as credentials for communicating and authenticating with VMware server. An authenticated user has, at least the following privileges, which are required for successfully protecting a VM:

- Global.ManageCustomFields
- Network.Assign
- Datastore.AllocateSpace
- VirtualMachine.Config.ChangeTracking
- VirtualMachine.State.RemoveSnapshot
- VirtualMachine.State.CreateSnapshot
- VirtualMachine.Provisioning.DiskRandomRead
- VirtualMachine.Interact.PowerOff
- VirtualMachine.Inventory.Create
- VirtualMachine.Config.AddNewDisk
- VirtualMachine.Config.HostUSBDevice
- VirtualMachine.Config.AdvancedConfig
- VirtualMachine.Config.SwapPlacement

The recommended steps for assigning these privileges:

#### Create a role, for example, BackupAdminRole

1. In the vSphere Web Client, from the **Navigator** menu, click **Administration** > **Roles**.
2. From the **Roles provider** drop-down menu, select the vCenter Server to which the role applies.
3. On the **Roles** pane, click '+' to open the **Create Role** dialog and create a role.
  ![create a new role ](./media/create-new-role-dialog.png)
4. Name the role, **BackupAdminRole**.
5. Select the privileges (identified in the bulleted list above) for the role and click **OK**.

#### Create a new user, for example, BackupAdmin

When you create a user, that user must be in the same domain as the objects you want to protect.

1. In the vSphere Web Client, on the **Navigator** menu, click **Administration**.
2. In the **Administration** menu, click **Users and Groups**.
3. To create a new user, on the **Users** tab, click '+' to open the **New User** dialog.
4. Provide a **User name** and **password** for the role. Use BackupAdmin as the User name. Additional information is optional.

#### Assign the role, BackupAdminRole, to the user, BackupAdmin

1. In the vSphere Web Client, on the Navigator menu, click **Administration**.
2. In the Administration menu, click **Global Permissions**.
3. On the **Global Permissions** pane, click the **Manage** tab.
4. On the **Manage** tab, click '**+**' to open the **Add Permission** dialog.
5. In the **Add Permissions** dialog, click **Add**.
6. In the **Select Users/Groups** dialog, choose the correct domain from the **Domain** menu, then in the **User/Group** column select **BackupAdmin**, and click **Add**.
   The user name appears in the Users field in the format: domain\BackupAdmin.
7. Click **OK** to return to the Add Permissions dialog.
8. In the **Assigned Role** area, from the drop-down menu, select the role, **BackupAdminRole**, and click **OK**.
   The new user and role association appears in the Manage tab.

### Add a VMware server to DPM

1. In the DPM Administrator Console, click **Management** > **Production Servers** > **Add** to open the Production Server Addition Wizard.
   ![open the Production Server Addition wizard ](./media/add-production-server.png)
2. On the **Select Production Server type screen, select **VMware Servers** and click **Next**.
   ![select VMware server ](./media/add-production-server-choose-vmware.png)
3. On the **Select Computers** screen, provide the following information:
   - **Server Name/IP Address**: enter the VMware server fully qualified domain name (fQDN) or IP address.
   - **SSL Port**: select the SSL port number used to communicate with the VMware server. DPM uses Https to communicate with VMware servers over a secured connection. To successfully communicate with VMware servers, DPM requires the SSL port number configured for that VMware server. If the VMware servers are not explicitly configured with different SSL ports, continue with default port, 443.
   - **Specify Credential**: Select the credential needed to authenticate with this VMware server. If the required credential has not yet been added to DPM, choose **Add New Credential** and provide the Name, Description, User name, and Password for the credential.
    Once you have filled out the fields, click **Add** to add the server to the list of VMware Servers. If you would like to add more VMware servers to the list, repeat this step. If you are finished adding servers to the list, click **Next**.
4. On the **Summary** screen, select the server you want to add, and click **Add**.
    After adding the VMware servers to DPM, see [Configure Backup](back-up-vmware.md#configure-backup) for information about the available methods of protection.

### Disable secure communication protocol

If your organization does not want to use secure communication protocol (HTTPS), you can create a registry key to disable it. To create this registry key:

1. Copy and paste the following text into a .txt file.
    `Windows Registry Editor Version 5.00`
    `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]`
    `"IgnoreCertificateValidation"=dword:00000001`
2. Save the file with the name, **DisableSecureAuthentication.reg**, to your DPM server.
3. Double-click the file to activate the registry entry.

## Configure Backup

Once you've added the VMware server(s) to DPM, you're almost ready to start protection in DPM. However, before you begin protection, you need to allocate disk storage that DPM can use for short-term storage. For guidance on adding storage, see [Adding Storage to DPM](https://technet.microsoft.com/en-us/library/hh758075(v=sc.12).aspx). Once you have added storage, you are ready to use the **Create New Protection Group** wizard to create a protection group for the VMware VMs. 

### Folder-level protection

VMware provides VM folders that let you organize VMs as you like, whether it is based on applications to which those VMs belong, or to departments in the business.

DPM can protect individual VMs, as well as cascading levels of folders that contain VMs. Once you select a folder for protection, all folders (and VMs) within this folder are automatically detected and protected. This is called folder-level protection. DPM detects and configures protection for the VMs at 12 AM (based on the DPM server's local timezone). When DPM detects that new VMs have been created, DPM configures protection by end of that day.

### Scale-out protection of clustered VMware servers

In large VMware deployments, a single vCenter server can manage thousands of VMs. DPM supports scale-out protection of VMware server clusters. The new scale-out feature removes the limit of a one-to-one relationship between a VMware cluster and a DPM server. You can add a VM to a protection group on any of the recognized DPM servers. Please note, scale-out protection is only available for VMs hosted on servers running Windows Server 2012. Multiple DPM servers can be used to protect VMs managed by a single vCenter server. While multiple DPM servers can be used to protect VMs deployed on the same vCenter server, only one DPM server can protect a VM or folder at any given time. VMs and folders that are already protected by one DPM server cannot be selected by another DPM server. To deploy scale-out protection, there must be a minimum of two DPM servers, for example D1 and D2, which are visible to all virtual machines hosted on nodes N1, N2, N3 and N4. When protection groups on D1 or D2 are created, any of the virtual machines from V1 to V8 can be added to the DPM for protection.

 ![conceptual diagram of a scale-out farm ](./media/scale-out-protection-diagram.png)

### Backing up virtual machines to disk or cloud

DPM can back up VMware VMs to disk and to the Azure cloud. You specify the protection method while creating the new Protection Group.
For all operational recovery scenarios like accidental deletion or corruption scenarios, back up to disk. For long-term retention or offsite backup requirements, back up to cloud. See the [Azure Backup documentation](https://azure.microsoft.com/en-in/blog/new-features-in-azure-backup-long-term-retention-offline-backup-seeding-and-more/) for more information about long-term retention.

DPM provides application-consistent backups of Windows VMs and file-consistent backups of Linux VMs (provided you install VMware tools on the guest).

### Create a Protection Group for VMware VMs

1. In the Administrator Console, click **Protection**.
2. On the tool ribbon, click **New** to open the **Create New Protection Group** wizard.
3. In the **Select Protection Group Type** screen, select **Servers** and click **Next**.
   ![create new protection group ](./media/create-new-protection-group-wizard.png)
4. In the **Select Group Members** screen, expand the **Available members** folders and select the folders to protect and click **Next**.
    Once you select a folder, the member is added to the Selected members list. Note: items already protected by a DPM server cannot be selected, and will not be a member of the protection group. View the DPM server that protects an item by hovering over the item in the Available members list.
    ![select members for the new protection group ](./media/select-group-members.png)
5. On the **Select Data Protection Method** screen, type a **Protection group name**, and then select the protection method.
    For protection method, you can choose: short-term protection to a hard drive, or online protection to the cloud. Note that tape protection is not supported for VMware VMs. Once you've selected your protection method, click **Next**.
6.	On the **Specify Short-Term Goals** screen, for the **Retention Range** specify the number of days your data will be kept on disk.
    If you want to change the schedule when application recovery points are taken, click Modify. On the Express Full Backup tab, choose a new schedule for the time(s) and days of the week when Express Full Backups are taken. The default is daily at 8 PM, local time for the DPM server. When you have the short-term goals you like, click **Next**.
7. On the **Review Disk Allocation** screen, recommended disk allocations are displayed. Recommendations are based on the retention range, the type of workload and the size of the protected data. Click **Next**.
8. On the **Choose Replica Creation Method** screen, specify how the initial replication of data in the protection group will be performed. If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.
9. On the **Consistency Check Options** screen, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don’t want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the Protection area of the DPM console, and selecting Perform Consistency Check.
10. On the **Specify Online Protection Data** screen, select the data source(s) that you want to protect.
11. On the **Specify Online Backup Schedule** screen, specify how often you want to take a backup from the disk backup to Azure. A recovery point is created each time a backup is taken.
12. On the **Specify Online Retention Policy** screen, specify how long you want to retain your data in Azure. Read more about backing up DPM to Azure in the article, [Backup DPM workloads with Azure Backup](https://docs.microsoft.com/azure/backup/backup-azure-dpm-introduction).
13. On the Choose Online Replication screen, choose your method for creating your initial backup copy. The default choice is to send the initial backup copy of your data over the network. However, if you have an extremely large amount of data, it may be more timely to use the Offline Backup feature. See the Offline Backup topic in Azure for more information, including a step-by-step walkthrough.
14. On the Summary screen, review the settings. If you are interested in optimizing performance of the protection group, see the topic, [Optimizing DPM operations(https://technet.microsoft.com/en-us/library/jj628105(v=sc.12).aspx) that affect performance. Once you are satisfied with all settings for the protection group, click **Create Group** to create the protection group and trigger the initial backup copy.
    The Status screen appears and gives you an update on the creation of your protection group, and the state of your initial backup.

## Restore VMware virtual machines

This section explains how to use DPM to restore VMware VM [recovery points](https://technet.microsoft.com/en-us/library/jj627975(v=sc.12).aspx). For an overview on using DPM to recover data, see [Recover protected data](https://technet.microsoft.com/en-us/library/jj628056(v=sc.12).aspx). In the DPM Administrator Console, there are two ways to find recoverable data - search or browse. When recovering data, you may, or may not want to restore data or a VM to the same location. For this reason DPM supports three recovery options for VMware VM backups.

- **Original location recovery (OLR)** - Use OLR to restore a protected VM to its original location. You can restore a VM to its original location only if no disks have been added or deleted, since the back up occurred. If disks have been added or deleted, you must use alternate location recovery.
- **Alternate location recovery (ALR)** - When the original VM is missing, or you don't want to disturb the original VM, you can recover the VM to an alternate location. To recover a VM to an alternate location, you must provide the location of an ESXi host, resource pool, folder, and the storage datastore and path. Once the VM has been restored, to help differentiate the restored VM from the original VM, DPM appends "-Recovered" to the name of the VM.
- **Individual file location recovery (ILR)** - If the protected VM is a Windows Server VM, individual files/folders inside the VM can be recovered using DPM’s ILR capability. To recover individual files, see the procedure later in this topic.

### Restore a recovery point

1. In the DPM Administrator Console, click **Recovery** view.
2. Using the Browse pane, browse or filter to find the VM you want to recover. Once you select a VM or folder, the Recovery points for pane displays the available recovery points.
    ![open recovery points panel](./media/recovery-points-panel.png)
3. In the **Recovery points for** field, use the calendar and drop-down menus to select a date when a recovery point was taken. Calendar dates in bold have available recovery points.
4. On the tool ribbon, click **Recover** to open the **Recovery Wizard**.
   ![open Recovery wizard ](./media/recovery-wizard.png)
5. Click **Next** to advance to the **Specify Recovery Options** screen.
6. On the **Specify Recovery Options** screen, if you want to enable network bandwidth throttling, click **Modify**. To leave network throttling disabled, click **Next**. No other options on this wizard screen are available for VMware VMs.
    If you choose to modify the network bandwidth throttle, in the Throttle dialog, select **Enable network bandwidth usage throttling** to turn it on. Once enabled, configure the **Settings** and **Work Schedule**.
7. On the **Select Recovery Type** screen, choose whether to recover to the original instance, or to a new location, and click **Next**.
  - If you choose **Recover to original instance**, you don't need to make any more choices in the wizard. The data for the original instance is used.
  - If you choose **Recover as virtual machine on any host**, then on the **Specify Destination** screen, provide the information for **ESXi Host**, **Resource Pool**, **Folder**, and **Path**.
     ![open Recovery wizard ](./media/select-recovery-type.png)
8. On the **Summary** screen, review your settings and click **Recover** to start the recovery process.
The **Recovery status** screen shows the progression of the recovery operation.

### Restore an individual file from a VM

You can restore individual files from a protected VM recovery point. Note that this feature is only available for Windows Server VMs. Restoring individual files is similar to restoring the entire VM, except you browse into the VMDK and find the file(s) you want, before starting the recovery process. To recover an individual file or select files from a Windows Server VM:

1. In the DPM Administrator Console, click **Recovery** view.
2. Using the **Browse** pane, browse or filter to find the VM you want to recover. Once you select a VM or folder, the Recovery points for pane displays the available recovery points.
  ![open Recovery points ](./media/view-available-recovery-points.png)
3. In the **Recovery Points for:** pane, use the calendar to select the date that contains the desired recovery point(s).
    Depending on how the backup policy has been configured, dates can have more than one recovery point. Once you've selected the day when the recovery point was taken, make sure you've chosen the correct Recovery time. If the selected date has multiple recovery points, choose your recovery point by selecting it in the **Recovery time** drop-down menu. Once you chose the recovery point, the list of recoverable items appears in the **Path:** pane.
4. To find the files you want to recover, in the **Path** pane, double-click the item in the **Recoverable item** column to open it. Select the file, files, or folders you want to recover. To select multiple items, press the **Ctrl** key while selecting each item.
    The **Path** pane has a search box that can search the list of files or folders appearing in the **Recoverable Item** column. **Search list below** will not search into subfolders. To look through sub-folders, double-click the folder to go into it. Use the **Up** button to move from a child folder into the parent folder. You can select multiple items (files and folders), but they must be in the same parent folder. You cannot recover items from multiple folders in the same recovery job.
5. When you have selected the item(s) for recovery, in the Administrator Console tool ribbon, click **Recover** to open the **Recovery Wizard**.
    In the Recovery Wizard, the **Review Recovery Selection** screen shows the selected items to be recovered.
    ![review Recovery points ](./media/review-recovery-point-selection.png)
6. On the **Specify Recovery Options** screen, if you want to enable network bandwidth throttling, click **Modify**. To leave network throttling disabled, click **Next**. No other options on this wizard screen are available for VMware VMs.
    If you choose to modify the network bandwidth throttle, in the Throttle dialog, select **Enable network bandwidth usage throttling** to turn it on. Once enabled, configure the **Settings** and **Work Schedule**.
7. On the **Select Recovery Type** screen, click **Next**. You can only recover your file(s) or folder(s) to a network folder.
8. On the **Specify Destination** screen, click **Browse** to find a network location for your files or folders. DPM creates a folder where all recovered items will be copied. The folder name has the prefix, DPM_day-month-year. When you select a location for the recovered files or folder, the details for that location (Destination, Destination path, and available space) are provided.
    ![specify destination for files or folders ](./media/specify-destination.png)
9. On the **Specify Recovery Options** screen, choose which security setting to apply. You can opt to modify the network bandwidth usage throttling, but the default is throttling is disabled. Also, **SAN Recovery** and **Notification** are not enabled.
10.	On the **Summary** screen, review your settings and click **Recover** to start the recovery process.
    The **Recovery status screen shows the progression of the recovery operation.