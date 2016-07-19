---
title: How to Enable Audit Collection Services (ACS) Forwarders
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46223bea-3f73-44ab-832a-e13d0fe9f370
author:mgoedtel
manager:cfreemanwa
---
# How to Enable Audit Collection Services (ACS) Forwarders
Depending on your auditing needs, you might have several hundred to thousands of computers from which you want to collect audit events. By default, the service needed for an agent to be an Audit Collection Services \(ACS\) forwarder is installed but not enabled when the Operations Manager agent is installed. After you install the ACS collector and database you can then remotely enable this service on multiple agents through the Operations Manager console by running the **Enable Audit Collection** task.  
  
This procedure should be run after the ACS collector and database are installed and can only be run against computers that already have the Operations Manager agent installed. In addition, the user account that runs this task must belong to the local Administrators group on each agent computer.  
  
### To enable audit collection on Operations Manager agents  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role. This account must also have the rights of a local administrator on each agent computer that you want to enable as an ACS forwarder.  
  
2.  In the Operations console, click **Monitoring**.  
  
3.  In the navigation pane, expand **Operations Manager**, expand **Agent Details**, and then click **Agent Health State**. This view has two panes, and the actions in this procedure are performed in the right pane.  
  
4.  In the details pane, click all agents that you want to enable as ACS forwarders. You can make multiple selections by pressing CTRL or SHIFT.  
  
5.  In the **Actions** pane, under **Health Service Tasks**, click **Enable Audit Collection** to open the **Run Task \- Enable Audit Collection** dialog box.  
  
6.  In the **Task Parameters** section, click **Override** to open the **Override Task Parameters** dialog box.  
  
7.  In the **Override the task parameters with the new values** section, click the *CollectorServer* parameter; in the **New Value** column, type the FQDN of the ACS collector; and then click **Override**.  
  
    > [!NOTE]  
    > If you are enabling ACS on a gateway or management server and you do not specify the *CollectorServer* parameter, the task will fail with a “Type Mismatch Error.” To avoid this, provide a value for the override.  
  
8.  In the **Task credentials** section, click **Other**. In the **User Name** box, type the name of a user account that belongs to the local Administrators group on the agent computers. In the **Password** box, type the password for this user account. Click to expand the **Domain** list to view the available domains, and then click the domain of the user account.  
  
9. Click **Run Task**. The **Task Status** dialog box displays tracking the progress of the task.  
  
10. When the task completes successfully, click **Close**.  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[How to Configure Certficates for ACS Collector and Forwarder](../../om/manage/How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[How to Enable Event Logging and ACS Rules on Solaris and AIX Computers](../../om/manage/How-to-Enable-Event-Logging-and-ACS-Rules-on-Solaris-and-AIX-Computers.md)  
[How to Filter ACS Events for UNIX and Linux Computers](../../om/manage/How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[How to Remove Audit Collection Services &#40;ACS&#41;](../../om/manage/How-to-Remove-Audit-Collection-Services--ACS-.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
