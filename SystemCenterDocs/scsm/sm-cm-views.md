---
title:  Mapping Service Manager properties to Configuration Manager database views
description: Learn about the relationships between Service Manager properties and Configuration Manager database views.
manager:  carmonm
ms.topic: reference
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  b1af3b48-696b-4db8-94e6-9da28c2ef125
---

# Mapping System Center 2016 - Service Manager properties to Configuration Manager database views

>Applies To: System Center 2016 - Service Manager

The hardware inventory feature in Configuration Manager gathers information about computers in the organization. In Service Manager, by using a Configuration Manager Connector, you can import that hardware inventory data from Configuration Manager. The tables in this appendix describe the mapping between Service Manager properties and column names of Configuration Manager database views.

## Microsoft.SystemCenter.ConfigurationManager.DeployedComputer
The following table describes the mapping for the **Microsoft.SystemCenter.ConfigurationManager.DeployedComputer** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Name0|
|Microsoft.SystemCenter.ConfigurationManager.DeployedComputer|HardwareID [Key]|SCCM.Ext.vex_R_System.Hardware_ID0|
||SMBIOS_UUID|SCCM.Ext.vex_R_System.SMBIOS_GUID0|
||SMBIOSAssetTag|SCCM.Ext.vex_GS_SYSTEM_ENCLOSURE.SMBIOSAssetTag0|
||Manufacturer|SCCM.Ext.vex_GS_SYSTEM_ENCLOSURE.Manufacturer0|
||Model|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Model0|
||NumberOfProcessors|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.NumberOfProcessors0|
||SystemType|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.SystemType0|
||ChassisType|SCCM.Ext.vex_GS_SYSTEM_ENCLOSURE.ChassisTypes0|
||SerialNumber|If SCCM.Ext.vex_GS_SYSTEM_ENCLOSURE.SerialNumber0 is NULL, '00000000' or 'Not Available', then SCCM.Ext.vex_GS_PC_BIOS.SerialNumber0, else SCCM.Ext.vex_GS_SYSTEM_ENCLOSURE.SerialNumber0|

## Microsoft.Windows.Computer
The following table describes the mappings for the **Microsoft.Windows.Computer** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Name0|
|Microsoft.Windows.Computer|PrincipalName (FQDN) [Key]|Constructed using SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Name0 or SCCM.Ext.vex_R_System.Netbios_Name0 and SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Domain0 or SCCM.Ext.vex_R_System.Resource_Domain_OR_Workgr0. If SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Name0 is null, SCCM.Ext.vex_R_System.Netbios_Name0 is used as name. If SCCM.Ext.vex_GS_COMPUTER_SYSTEM.Domain0 is null, SCCM.Ext.vex_R_System.Resource_Domain_OR_Workgr0 is used as domain.|
||NetbiosComputerName|SCCM.Ext.vex_R_System.Netbios_Name0|
||NetbiosDomainName|SCCM.Ext.vex_R_System.Resource_Domain_OR_Workgr0|
||OffsetInMinuteFromGreenwichTime|SCCM.Ext.vex_GS_Computer_System.CurrentTimeZone0|
||IsVirtualMachine|SCCM.Ext.vex_GS_Computer_System.Model0, vex_GS_Manufacturer, that is, Model0 = "Virtual Machine" or "VMware Virtual Platform" OR Manufacturer="Microsoft Corporation" or "VMware, Inc"|
||ActiveDirectorySite|SCCM.Ext.vex_R_System.AD_Site_Name0|
||LastInventoryDate|SCCM.Ext.Vex_GS_Workstation_Status.LastHWScan|

