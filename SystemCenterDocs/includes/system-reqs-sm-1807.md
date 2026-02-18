---
title: include file
description: include file to describe the hardware, software, and other system requirements Service Manager 1807.
ms.custom: na
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 05/14/2019
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: include
ms.assetid: 87d03428-968d-4036-8d1c-8064900756cb
ms.update-cycle: 1095-days
---

## System requirements for System Center 1807 - Service Manager

The following sections describe the general performance and scalability guidance for SM 1807, and recommend the  hardware configurations for various workloads. Because System Center 1807 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.  

## Capacity limits for Service Manager

Read [Configurations for deployment scenarios](../scsm/deploy-topo-scenarios.md) to learn about the tested capacity limits of Service Manager.

## Supported coexistence

To help simplify upgrades, you can use Service Manager 1807 connectors with the following  System Center components.

- System Center 2012 R2/2016 Virtual Machine manager
- System Center 2012 R2/2016 Orchestrator
- System Center 2012 R2/2016 Operations Manager
- System Center 2012 R2/2016 Configuration Manager
- System Center Configuration Manager CB releases - 1511, 1602, 1606, 1710, 1802, 1806, and 1810

## Hardware

|Servers|Processor (min)|Processor (rec)|RAM (min)|RAM (rec)|Hard drive space (min)|Hard drive space (rec)|
|---------------------------------|---------------------|---------------------|---------------|---------------|----------------------------|----------------------------|
|**Service Manager** Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|8 GB|10 GB|10 GB|
|**Service Manager** Database|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|80 GB|80 GB|
|**Service Manager** Data Warehouse Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|16 GB|10 GB|10 GB|
|**Service Manager** Data Warehouse Databases|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|400 GB|400 GB|
|**Service Manager** Console|2-Core 2 GHz CPU|2-Core 2 GHz CPU|4 GB|4 GB|10 GB|10 GB|
|**Service Manager** Self-Service Portal (standalone)|4-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|16 GB|80 GB|80 GB|
|**Service Manager** Self-Service Portal + Secondary Management Server (Recommended)|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|16 GB|32 GB|80 GB|80 GB|

## Software requirements

|Component| Requirement|  
|---|---|  
|**Service Manager management server**|The management server needs: [ADO.NET Data Services Update for .NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22) for Windows Server; SQL Server Native client; Microsoft Report Viewer Redistributable, which is available with the Service Manager media.<br/><br/> The management server must be installed on a 64\-bit edition of Windows. |  
|**Data warehouse management server**|The warehouse management server requires: SQL Server Native client<br/><br/> The data warehouse management server must be installed on a 64\-bit edition of Windows.|  
|**Service Manager/data warehouse databases**|The Service Manager or data warehouse databases require:  SQL Server Reporting Services \(SSRS\); SQL Server Analysis Management Objects.<br/><br/> The SQL Server and Analysis Services collation settings must be the same for the computers hosting the Service Manager database, data warehouse database, analysis services database, and Reporting Services database.|  
|**Service Manager console**|The console requires: Microsoft Report Viewer Redistributable (available on System Center media): Microsoft Excel in order to view OLAP data cubes on the console computer;  ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server; SQL Server Analysis Management Objects.<br/><br/> The console can be installed on both 32\-bit and 64\-bit editions of Windows.|  
|**Self-Service portal**|The Self-Service Portal server requires: Windows 2012 R2 server or later; the IIS role and ASP.NET 4.5 enabled; SQL Server Analysis Management Objects.<br/><br/>  Join the server machine to the same domain where the Service Manager SDK Service is running. Ideally, on the primary or secondary server.
|**Machines using self-service**|The Self Service portal needs a screen resolution above 1024 X 768.<br/><br/> Supported browsers: Microsoft Edge; Microsoft Internet Explorer 10 and 11; Mozilla Firefox 42 and later; Google Chrome 46 and later.|  
|**SQL Server Reporting Services**|In a deployment topology where the computer hosting SSRS isn't on the same computer that hosts the data warehouse management server, you've to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. [Learn about](../scsm/config-remote-ssrs.md) the manual steps.


### Additional notes

- **Operations Manager** - Service Manager has the capability to import alerts and configuration items from an Operations Manager environment. [Read about](../scsm/om-considerations.md) installing both Service Manager and Operations Manager in the same environment. You can create a data mart for Operations Manager.

