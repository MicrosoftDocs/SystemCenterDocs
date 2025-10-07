---
title: Manage usage metering in SPF
description: Provides information about setting up usage metering in SPF
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/20/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: service-provider-foundation
ms.custom:
  - UpdateFrequency2
  - engagement-fy24
  - sfi-ropc-nochange
---

# Manage usage metering in SPF



You can configure System Center - Service Provider Foundation (SPF) to aggregate usage statistics for queries by the SPF Usage web service.

## Before you start

Here's what you need:

- Servers running SPF, VMM, and Operations Manager. If needed, all these components can be on the same computer.
- The Windows Azure Pack for Windows Server and API to provision IaaS.
- The Operations Manager server should have an Operations Manager Data Warehouse(OMDW) database. VMM management packs should be installed.
- A server running SQL Server with the Operations Manager Data Warehouse (OMDW).
- You can have the database for the OMDW and the database for Service Provider Foundation on the same server. Connection settings are stored in the Service Provider Foundation database.
- A Usage application pool identity credential that must be specified as a sign-in account to the OMDW databases. This account must have the db_DataReader and OpsMgrReader user mappings on each OMDW database. This is the same account specified for the Service Provider Foundation database.
- One or more virtual machines hosted by Hyper V (or VMM), and System Center Operations Manager.

## Set up metering

Before you set up metering, check these resources:

- [Learn about the SPF cmdlets](/powershell/module/spfadmin/set-scspftenant).
- [Read a blog post](/archive/blogs/privatecloud/configuring-spf-and-windows-azure-pack-for-iaas-usage-and-metering) about usage metering.

Then set up metering as follows:

1. Create an instance of a server \(using the `New\-SCSPFServer` cmdlet\) with the *ServerType* as OMDW.
2. Use the `New\-SCSPFSetting` cmdlet to create a setting on that server (the one created in the previous step) that has the connection string to OperationsManagerDW database on the OMDW server.
3. Verify that the Application Pool account under which SPF\_Usage runs has the ability to query OMDW.
4. Verify that the Windows Azure Pack calling account is a member of the SPF\_User local security group on the server that has SPFinstalled.
5. Run the `New\-SCSPFSetting` command with the parameters described in the following table: 

    |New\-SCSPFSetting Parameter|Value|  
    |-------------------------------|---------|  
    |Value|Required. Must be a database connection string.|  
    |SettingType|Required. Must be **DatabaseConnectionString**.|  
    |Name|Optional. This setting is recommended. Specify a meaningful name for each setting.|  
    |Server|Associates the setting with the server from which usage metering is to be obtained. Must be a server object obtained from the Get\-SCSPFServer cmdlet.|  

    For example:  

    ```powershell  
    PS C:\> $omdwserver = New-SCSPFServer -Name "omdw.contoso.com" -ServerType OMDW  
    PS C:\>$setting = New-SCSPFSetting -Name mysetting -SettingType DatabaseConnectionString -Value "Server=myomdwserver\myomdwinstance;Database=OperationsManagerDW;Trusted_Connection=True;Connect Timeout=300" -Server $omdwserver  

    ```  
Use the Get\-SCSPFSetting cmdlet to make changes to a particular setting. For example, the following code associates the setting with a different server that is stored in the `$newSvr` variable.  

```powershell  
PS C:\>$myset = Get-SCSPFSetting -Name "mySetting"  
PS C:\>$myset.Server = $newSvr  

```  

## Modify connection timeouts

The recommended connection timeout is 300 seconds or 5 minutes. This value is also dependent on the volume of virtual machine usage metrics, SQL server edition (Enterprise recommended), and hardware capacity, among other environment settings. You can change the connection timeout value using the `Get-SCSPFSetting` cmdlet.