## Microsoft.Windows.OperatingSystem
The following table describes the mappings for the **Microsoft.Windows.OperatingSystem** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Caption0|
|Microsoft.Windows.OperatingSystem|OSVersion|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Version0|
||BuildNumber|SCCM.Ext.vex_GS_OPERATING_SYSTEM.BuildNumber0|
||CSDVersion|SCCM.Ext.vex_GS_OPERATING_SYSTEM.CSDVersion0|
||InstallDate|SCCM.Ext.vex_GS_OPERATING_SYSTEM.InstallDate0|
||SystemDrive|SCCM.Ext.vex_GS_OPERATING_SYSTEM.SystemDirectory0|
||WindowsDirectory|SCCM.Ext.vex_GS_OPERATING_SYSTEM.WindowsDirectory0|
||PhysicalMemory|SCCM.Ext.vex_GS_OPERATING_SYSTEM.TotalVisibleMemorySize0|
||LogicalProcessors|SCCM.Ext.vex_GS_COMPUTER_SYSTEM.NmberOfProcessors0|
||CountryCode|SCCM.Ext.vex_GS_OPERATING_SYSTEM.CountryCode0|
||Locale|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Locale0|
||Manufacturer|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Manufacturer0|
||OSLanguage|SCCM.Ext.vex_GS_OPERATING_SYSTEM.OSLanguage0|
||MinorVersion|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Version0|
||MajorVersion|SCCM.Ext.vex_GS_OPERATING_SYSTEM.Version0|

## Microsoft.Windows.Peripherals.LogicalDisk
The following table describes the mappings for the **Microsoft.Windows.Peripherals.LogicalDisk** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_LOGICAL_DISK.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID [Key]|SCCM.Ext.vex_GS_LOGICAL_DISK.DeviceID0|
||Name|SCCM.Ext.vex_GS_LOGICAL_DISK.Name0|
||Description|SCCM.Ext.vex.GS_LOGICAL_DISK.Description0|
|Microsoft.Windows.LogicalDisk|VolumeName|SCCM.Ext.vex_GS_LOGICAL_DISK.VolumeName0|
|Microsoft.Windows.Peripherals.LogicalDisk|FileSystem|SCCM.Ext.vex_GS_LOGICAL_DISK.FileSystem0|
||Compressed|SCCM.Ext.vex_GS_LOGICAL_DISK.Compressed0|
||Size|SCCM.Ext.vex_GS_LOGICAL_DISK.Size0|
||DriveType|SCCM.Ext.vex_GS_LOGICAL_DISK.DriveType0|
||FreeSpace|SCCM.Ext.vex_GS_LOGICAL_DISK.FreeSpace0|

## Microsoft.Windows.Peripherals.PhysicalDisk
The following table describes the mappings for the **Microsoft.Windows.Peripherals.PhysicalDisk** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_DISK.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID [Key]|SCCM.Ext.vex_GS_DISK.DeviceID0|
||Name|SCCM.Ext.vex_GS_DISK.Name0|
||Description|SCCM.Ext.vex.GS_DISK.Description0|
|Microsoft.Windows.PhysicalDisk|MediaType|SCCM.Ext.vex.GS_DISK.MediaType0|
||PNPDeviceID|SCCM.Ext.vex.GS_DISK.PNPDeviceID0|
|Microsoft.Windows.Peripherals.PhysicalDisk|Caption|SCCM.Ext.vex.GS_DISK.Description0|
||Index|SCCM.Ext.vex.GS_DISK.Index0|
||InterfaceType|SCCM.Ext.vex.GS_DISK.InterfaceType0|
||Manufacturer|SCCM.Ext.vex.GS_DISK.Manufacturer0|
||Model|SCCM.Ext.vex.GS_DISK.Model0|
||SCSIBus|SCCM.Ext.vex.GS_DISK.SCSIBus0|
||SCSILogicalUnit|SCCM.Ext.vex.GS_DISK.SCSILogicalUnit0|
||SCSIPort|SCCM.Ext.vex.GS_DISK.SCSIPort0|
||SCSITargetID|SCCM.Ext.vex.GS_DISK.TargetId0|
||Size|SCCM.Ext.vex.GS_DISK.Size0|
||TotalCylinders|SCCM.Ext.vex.GS_DISK.TotalCylinders0|
||TotalHeads|SCCM.Ext.Vex.GS_DISK.TotalHeads0|
||TotalSectors|SCCM.Ext.vex.GS_DISK.TotalSectors0|
||TotalTracks|SCCM.Ext.vex.GS_DISK.TotalTracks0|
||TracksPerCylinder|SCCM.Ext.vex.GS_DISK.TracksPerCylinder0|

