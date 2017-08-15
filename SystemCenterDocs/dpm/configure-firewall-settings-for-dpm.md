---
title: Configure firewall settings for DPM
description: This article explains how to configure firewall settings for various DPM installations.
author: markgalioto
manager: carmonm
ms.date: 08-15-2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: data-protection-manager
ms.topic: article
---

# Configure firewall settings in DPM

>Applies To: System Center 2016 - Data Protection Manager

A common question that arises during Data Protection Manager (DPM) server and DPM agent deployment concerns which ports have to be opened on the firewall. This article introduces the firewall ports and protocols that DPM uses for network traffic. For more information about firewall exceptions for DPM clients, go to: [Configure firewall exceptions for the agent](../Topic/Configure%20firewall%20exceptions%20for%20the%20agent.md).  
  
|Protocol|Port|Details|  
|--------------|----------|-------------|  
|DCOM|135/TCP Dynamic|DCOM is used by the DPM server and the DPM protection agent to issue commands and responses. DPM issues commands to the protection agent by invoking DCOM calls on the agent. The protection agent responds by invoking DCOM calls on the DPM server.<br /><br /> TCP port 135 is the DCE endpoint resolution point that is used by DCOM. By default, DCOM assigns ports dynamically from the TCP port range of 1024 through 65535. However, you can use Component Services to adjust the TCP port range. To do this, follow these steps:<br /><br /> 1.  In IIS 7.0 Manager, in the **Connections** pane, click the server-level node in the tree.<br />2.  In the list of features, double-click the **FTP Firewall Support** icon.<br />3.  Enter a range of values for the **Data Channel Port Range** for your FTP service.<br />4.  In the **Actions** pane, click **Apply** to save your configuration settings.|  
|TCP|5718/TCP<br /><br /> 5719/TCP|The DPM data channel is based on TCP. Both DPM and the protected computer initiate connections to enable DPM operations such as synchronization and recovery. DPM communicates with the agent coordinator on port 5718 and with the protection agent on port 5719.|  
|TCP|6075/TCP|Enabled when you create a protection group to help protect client computers. Required for end-user recovery.<br /><br /> An exception in Windows Firewall (DPMAM_WCF_Service) is created for the program Amscvhost.exe when you enable Central Console for DPM in Operations Manager.|  
|DNS|53/UDP|Used for host name resolution between DPM and the domain controller, and between the protected computer and the domain controller.|  
|Kerberos|88/UDP<br /><br /> 88/TCP|Used for authentication of the connection endpoint between DPM and the domain controller, and between the protected computer and the domain controller.|  
|LDAP|389/TCP<br /><br /> 389/UDP|Used for queries between DPM and the domain controller.|  
|NetBios|137/UDP<br /><br /> 138/UDP<br /><br /> 139/TCP<br /><br /> 445/TCP|Used for miscellaneous operations between DPM and the protected computer, between DPM and the domain controller, and between the protected computer and the domain controller. Used for DPM functions for Server Message Block (SMB) when it is directly hosted on TCP/IP.|  
  
##  <a name="BKMK_WF"></a> Windows Firewall settings  
 If Windows Firewall is enabled when you install DPM, the DPM setup configures the Windows Firewall settings as required together with the rules and exceptions. The settings are summarized in the following table.  
  
 Note:  
  
-   If you’re looking for information about how to set up firewall exceptions for computers that DPM helps protect, see [Configure firewall exceptions for the agent](../Topic/Configure%20firewall%20exceptions%20for%20the%20agent.md).  
  
-   If Windows Firewall wasn’t available when you installed DPM, see [How to configure Windows Firewall manually](#BKMK_Manual).  
  
-   If you’re running the DPM database on a remote instance of SQL Server, you’ll have to set up several firewall exceptions on the remote instance of SQL Server. See [Set up Windows Firewall on the remote instance of SQL Server](#BKMK_SQL).  
  
|Rule name|Details|Protocol|Port|  
|---------------|-------------|--------------|----------|  
|Microsoft System Center 2012 Data Protection Manager DCOM Setting|Required for DCOM communications between the DPM server and protected computers.|DCOM|135/TCP Dynamic|  
|Microsoft System Center 2012 Data Protection Manager|Exception for Msdpm.exe (the DPM service). Runs on the DPM server.|All protocols|All ports|  
|Microsoft System Center 2012 Data Protection Manager Replication Agent|Exception for Dpmra.exe (protection agent service that is used to back up and restore data). Runs on the DPM server and protected computers.|All protocols|All ports|  
  
###  <a name="BKMK_Manual"></a> How to configure Windows Firewall manually  
  
1.  In Server Manager, select **Local Server** > **Tools** > **Windows Firewall with Advanced Security**.  
  
2.  In the **Windows Firewall with Advanced Security** console, verify that Windows Firewall is on for all profiles, and then click **Inbound Rules**.  
  
3.  To create an exception, in the **Actions** pane, click **New Rule** to open the **New Inbound Rule** Wizard.  
  
     On the **Rule Type** page, verify that **Program** is selected, and then click **Next**.  
  
4.  Configure exceptions to match the default rules that would have been created by DPM Setup if Windows Firewall had been enabled when DPM was installed.  
  
    1.  To manually create the exception that matches the default Microsoft System Center 2012 R2 Data Protection Manager rule on the **Program** page, click **Browse** for the **This program path** box, and then browse to **<system drive letter\>:\Program Files\Microsoft DPM\DPM\bin** > **Msdpm.exe** > **Open**> **Next**.  
  
         On the Action page leave the default setting of **Allow the connection**, or change the settings according to your organization’s guidelines > **Next**.  
  
         On the **Profile** page, leave the default settings of **Domain**, **Private**, and **Public**, or change the settings according to your organization’s guidelines > **Next**.  
  
         On the **Name** page, type a name for the rule and optionally a description > **Finish**.  
  
    2.  Now follow the same steps to manually create the exception that matches the default Microsoft System Center 2012 R2 Data Protection Replication Agent rule by browsing to **<system drive letter\>:\Program Files\Microsoft DPM\DPM\bin**, and selecting **Dpmra.exe**.  
  
     Be aware that if you’re running System Center 2012 R2 with SP1 the default rules will be named by using **Microsoft System Center 2012 Service Pack 1 Data Protection Manager**.  
  
##  <a name="BKMK_SQL"></a> Set up Windows Firewall on the remote instance of SQL Server  
  
-   If you use a remote instance of SQL Server for your DPM database, as part of the process, you’ll have to configure Windows Firewall on that remote instance of SQL Server.  
  
-   After the SQL Server installation is complete, the TCP/IP protocol should be enabled for the DPM instance of SQL Server together with the following settings:  
  
    -   Default failure audit  
  
    -   Enabled password policy checking  
  
-   Configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server to allow TCP on port 80. The report server listens for HTTP requests on port 80.  
  
-   The default instance of the database engine listens on TCP port 1443. This setting can be changed. To use the SQL Server Browser service to connect to instances that don’t listen on the default 1433 port, you’ll need UDP port 1434.  
  
-   By default, a named instance of SQL Server uses Dynamic ports. This setting can be changed.  
  
-   You can see the current port number that is being used by the database engine in the SQL Server error log. You can view error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under **Management – SQL Server Logs** in the entry “Server is listening on [‘any’ <ipv4\> port_number].”  
  
     You’ll have to enable remote procedure call (RPC) on the remote instance of SQL Server.