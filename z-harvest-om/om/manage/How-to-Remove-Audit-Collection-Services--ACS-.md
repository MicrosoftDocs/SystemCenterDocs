---
title: How to Remove Audit Collection Services (ACS)
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce23ebff-79b3-4675-a9f2-7179a933de44
author:mgoedtel
manager:cfreemanwa
---
# How to Remove Audit Collection Services (ACS)
Each component of [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] Audit Collection Services \(ACS\) has a separate procedure for removing it.  
  
The ACS collector is removed by using the Audit Collection Services Collector Setup wizard. When you remove the ACS collector, the ACS database is not deleted. You delete the ACS database from within Microsoft SQL Server.  
  
To delete the ACS database you must be a member of the SQL Admins group or have the right to delete a database delegated to you. You must also have read access to the ACS database. As a best practice for security, consider using Run as to perform this procedure.  
  
Because service for the ACS forwarder is part of the Operations Manager agent, you can either disable service for the ACS forwarder and keep the Operations Manager agent or uninstall the agent from the computer. If you do not need to monitor the computer after it is removed from an ACS deployment, you should uninstall the Operations Manager agent. If you want to monitor other services or applications on the computer even though it is no longer acting as an ACS forwarder, you can disable service for the ACS forwarder.  
  
### To remove an ACS collector  
  
1.  Insert the Operations Manager CD in the management server that you selected to be the ACS collector.  
  
2.  On the root of the CD, double\-click **SetupOM.exe**. In the **Install** section, click **Audit collection services**. The Audit Collection Services Collector Setup wizard starts.  
  
3.  On the **Welcome** page click **Next**.  
  
4.  On the ACS Collector Maintenance page, click **Remove the ACS collector** and then click **Next**.  
  
5.  On the **Summary** page, the wizard lists the actions it performs to remove the ACS collector. Review the list and click **Next**.  
  
6.  When the removal of the ACS collector is complete, click **Finish**.  
  
### To delete an ACS database  
  
1.  Click **Start**, point to **All Programs**, point to **SQL Enterprise Manager**, and click **Query Analyzer**.  
  
2.  In the console tree, right\-click the name of the ACS database that you want to remove, click **Delete**, and then click **OK**.  
  
### To disable ACS forwarders  
  
1.  Log on to the computer with an account that has the rights of the Operations Manager Administrator Operator role. This account must also have the rights of a local administrator on each ACS forwarder.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  If you already have already created a state view for ACS, you can skip this step. Right\-click in the Monitoring navigation pane, point to **New**, and then click **State View**.  
  
4.  In **Name**, type a descriptive name, such as ACS Forwarders, and a short description in **Description**.  
  
5.  If necessary, click the **Criteria** tab. In **Show data related to**, click **Agent** and then click **OK**.  
  
6.  In the **Actions** pane, under **Health Service Tasks**, click **Disable Audit Collection**. The **Run Task \- Enable Audit Collection** dialog box displays.  
  
7.  In the **Specify the credentials you want to run the task with** section, click **Other**. In the **User Name** box, type the name of a user account that belongs to the local Administrators group on the agent computers. In the **Password** box, type the password for this user account. Click to expand the **Domain** drop\-down list to view the available domains, and then click the domain of the user account.  
  
8.  Click **Run Task**. The Task Status dialog box displays tracking the progress of the task.  
  
9. When the task completes successfully, click **Close**.  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[How to Configure Certficates for ACS Collector and Forwarder](../../om/manage/How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[How to Filter ACS Events for UNIX and Linux Computers](../../om/manage/How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