## Microsoft.Windows.Peripherals.Processor
The following table describes the mappings for the **Microsoft.Windows.Peripherals.Processor** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_PROCESSOR.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID [Key]|SCCM.Ext.vex_GS_PROCESSOR.DeviceID0|
||Name|SCCM.Ext.vex_GS_PROCESSOR.Name0|
||Description|SCCM.Ext.vex.GS_PROCESSOR.Name0|
|Microsoft.Windows.Processor|Family|SCCM.Ext.vex.GS_PROCESSOR.Family0|
||MaxClockSpeed|SCCM.Ext.vex.GS_PROCESSOR.MaxClockSpeed0|
||Type|SCCM.Ext.vex.GS_PROCESSOR.ProcessorType0|
||BrandID|SCCM.Ext.vex.GS_PROCESSOR.BrandID0|
||PCache|SCCM.Ext.vex.GS_PROCESSOR.PCache0|
||CPUKey|SCCM.Ext.vex.GS_PROCESSOR.CPUKey0|
||IsMobile (bool)|SCCM.Ext.vex.GS_PROCESSOR.IsMobile0|
||IsMultiCore (bool)|SCCM.Ext.vex.GS_PROCESSOR.IsMulticore0|
|Microsoft.Windows.Peripherals.Processor|Manufacturer|SCCM.Ext.vex.GS_PROCESSOR.Manufacturer0|
||Speed|SCCM.Ext.vex.GS_PROCESSOR.NormSpeed0|
||DataWidth|SCCM.Ext.vex.GS_PROCESSOR.DataWidth0|
||Revision|SCCM.Ext.vex.GS_PROCESSOR.Revision0|
||Version|SCCM.Ext.vex.GS_PROCESSOR.Version0|

## Microsoft.Windows.Peripherals.NetworkAdapter
The following table describes the mappings for the **Microsoft.Windows.Peripherals.NetworkAdapter** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager Database Views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_NETWORK_ADAPTER.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID [Key]|SCCM.Ext.vex_GS_NETWORK_ADAPTER.DeviceID0|
||Name|SCCM.Ext.vex_GS_NETWORK_ADAPTER.Name0|
||Description|SCCM.Ext.vex.GS_NETWORK_ADAPTER.Description0|
|Microsoft.Windows.NetworkAdapter|Bandwidth|SCCM.Ext.vex.GS_NETWORK_ADAPTER.Speed0|
||MaxSpeed (int)|SCCM.Ext.vex.GS_NETWORK_ADAPTER.MaxSpeed0|
||ProductName|SCCM.Ext.vex.GS_NETWORK_ADAPTER.ProductName0|
||DefaultIPGateway|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.DefaultIPGateway0|
||DHCPHostName|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.DHCPServer|
||IPEnabled|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.IPEnabled0|
|Microsoft.Windows.Peripherals.NetworkAdapter|AdapterType|SCCM.Ext.vex.GS_NETWORK_ADAPTER.AdapterType0|
||Index|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.Index0|
||Manufacturer|SCCM.Ext.vex.GS_NETWORK_ADAPTER.Manufacturer0|
||MACAddress|SCCM.Ext.vex.GS_NETWORK_ADAPTER.MACAddress0|
||ServiceName|SCCM.Ext.vex.GS_NETWORK_ADAPTER.ServiceName0|
||DHCPEnabled|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.DHCPEnabled0|
||DHCPServer|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.DHCPServer0|
||DNSDomain|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.DNSDomain0|
||IPAddress|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.IPAddress0|
||IPSubnet|SCCM.Ext.vex.GS_NETWORK_ADAPTER_CONFIGUR.IPSubnet0|

## System.DeviceHasSoftwareItemInstalled
The following table describes the mappings for the **System.DeviceHasSoftwareItemInstalled** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.ProductName0|
|System.SoftwareItem|ProductName [Key]|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.ProductName0|
||Publisher [Key]|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.Publisher0|
||VersionString [Key]|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.ProductVersion0|
||MajorVersion|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.VersionMajor0|
||MinorVersion|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.VersionMinor0|
||LocaleID|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.Language0|
|System.DeviceHasSoftwareItemInstalled|InstalledDate|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.InstalledDate0|
||InstalledPath|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.InstalledLocation0|
||SerialNumber|SCCM.Ext.vex_GS_INSTALLED_SOFTWARE.ProductID0|
||IsVirtualApplication|SCCM.Ext.Vex_GS_INSTALLED_SOFTWARE.InstallType|