- **Configuration Manager** - Service Manager can import configuration items from a Configuration Manager environment.

- **Network requirements** - To view external content from within knowledge articles, computers that host the Service Manager console must have Internet access, either directly or through a proxy server.  

- **SMTP server**- You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.  

- **Windows safe mode**- Service Manager doesn't operate and the services used by Service Manager don't start if Windows Server is running in safe mode. If you attempt to start the Service Manager services manually while in safe mode, the services fail to start and an error is written into the event log.  

## SQL Server requirements

 Microsoft SQL Server hosts the databases that System Center - Service Manager creates. In addition, System Center 1807 - Service Manager requires SQL Server Analysis Services (SSAS) to work with Microsoft Online Analytical Processing (OLAP) cubes. SQL Server Reporting Services (SSRS) is required to support System Center 1807 - Service Manager reporting.

 Use this information to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center 1807. Use this information whether you're deploying one or multiple components of System Center.


### SQL Server version support

> [!NOTE]
> For the supported versions of SQL, use the service packs that are currently in support by Microsoft.


**Service Manager** | **SQL Server 2012** | **SQL Server 2014 and [SPs](/lifecycle/products/?terms=SQL+Server+2014)**  | **SQL Server 2016 and [SPs](/lifecycle/products/?terms=SQL+Server+2016)** | **SQL Server [2017](/lifecycle/products/?terms=SQL+Server+2017)**
--- | --- | --- | --- | ---
**Service Manager/Data Warehouse database** | | &#8226;| &#8226; | &#8226;



  > [!NOTE]
  > System Center 1807 - Service Manager doesn't support the *MultiSubnetFailover* parameter. This parameter isn't used in System Center 1807 - Service Manager connection strings.

### Allow updates

 To either install or upgrade System Center 1807 - Service Manager, computers running SQL Server that host databases must be configured to allow updates. If updates aren't allowed, System Center 1807 - Service Manager Setup won't complete and the following error message will appear at the **Create database** stage of the installation:

 *An error occurred while executing a customer action: _ExecuteSqlScripts. This upgrade attempt has failed before permanent modifications were made. Upgrade has successfully rolled back to the original state of the system. Once the corrections are made, you can retry the upgrade for this role.*

 You can check the status of **allow updates** on SQL Server by executing the following stored procedure from within SQL Server Management Studio:

 ```
 sp_configure 'allow updates'
 ```

 In the results table, examine the value for "run_value". If the value of "run value" is 1, set it back to 0 with the following stored procedure, and then run Setup again.

 ```
 sp_configure 'allow updates',0 reconfigure with override
 ```

### AlwaysOn Availability Groups considerations for Service Manager databases

 SQL Server AlwaysOn Availability Groups functionality is supported by System Center 1807 - Service Manager.

 For more information about installing Service Manager with AlwaysOn availability groups, [refer here](../scsm/sql-always-on.md).

## Upgrade to SQL 2017

The following steps provide information about upgrading to SQL 2017.

 > [!NOTE]  
 > - With SM 1807, SQL 2017 is supported only if it's upgraded from SQL 2016. Fresh installation of SQL 2017 with SM 1807 isn't supported.
 > -	Users with SM 1801 deployment and SQL 2016 need to apply SM 1807 and then upgrade to SQL 2017.
 > -	Upgrade process to SQL 2017 uninstalls the reporting services; ensure to migrate required reports such as backup reporting DB and encryption keys.

 **Use the following steps to upgrade from SQL 2016 to 2017**:

1. Upgrade to SQL 2017.
2. Install SQL 2017 reporting services (SSRS), and launch the reporting services configuration manager to use the existing reporting DB, restore encryption keys.  Configure the Web service URL and Web portal URL.
3. Use the same values for reporting server Web service virtual directory and Web portal URL that you had before initiating the upgrade process for SQL 2017.      
4. Configure the SSRS as per the details shared [here](../scsm/prepare-remote-ssrs.md).
5. [**Optional**] To enable CLR strict security, run the following script on each of the service manager databases.

   By default, CLR strict security is disabled after you upgrade to SQL 2017.

   ```
   -- Do this only for SQL server version 2017 and more
   IF( convert(int, SERVERPROPERTY('ProductMajorVersion')) > 13 )
   BEGIN
   DECLARE @Hash1 BINARY(64), @ClrName1 NVARCHAR(4000);
   set @Hash1 = HASHBYTES(N'SHA2_512', 0x4d5a90000300000004000000ffff0000b800000000000000400000000000000000000000000000000000000000000000000000000000000000000000800000000e1fba0e00b409cd21b8014ccd21546869732070726f6772616d2063616e6e6f742062652072756e20696e20444f53206d6f64652e0d0d0a2400000000000000504500004c010300cdef7c440000000000000000e0000e210b010800000c000000080000000000005e2b000000200000004000000000ec560020000000020000040000000000000004000000000000000080000000020000f2f10000030000040000100000100000000010000010000000000000100000000000000000000000042b000057000000004000001005000000000000000000000000000000000000006000000c0000008c2a00001c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000080000000000000000000000082000004800000000000000000000002e74657874000000640b000000200000000c000000020000000000000000000000000000200000602e72737263000000100500000040000000060000000e0000000000000000000000000000400000402e72656c6f6300000c0000000060000000020000001400000000000000000000000000004000004200000000000000000000000000000000402b0000000000004800000002000500082100008409000009000000000000000000000000000000502000008000000000000000000000000000000000000000000000000000000000000000000000000c506f2ef337d14f0bc66e27fa02006623253f6655697a25078f76132dfd4cf9ec02d54581a9310a12538c2a82f19f230bbe2ac6017a095a82147a15f65488b5b38c9612cfc2c228f748d5519b4981a836189698e99b7f54961091fbb404afb93ab9d8110f22652ab16e7ff50f9dfb4236d78f61e93555018ba85d95c28cb5452a02281000000a0000002a00133003001e00000001000011000214fe0116fe010b072d0500160a2b0b02031e281200000a0a2b00062a000042534a4201000100000000000c00000076322e302e35303732370000000005006c0000001c020000237e0000880200003c03000023537472696e677300000000c40500000800000023555300cc050000100000002347554944000000dc050000a803000023426c6f620000000000000002000001471502000900000000fa0133001600000100000014000000020000000200000002000000120000000e00000001000000010000000300000000000a00010000000000060084007d000600c900aa000600d700aa000600fd00eb0006001601eb0006003101eb0006005001eb0006006d01eb0006008401eb0006009f01eb000600b801eb000600d101eb000600ee01eb0006001a0207023b002e02000006005d023d0206007d023d020a00df02c4020e00210302030e00270302030000000001000000000001000100010110002b004600050001000100d0200000000081188b000a000100dc2000000000960091000e00010000000100f40200000200fa0211008b00140019008b00190021008b00140029008b00140031008b00140039008b00140041008b00140049008b00140051008b00140059008b00140061008b00140069008b00140071008b001e0081008b00240089008b000a0009008b000a0091008b000a009900340336022e003b00ac022e000b0043022e0013006d022e0023006d022e002b006d022e00330073022e0053004a032e004300e4022e004b0025032e006b0075032e007b0087032e005b0065032e0073007e0340008b00cb003e020480000006000000f50f00000100000029009b02000002000000000000000000000001007400000000000200000000000000000000000100b8020000000002000000000000000000000001007d00000000000000003c4d6f64756c653e004d6963726f736f66742e4d6f6d2e446174614163636573732e53716c2e646c6c00526567756c617245787072657373696f6e4576616c7561746f72004d6963726f736f66742e456e74657270726973654d616e6167656d656e742e446174614163636573732e53716c006d73636f726c69620053797374656d004f626a656374002e63746f72004d617463686573526567756c617245787072657373696f6e0053797374656d2e52756e74696d652e496e7465726f705365727669636573004775696441747472696275746500436f6d56697369626c654174747269627574650053797374656d2e5265666c656374696f6e00417373656d626c7943756c7475726541747472696275746500417373656d626c7954726164656d61726b41747472696275746500417373656d626c79436f6e66696775726174696f6e41747472696275746500417373656d626c794465736372697074696f6e41747472696275746500417373656d626c795469746c6541747472696275746500417373656d626c79436f7079726967687441747472696275746500417373656d626c7950726f6475637441747472696275746500417373656d626c79436f6d70616e7941747472696275746500417373656d626c7946696c6556657273696f6e41747472696275746500417373656d626c7956657273696f6e4174747269627574650053797374656d2e446961676e6f73746963730044656275676761626c6541747472696275746500446562756767696e674d6f6465730053797374656d2e52756e74696d652e436f6d70696c6572536572766963657300436f6d70696c6174696f6e52656c61786174696f6e734174747269627574650052756e74696d65436f6d7061746962696c697479417474726962757465004d6963726f736f66742e4d6f6d2e446174614163636573732e53716c0053797374656d2e44617461004d6963726f736f66742e53716c5365727665722e5365727665720053716c46756e6374696f6e41747472696275746500696e707574007061747465726e0053797374656d2e546578742e526567756c617245787072657373696f6e730052656765780052656765784f7074696f6e730049734d61746368000003200000000000a79e22af2016204a81c804d4f9bce8010008b77a5c561934e08903200001050002020e0e042001010e042001010205200101113d042001010880a000240000048000009400000006020000002400005253413100040000010001004ddb14fd25fa54ef1fe05516d69c0bb19c86956e2d5245e728300417e6a018daac56b61ee215e4c096dba942368bb4aa76956042bb3efb709cda847d7396839f57a40b90829fe5f347a5d2e2c198367cbc1092aa9762ae9776e59fed16703887329ffeb6d6cbf44853c496a22bc79bb3ce00f29760995dafa6aa97779983e0b48169010005005455794d6963726f736f66742e53716c5365727665722e5365727665722e446174614163636573734b696e642c2053797374656d2e446174612c2056657273696f6e3d322e302e302e302c2043756c747572653d6e65757472616c2c205075626c69634b6579546f6b656e3d623737613563353631393334653038390a446174614163636573730000000054020f497344657465726d696e69737469630154020949735072656369736501540e044e616d651b666e5f4d617463686573526567756c617245787072657373696f6e54557f4d6963726f736f66742e53716c5365727665722e5365727665722e53797374656d446174614163636573734b696e642c2053797374656d2e446174612c2056657273696f6e3d322e302e302e302c2043756c747572653d6e65757472616c2c205075626c69634b6579546f6b656e3d623737613563353631393334653038391053797374656d4461746141636365737300000000070003020e0e115104070202022901002433333532323533352d393332652d346130342d623965302d30616330383630353137663300000501000000003801003353716c436c722066756e6374696f6e616c697479207573656420627920746865206461746120616363657373206c617965722e0000370100324d6963726f736f66742e456e74657270726973654d616e6167656d656e742e53716c2e446174614163636573734c6179657200004001003b436f707972696768742032303035204d6963726f736f667420436f72706f726174696f6e2e2020416c6c207269676874732072657365727665642e00002401001f4d6963726f736f6674204f7065726174696f6e73204d616e6167657220763300001a0100154d6963726f736f667420436f72706f726174696f6e00000f01000a362e302e343038352e3000000801000701000000000801000800000000001e01000100540216577261704e6f6e457863657074696f6e5468726f777301000000000000cdef7c44000000000200000059000000a82a0000a80c000052534453165649e3ed4a514990cc3fb2ca36648a01000000643a5c6d6f6d76332e6d61696e5c7461726765745c64656275675c693338365c4d6963726f736f66742e4d6f6d2e446174614163636573732e53716c2e706462000000002c2b000000000000000000004e2b0000002000000000000000000000000000000000000000000000402b00000000000000000000000000000000000000005f436f72446c6c4d61696e006d73636f7265652e646c6c0000000000ff250020ec5600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000100100000001800008000000000000000000000000000000100010000003000008000000000000000000000000000000100000000004800000058400000b80400000000000000000000b80434000000560053005f00560045005200530049004f004e005f0049004e0046004f0000000000bd04effe00000100000006000000f50f000006000000f50f3f000000000000000400000002000000000000000000000000000000440000000100560061007200460069006c00650049006e0066006f00000000002400040000005400720061006e0073006c006100740069006f006e00000000000000b00418040000010053007400720069006e006700460069006c00650049006e0066006f000000f4030000010030003000300030003000340062003000000080003400010043006f006d006d0065006e00740073000000530071006c0043006c0072002000660075006e006300740069006f006e0061006c0069007400790020007500730065006400200062007900200074006800650020006400610074006100200061006300630065007300730020006c0061007900650072002e0000004c001600010043006f006d00700061006e0079004e0061006d006500000000004d006900630072006f0073006f0066007400200043006f00720070006f0072006100740069006f006e000000900033000100460069006c0065004400650073006300720069007000740069006f006e00000000004d006900630072006f0073006f00660074002e0045006e00740065007200700072006900730065004d0061006e006100670065006d0065006e0074002e00530071006c002e0044006100740061004100630063006500730073004c0061007900650072000000000038000b000100460069006c006500560065007200730069006f006e000000000036002e0030002e0034003000380035002e0030000000000064002100010049006e007400650072006e0061006c004e0061006d00650000004d006900630072006f0073006f00660074002e004d006f006d002e0044006100740061004100630063006500730073002e00530071006c002e0064006c006c00000000009c003c0001004c006500670061006c0043006f007000790072006900670068007400000043006f0070007900720069006700680074002000320030003000350020004d006900630072006f0073006f0066007400200043006f00720070006f0072006100740069006f006e002e002000200041006c006c0020007200690067006800740073002000720065007300650072007600650064002e0000006c00210001004f0072006900670069006e0061006c00460069006c0065006e0061006d00650000004d006900630072006f0073006f00660074002e004d006f006d002e0044006100740061004100630063006500730073002e00530071006c002e0064006c006c0000000000600020000100500072006f0064007500630074004e0061006d006500000000004d006900630072006f0073006f006600740020004f007000650072006100740069006f006e00730020004d0061006e00610067006500720020007600330000003c000b000100500072006f006400750063007400560065007200730069006f006e00000036002e0030002e0034003000380035002e0030000000000040000b00010041007300730065006d0062006c0079002000560065007200730069006f006e00000036002e0030002e0034003000380035002e00300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000c000000603b00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000);
   set        @ClrName1 = CONVERT(NVARCHAR(4000), 'Microsoft.EnterpriseManagement.Sql.DataAccessLayer');        

   -- Drop trusted assembly if exists
   IF EXISTS (select * from sys.trusted_assemblies where description = @ClrName1)
   BEGIN
   EXEC SYS.sp_drop_trusted_assembly @Hash1
   END        

   --Add to trusted assembly
   EXEC SYS.SP_ADD_TRUSTED_ASSEMBLY @Hash1, @ClrName1        
   END
   GO
   ```

