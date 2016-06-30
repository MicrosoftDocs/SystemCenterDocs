t isn't start it.

    2.  Open Microsoft SQL Server Management Studio and connect to the instance that hosts the DPM database (DPMDB). On DPMDB run the following query: `SELECT TOP 1000 [PropertyName] ,[PropertyValue] FROM[DPMDB].[dbo].[tbl_DLS_GlobalSetting]`

        This query contains a property, called `KnownVMMServer`. This value should be the same as the value that you provided with the `Set-DPMGlobalProperty` cmdlet.

    3.  Run the following query to validate the *VMMIdentifier* parameter in the `PhysicalPathXML` for a particular virtual machine. Replace `VMName` with the name of the virtual machine.

        `select cast(PhysicalPath as XML) from tbl_IM_ProtectedObject where DataSourceId in (select datasourceid from tbl_IM_DataSource where DataSourceName like '%<VMName>%')`

    4.  Open the .xml file that this query returns and validate that the *VMMIdentifier* field has a value.

**Run manual migration**-After you've completed the steps migration is enabled after the DPM Summary Manager job runs. By default, this job starts at midnight and runs every morning. If you want to run a manual migration in the meantime to check everything is working as expected, do the following:

1.  Open SQL Server Management Studio and connect to the instance that hosts DPMDB.

2.  Run the following query: `select * from tbl_SCH_ScheduleDefinition where JobDefinitionID='9B30D213-B836-4B9E-97C2-DB03C3EB39D7'`. Note that the query returns the **ScheduleID**.

3.  In SQL Server Management Studio, expand **SQL Server Agent**, and then expand **Jobs**. Right-click the **ScheduleID** that you noted, and select **Start Job at Step**.

Note that backup performance is affected when the job runs. The size and scale of your deployment determines how much time the job takes to finish.

## <a name="BKMK_Replica"></a>Back up replica virtual machines
You can back up replica virtual machines on a secondary server if DPM is running Windows Server 2012 R2. This is useful for a couple of reasons:

-   Reduces the impact of backups on running workload-Taking a backup of a virtual machine incurs some overhead as a snapshot is created. By offloading the backup process to a secondary remote site, the running workload is no longer impacted by the backup operation. Obviously this is applicable only to deployments where the backup copy is stored on a remote site. For example, you might take daily backups and store data locally to ensure quick restore times, but take monthly or quarterly backups from replica virtual machines stored remotely for long-term retention.

-   Saves bandwidth-In a typical remote branch office/headquarters deployment you'll need an appropriate amount of bandwidth is provisioned by administrators to transfer backup data between sites. If you deploy some type of replication and failover strategy in addition to your data backup strategy, you might be sending copies of the same data over the network. By backing up the replica virtual machine data rather than the primary you'll save the overhead of sending that backed up data over the network.

-   Enables hoster backup-Customers might use a datacenter hosted by a hoster as a replica site, with no secondary datacenter of their own. In this case the hoster SLA will require consistent backup of replica virtual machines.

A replica virtual machine is  turned off until a failover is initiated, and VSS can't guarantee an application-consistent backup for a replica virtual machine. Thus the backup of a replica virtual machine will be crash-consistent only. If crash- consistency can't be guaranteed then the backup will fail and this might occur in a number of conditions:

-   The replica virtual machine isn't healthy and is in a critical state.

-   The replica virtual machine is resynchronizing (in the Resynchronization in Progress or Resynchronization Required state).

-   Initial replication between the primary and secondary site is in progress or pending for the virtual machine.

-   .hrl logs are being applied to the replica virtual machine, or a previous action to apply the .hrl logs on the virtual disk failed, or was cancelled or interrupted.
    .

-   Migration or failover of the replica virtual machine is in progress

## Recover backed up virtual machines
You can recover backed up virtual machines. In the DPM Administrator console you select the virtual machine, and specify the point from which you want to recover the data. In the Recovery Wizard you select recovery settings:

1.  Select the VMs you want to recover and on the calendar, click any date to see the recovery points available. Select the recovery point you want to use on the **Recovery time** menu. Then in **Actions** click **Recover**. Select where you want to restore the data.

    -   **Recover to original location**: When you recover to the original location the original VHD is deleted.  DPM will recover the VHD and other configuration files on the original location using Hyper-V VSS writer. At the end of the recovery process, virtual machines will still be highly available.
        The resource group must be present for recovery. If it isn't available recover to an alternate location and then make the virtual machine highly available.

    -   **Recover to alternate location**: DPM supports alternate location recovery (ALR), which provides a seamless recovery of a protected Hyper-V virtual machine to a different Hyper-V host, independent of processor architecture. Hyper-V virtual machines that are recovered to a cluster node will not be highly available.

    -   **Item-level recovery**: DPM supports item-level recovery (ILR), which allows you to do item-level recovery of files, folders, volumes, and virtual hard disks (VHDs) from a host-level backup of Hyper-V virtual machines to a network share or a volume on a DPM protected server. The DPM protection agent doesn't have to be installed inside the guest to perform item-level recovery.

In **Specify Recovery Options** you can configure the recovery options for SAN, network bandwidth usage throttling if you're recovering over low bandwidth, and email notifications to specify when the restore job finishes, and complete the wiard.