## System.DeviceHasSoftwareUpdateInstalled
The following table describes the mappings for the **System.DeviceHasSoftwareUpdateInstalled** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.SoftwareUpdate|Vendor [Key]|SCCM.Ext.vex_LocalizedCategoryInstances.CategoryInstanceName|
||Title [Key]|SCCM.Ext.vex_LocalizedCIProperties.DisplayName|
|Microsoft.Windows.SoftwareUpdate|ArticleID|SCCM.Ext.vex_UpdateCIs.ArticleID|
||BulletinID|SCCM.Ext.vex_UpdateCIs.BulletinID|
||SupportString|SCCM.Ext.vex_LocalizedCIProperties.CIInformativeURL|
||Classification|SCCM.Ext.vex_LocalizedCategoryInstances.CategoryInstanceName|
|System.DeviceHasSoftwareUpdateInstalled|InstallStatus|SCCM.Ext.vex_UpdateComplianceStatus.Status|

## Microsoft.SystemCenter.ConfigurationManager.DCM_CI
The following table describes the mappings for the **Microsoft.SystemCenter.ConfigurationManager.DCM_CI** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|Microsoft.SystemCenter.ConfigurationManager.DCM_CI|DisplayName|SCCM.Ext.vex_LocalizedCIProperties.DisplayName|
||UniqueID [Key]|SCCM.Ext.vex_ConfigurationItems.CI_UniqueID|
||Description|SCCM.Ext.vex_LocalizedCIProperties.Description|
||IsBaseline|SCCM.Ext.vex_ConfigurationItems.CIType_ID|

## Microsoft.SystemCenter.ConfigurationManager.DCM_NoncompliantCI
The following table describes the mappings for the **Microsoft.SystemCenter.ConfigurationManager.DCM_NoncompliantCI** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|Microsoft.SystemCenter.ConfigurationManager.DCM_NoncompliantCI|UniqueID [Key]|SCCM.Ext.vex_ConfigurationItems.CI_UniqueID|
||Baseline_UniqueID [Key]|SCCM.Ext.vex_ConfigurationItems.CI_UniqueID|
||MaxNonComplianceCriticality [Key]|SCCM.Ext.vex_CICurrentComplianceStatus.MaxNoncomplianceCriticality|

## System.Domain.User
The following table describes the mappings for the **System.Domain.User** type.

|Configuration Manager class|Configuration Manager database value|Service Manager property|
|-------------------------------|----------------------------------------|----------------------------|
|System.Domain.User|Domain [Key]|Parse SCCM_Ext.vex_GS_SYSTEM_CONSOLE_USER|
||UserName [Key]|Parse SCCM_Ext.vex_GS_SYSTEM_CONSOLE_USER|

## Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf
The following table describes the mapping for the **Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.ConfigItem|DisplayName|SCCM_Ext.vex_Collection.CollectionName|
|Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf|Count|Count of computers in collection|
||CollID [Key]|SCCM_Ext.vex_Collection.CollID|
||CollectionName|SCCM_Ext.vex_Collection.CollectionName|
||CollectionID|SCCM_Ext.vex_Collection.CollectionID|

## Microsoft.ConfigMgr.SoftwarePackage
The following table describes the mapping for the **Microsoft.ConfigMgr.SoftwarePackage** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.ConfigItem|DisplayName|SCCM_Ext.vex_Package.Name|
|Microsoft.ConfigMgr.SoftwarePackage|ID [Key]|SCCM_Ext.vex_Package.PackageID|
||Version|SCCM_Ext.vex_Package.Version|
||Language|SCCM_Ext.vex_Package.Language|
||Manufacturer|SCCM_Ext.vex_Package.Manufacturer|
||Description|SCCM_Ext.vex_Package.Description|
