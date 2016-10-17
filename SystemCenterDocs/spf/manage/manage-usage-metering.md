---
ms.assetid: b64a106a-93d5-4cfd-bcd6-a39462713ca3
title: Manage usage metering in SPF
description: Provides information about setting up usage metering in SPF
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/16/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
---

# Manage usage metering in SPF
>Apples To: System Center 2016

You can configure System Center 2016 - Service Provider Foundation (SPF) to aggregate usage statistics for queries by the SPF Usage web service.

## Before you start

Here's what you need:

- Servers running SPF, VMM, and Operations Manager. If needed, all these components can all be on the same computer.
- The Windows Azure Pack for Windows Server and API to provision IaaS.
- The Operations Manager server should have an Operations Manager Data Warehouse \(OMDW\) database. VMM management packs should be installed.
- A server running SQL Server with the Operations Manager Data Warehouse (OMDW).
- You can have the database for the OMDW and the database for Service Provider Foundation on the same server. Connection settings are stored in the Service Provider Foundation database.
- A Usage application pool identity credential that must be specified as a logon account to the OMDW databases. This account must have the db_DataReader and OpsMgrReader user mappings on each OMDW database. This is the same account specified for the Service Provider Foundation database.
- One or more virtual machines hosted by Hyper V (or VMM), and System Center 2016 Operations Manager themselves.

## Set up metering

Before you set up metering, check these resources:

- [Learn about the SPF cmdlets](http://technet.microsoft.com/library/jj612525.aspx).
- [Read a blog post](http://blogs.technet.com/b/privatecloud/archive/2013/10/01/configuring-spf-and-windows-azure-pack-for-iaas-usage-and-metering.aspx) about usage metering.

Then set up metering as follows:

1. Create an instance of a server \(using the **New\-SCSPFServer** cmdlet\) with the *ServerType* as OMDW.
2. Use the **New\-SCSPFSetting** cmdlet to create a setting on that server \(the one created in the previous step\), that has the connection string to OperationsManagerDW database on the OMDW server.
3. Verify that the Application Pool account under which SPF\_Usage runs has the ability to query OMDW.
4. Verify to make sure that the Windows Azure Pack calling account is a member of the SPF\_User local security group on the server that has SPFinstalled.
5. Run the **New\-SCSPFSetting** command with the parameters described in the following table.  

    |New\-SCSPFSetting Parameter|Value|  
    |-------------------------------|---------|  
    |Value|Required. Must be a database connection string.|  
    |SettingType|Required. Must be **DatabaseConnectionString**.|  
    |Name|Optional. This setting is recommended. Specify a meaningful name for each setting.|  
    |Server|Associates the setting with the sever from which usage metering is to be obtained. Must be a server object obtained from the Get\-SCSPFServer cmdlet.|  

    For example:  

    ```powershell  
    PS C:\> $omdwserver = New-SCSPFServer -Name "omdw.contoso.com" -ServerType OMDW  
    PS C:\>$setting = New-SCSPFSetting -Name mysetting -SettingType DatabaseConnectionString -Value "Server=myomdwserver\myomdwinstance;Database=OperationsManagerDW;Trusted_Connection=True;Connect Timeout=300" -Server $omdwserver  

    ```  
Use the Get\-SCSPFSetting cmdlet to make changes to a particular setting. For example, the following code associates the setting with a different server, that is stored in the `$newSvr` variable.  

```powershell  
PS C:\>$myset = Get-SCSPFSetting -Name "mySetting"  
PS C:\>$myset.Server = $newSvr  

```  

## Modify connection timeouts

The recommended connection timeout is 300 seconds, or 5 minutes. This value is also dependent on the volume of virtual machine usage metrics, SQL server edition (Enterprise recommended), hardware capacity, among other environment settings. You can change the connection timeout value using the Get-SCSPFSetting cmdlet
