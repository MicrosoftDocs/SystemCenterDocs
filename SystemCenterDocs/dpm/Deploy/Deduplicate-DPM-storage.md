ing:

-   Be conservative in volume size requirements and allow for some overprovisioning of storage. It is recommended to allow for a buffer of at least 10% when planning for backup storage usage to allow for expected variation in deduplication savings and data churn.

-   Monitor the volumes used for backup storage to ensure that space utilization and deduplication savings rates are at expected levels.

If the volume becomes full the following symptoms result:

-   The DPM virtual machine will be put into a pause-critical state and no further backup jobs can be issued by that VM.

-   All backup jobs that use the VHDX files on the full volume will fail.

To recover from this condition and restore the system to normal operation, additional storage can be provisioned and a storage migration of the DPM virtual machine or its VHDX can be performed to free up space:

1.  Stop the DPM Server that owns the VHDX files on the full backup share.

2.  Create an additional volume and backup share using the same configuration and settings as used for the existing shares, including settings for NTFS and deduplication.

3.  **Migrate Storage** for the DPM Server virtual machine, and migrate at least one VHDX file from the full backup share to the new backup share created in step 2.

4.  Run a Data Deduplication garbage collection (GC) job on the source backup share that was full. The GC job should succeed and reclaim the free space.

5.  Restart the DPM Server virtual machine.

6.  A DPM consistency check job will be triggered during the next backup window for all data sources which previously failed.

7.  All backup jobs should now succeed.

## Summary
The combination of deduplication and DPM provides substantial space savings. This allows higher retention rates, more frequent backups, and better TCO for the DPM deployment. The guidance and recommendations in this document should provide you with the tools and knowledge to configure deduplication for DPM storage and see the benefits for yourself in your own deployment.

## Common questions
**Q:** DPM VHDX files need to be 1TB of size. Does this mean DPM cannot backup a VM or SharePoint or SQL DB or file volume of size > 1TB?

**A:** No. DPM aggregates multiple volumes into one to store backups. So, the 1TB file size doesn't have any implications for data source sizes that DPM can backup.

**Q:** It looks as though DPM storage VHDX files must be deployed on remote SMB file shares only. What will happen if I store the backup VHDX files on dedup-enabled volumes on the same system where the DPM virtual machine is running?

**A:** As discussed above, DPM, Hyper-V and dedup are storage and compute intensive operations. Combining all three of them in a single system can lead to I/O and process intensive operations that could starve Hyper-V and its VMs. If you decide to experiment configuring DPM in a VM with the backup storage volumes on the same machine, you should monitor performance carefully to ensure that there is enough I/O bandwidth and compute capacity to maintain all three operations on the same machine.

**Q:** You recommend dedicated, separate deduplication and backup windows. Why can't I enable dedup while DPM is backing up? I need to backup my SQL DB every 15 minutes.

**A:** Dedup and DPM are storage intensive operations and having both of them running at the same time can be inefficient and lead to I/O starvation. Therefore, to protect workloads more than once a day (for example SQL Server every 15 minutes) and to enable dedup at the same time, ensures there's enough I/O bandwith and computer capacity to avoid resource starvation.

**Q:** Based on the configuration described, DPM needs to be running in a virtual machine. Why can't I enable dedup on replica volume and shadow copy volumes directly rather than on VHDX files?

**A:** Dedup does deduplication per volume operating on individual files. Since dedup optimizes at the file level, it is not designed to support the VolSnap technology that DPM leverages to store its backup data. By running DPM in a VM, Hyper-V maps the DPM volume operations to the VHDX file level, allowing dedup to optimize backup data and provide larger storage savings.

**Q:** The above sample configuration has created only 7.2TB volumes. Can I create bigger or smaller volumes?

**A:** Dedup runs one thread per volume. As the volume size becomes bigger, dedup requires more time to complete its optimization. On the other hand with small volumes there is less data in which to find duplicate chunks, which can result in reduced savings. So, it is advisable to fine tune the volume size based on total churn and system hardware capabilities for optimal savings. More detailed information on determining volume sizes used with deduplication can be found in Sizing volumes for Deduplication in Windows Server. For more detailed information on determining volume sizes used with deduplication see [Sizing Volumes for Data Deduplication](http://go.microsoft.com/fwlink/?LinkId=522575).