## Server operating system

The following versions of Windows Server operating system are supported.

|System Center  component|Windows Server 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server 2016|Windows Server 2016 (Server with Desktop Experience)|Windows Server 2016 Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|
|**Service Manager** Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Data Warehouse Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Database or Data Warehouse Database||&#8226;|&#8226;|&#8226;||
|**Service Manager** Self-Service Portal (HTML 5)||&#8226;|&#8226;|&#8226;|&nbsp;|

## Client operating system

The following versions of Windows client operating system are supported for the Service Manager console.

|System Center client-side components|Windows&reg; 7|Windows&reg; 8|Windows&reg; 8.1|Windows Server&reg; 2008 R2 SP1|Windows Server&reg; 2012|Windows Server&reg; 2012 R2 Standard, Datacenter|Windows 10 Enterprise|Windows Server&reg; 2016 Standard, Datacenter|
|-----------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
|**Service Manager** Console|&#8226;|&#8226;|&#8226;|||&#8226;|&#8226;|&#8226;|


## .NET Versions supported

The following versions of .NET are supported for Service Manager.

|System Center 1807 component|.NET 3.5 SP1|.NET 4|.NET 4.5|.NET 4.5.1|.NET 4.5.2|.NET 4.6|
|-----------------------------------|----------------|----------|------------|--------------|--------------|------------|
|**Service Manager** Management Server|&#8226;| | |&#8226;| | |
|**Service Manager** Data Warehouse Management Server|&#8226;| | |&#8226;| | |
|**Service Manager** console|&#8226;| | |&#8226;| | |
|**Service Manager** Self\-Service Portal|&#8226;| | |&#8226;| | &nbsp; |

## PowerShell Versions supported

The following versions of PowerShell are supported for Service Manager.

|System Center Component|Windows PowerShell 2.0|Windows PowerShell 3.0|Windows PowerShell 4.0|Windows PowerShell 5.0|
|---------------------------|--------------------------|--------------------------|-----------------------------------------------|-----------------------------------------------|
|**Service Manager** Console|||&#8226;|&#8226;|
|**Service Manager** Management Server|||&#8226;|&#8226;|
|**Service Manager** Data Warehouse Management Server|||&#8226;|&#8226;|
