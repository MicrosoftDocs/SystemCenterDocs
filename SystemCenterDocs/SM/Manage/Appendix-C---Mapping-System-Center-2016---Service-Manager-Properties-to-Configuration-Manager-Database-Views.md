---
title: Appendix C - Mapping System Center 2016 - Service Manager Properties to Configuration Manager Database Views
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1af3b48-696b-4db8-94e6-9da28c2ef125
---
# Appendix C - Mapping System Center 2016 - Service Manager Properties to Configuration Manager Database Views
The hardware inventory feature in Configuration Manager gathers information about computers in the organization. In [!INCLUDE[smshort](../../includes/smshort_md.md)], by using a Configuration Manager Connector, you can import that hardware inventory data from Configuration Manager. The tables in this appendix describe the mapping between [!INCLUDE[smshort](../../includes/smshort_md.md)] properties and column names of Configuration Manager database views.

## Microsoft.SystemCenter.ConfigurationManager.DeployedComputer
The following table describes the mapping for the **Microsoft.SystemCenter.ConfigurationManager.DeployedComputer** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Name0|
|Microsoft.SystemCenter.ConfigurationManager.DeployedComputer|HardwareID \[Key\]|SCCM.Ext.vex\_R\_System.Hardware\_ID0|
||SMBIOS\_UUID|SCCM.Ext.vex\_R\_System.SMBIOS\_GUID0|
||SMBIOSAssetTag|SCCM.Ext.vex\_GS\_SYSTEM\_ENCLOSURE.SMBIOSAssetTag0|
||Manufacturer|SCCM.Ext.vex\_GS\_SYSTEM\_ENCLOSURE.Manufacturer0|
||Model|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Model0|
||NumberOfProcessors|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.NumberOfProcessors0|
||SystemType|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.SystemType0|
||ChassisType|SCCM.Ext.vex\_GS\_SYSTEM\_ENCLOSURE.ChassisTypes0|
||SerialNumber|If SCCM.Ext.vex\_GS\_SYSTEM\_ENCLOSURE.SerialNumber0 is NULL, '00000000' or 'Not Available', then SCCM.Ext.vex\_GS\_PC\_BIOS.SerialNumber0, else SCCM.Ext.vex\_GS\_SYSTEM\_ENCLOSURE.SerialNumber0|

## Microsoft.Windows.Computer
The following table describes the mappings for the **Microsoft.Windows.Computer** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Name0|
|Microsoft.Windows.Computer|PrincipalName \(FQDN\) \[Key\]|Constructed using SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Name0 or SCCM.Ext.vex\_R\_System.Netbios\_Name0 and SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Domain0 or SCCM.Ext.vex\_R\_System.Resource\_Domain\_OR\_Workgr0. If SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Name0 is null, SCCM.Ext.vex\_R\_System.Netbios\_Name0 is used as name. If SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.Domain0 is null, SCCM.Ext.vex\_R\_System.Resource\_Domain\_OR\_Workgr0 is used as domain.|
||NetbiosComputerName|SCCM.Ext.vex\_R\_System.Netbios\_Name0|
||NetbiosDomainName|SCCM.Ext.vex\_R\_System.Resource\_Domain\_OR\_Workgr0|
||OffsetInMinuteFromGreenwichTime|SCCM.Ext.vex\_GS\_Computer\_System.CurrentTimeZone0|
||IsVirtualMachine|SCCM.Ext.vex\_GS\_Computer\_System.Model0, vex\_GS\_Manufacturer, that is, Model0 \= "Virtual Machine" or "VMware Virtual Platform" OR Manufacturer\="Microsoft Corporation" or "VMware, Inc"|
||ActiveDirectorySite|SCCM.Ext.vex\_R\_System.AD\_Site\_Name0|
||LastInventoryDate|SCCM.Ext.Vex\_GS\_Workstation\_Status.LastHWScan|

## Microsoft.Windows.OperatingSystem
The following table describes the mappings for the **Microsoft.Windows.OperatingSystem** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Caption0|
|Microsoft.Windows.OperatingSystem|OSVersion|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Version0|
||BuildNumber|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.BuildNumber0|
||CSDVersion|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.CSDVersion0|
||InstallDate|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.InstallDate0|
||SystemDrive|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.SystemDirectory0|
||WindowsDirectory|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.WindowsDirectory0|
||PhysicalMemory|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.TotalVisibleMemorySize0|
||LogicalProcessors|SCCM.Ext.vex\_GS\_COMPUTER\_SYSTEM.NmberOfProcessors0|
||CountryCode|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.CountryCode0|
||Locale|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Locale0|
||Manufacturer|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Manufacturer0|
||OSLanguage|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.OSLanguage0|
||MinorVersion|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Version0|
||MajorVersion|SCCM.Ext.vex\_GS\_OPERATING\_SYSTEM.Version0|

## Microsoft.Windows.Peripherals.LogicalDisk
The following table describes the mappings for the **Microsoft.Windows.Peripherals.LogicalDisk** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID \[Key\]|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.DeviceID0|
||Name|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.Name0|
||Description|SCCM.Ext.vex.GS\_LOGICAL\_DISK.Description0|
|Microsoft.Windows.LogicalDisk|VolumeName|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.VolumeName0|
|Microsoft.Windows.Peripherals.LogicalDisk|FileSystem|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.FileSystem0|
||Compressed|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.Compressed0|
||Size|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.Size0|
||DriveType|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.DriveType0|
||FreeSpace|SCCM.Ext.vex\_GS\_LOGICAL\_DISK.FreeSpace0|

## Microsoft.Windows.Peripherals.PhysicalDisk
The following table describes the mappings for the **Microsoft.Windows.Peripherals.PhysicalDisk** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_DISK.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID \[Key\]|SCCM.Ext.vex\_GS\_DISK.DeviceID0|
||Name|SCCM.Ext.vex\_GS\_DISK.Name0|
||Description|SCCM.Ext.vex.GS\_DISK.Description0|
|Microsoft.Windows.PhysicalDisk|MediaType|SCCM.Ext.vex.GS\_DISK.MediaType0|
||PNPDeviceID|SCCM.Ext.vex.GS\_DISK.PNPDeviceID0|
|Microsoft.Windows.Peripherals.PhysicalDisk|Caption|SCCM.Ext.vex.GS\_DISK.Description0|
||Index|SCCM.Ext.vex.GS\_DISK.Index0|
||InterfaceType|SCCM.Ext.vex.GS\_DISK.InterfaceType0|
||Manufacturer|SCCM.Ext.vex.GS\_DISK.Manufacturer0|
||Model|SCCM.Ext.vex.GS\_DISK.Model0|
||SCSIBus|SCCM.Ext.vex.GS\_DISK.SCSIBus0|
||SCSILogicalUnit|SCCM.Ext.vex.GS\_DISK.SCSILogicalUnit0|
||SCSIPort|SCCM.Ext.vex.GS\_DISK.SCSIPort0|
||SCSITargetID|SCCM.Ext.vex.GS\_DISK.TargetId0|
||Size|SCCM.Ext.vex.GS\_DISK.Size0|
||TotalCylinders|SCCM.Ext.vex.GS\_DISK.TotalCylinders0|
||TotalHeads|SCCM.Ext.Vex.GS\_DISK.TotalHeads0|
||TotalSectors|SCCM.Ext.vex.GS\_DISK.TotalSectors0|
||TotalTracks|SCCM.Ext.vex.GS\_DISK.TotalTracks0|
||TracksPerCylinder|SCCM.Ext.vex.GS\_DISK.TracksPerCylinder0|

## Microsoft.Windows.Peripherals.Processor
The following table describes the mappings for the **Microsoft.Windows.Peripherals.Processor** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_PROCESSOR.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID \[Key\]|SCCM.Ext.vex\_GS\_PROCESSOR.DeviceID0|
||Name|SCCM.Ext.vex\_GS\_PROCESSOR.Name0|
||Description|SCCM.Ext.vex.GS\_PROCESSOR.Name0|
|Microsoft.Windows.Processor|Family|SCCM.Ext.vex.GS\_PROCESSOR.Family0|
||MaxClockSpeed|SCCM.Ext.vex.GS\_PROCESSOR.MaxClockSpeed0|
||Type|SCCM.Ext.vex.GS\_PROCESSOR.ProcessorType0|
||BrandID|SCCM.Ext.vex.GS\_PROCESSOR.BrandID0|
||PCache|SCCM.Ext.vex.GS\_PROCESSOR.PCache0|
||CPUKey|SCCM.Ext.vex.GS\_PROCESSOR.CPUKey0|
||IsMobile \(bool\)|SCCM.Ext.vex.GS\_PROCESSOR.IsMobile0|
||IsMultiCore \(bool\)|SCCM.Ext.vex.GS\_PROCESSOR.IsMulticore0|
|Microsoft.Windows.Peripherals.Processor|Manufacturer|SCCM.Ext.vex.GS\_PROCESSOR.Manufacturer0|
||Speed|SCCM.Ext.vex.GS\_PROCESSOR.NormSpeed0|
||DataWidth|SCCM.Ext.vex.GS\_PROCESSOR.DataWidth0|
||Revision|SCCM.Ext.vex.GS\_PROCESSOR.Revision0|
||Version|SCCM.Ext.vex.GS\_PROCESSOR.Version0|

## Microsoft.Windows.Peripherals.NetworkAdapter
The following table describes the mappings for the **Microsoft.Windows.Peripherals.NetworkAdapter** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager Database Views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_NETWORK\_ADAPTER.Name0|
|Microsoft.Windows.LogicalDevice|DeviceID \[Key\]|SCCM.Ext.vex\_GS\_NETWORK\_ADAPTER.DeviceID0|
||Name|SCCM.Ext.vex\_GS\_NETWORK\_ADAPTER.Name0|
||Description|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.Description0|
|Microsoft.Windows.NetworkAdapter|Bandwidth|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.Speed0|
||MaxSpeed \(int\)|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.MaxSpeed0|
||ProductName|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.ProductName0|
||DefaultIPGateway|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.DefaultIPGateway0|
||DHCPHostName|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.DHCPServer|
||IPEnabled|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.IPEnabled0|
|Microsoft.Windows.Peripherals.NetworkAdapter|AdapterType|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.AdapterType0|
||Index|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.Index0|
||Manufacturer|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.Manufacturer0|
||MACAddress|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.MACAddress0|
||ServiceName|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER.ServiceName0|
||DHCPEnabled|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.DHCPEnabled0|
||DHCPServer|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.DHCPServer0|
||DNSDomain|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.DNSDomain0|
||IPAddress|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.IPAddress0|
||IPSubnet|SCCM.Ext.vex.GS\_NETWORK\_ADAPTER\_CONFIGUR.IPSubnet0|

## System.DeviceHasSoftwareItemInstalled
The following table describes the mappings for the **System.DeviceHasSoftwareItemInstalled** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.Entity|DisplayName|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.ProductName0|
|System.SoftwareItem|ProductName \[Key\]|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.ProductName0|
||Publisher \[Key\]|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.Publisher0|
||VersionString \[Key\]|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.ProductVersion0|
||MajorVersion|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.VersionMajor0|
||MinorVersion|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.VersionMinor0|
||LocaleID|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.Language0|
|System.DeviceHasSoftwareItemInstalled|InstalledDate|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.InstalledDate0|
||InstalledPath|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.InstalledLocation0|
||SerialNumber|SCCM.Ext.vex\_GS\_INSTALLED\_SOFTWARE.ProductID0|
||IsVirtualApplication|SCCM.Ext.Vex\_GS\_INSTALLED\_SOFTWARE.InstallType|

## System.DeviceHasSoftwareUpdateInstalled
The following table describes the mappings for the **System.DeviceHasSoftwareUpdateInstalled** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.SoftwareUpdate|Vendor \[Key\]|SCCM.Ext.vex\_LocalizedCategoryInstances.CategoryInstanceName|
||Title \[Key\]|SCCM.Ext.vex\_LocalizedCIProperties.DisplayName|
|Microsoft.Windows.SoftwareUpdate|ArticleID|SCCM.Ext.vex\_UpdateCIs.ArticleID|
||BulletinID|SCCM.Ext.vex\_UpdateCIs.BulletinID|
||SupportString|SCCM.Ext.vex\_LocalizedCIProperties.CIInformativeURL|
||Classification|SCCM.Ext.vex\_LocalizedCategoryInstances.CategoryInstanceName|
|System.DeviceHasSoftwareUpdateInstalled|InstallStatus|SCCM.Ext.vex\_UpdateComplianceStatus.Status|

## Microsoft.SystemCenter.ConfigurationManager.DCM\_CI
The following table describes the mappings for the **Microsoft.SystemCenter.ConfigurationManager.DCM\_CI** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|Microsoft.SystemCenter.ConfigurationManager.DCM\_CI|DisplayName|SCCM.Ext.vex\_LocalizedCIProperties.DisplayName|
||UniqueID \[Key\]|SCCM.Ext.vex\_ConfigurationItems.CI\_UniqueID|
||Description|SCCM.Ext.vex\_LocalizedCIProperties.Description|
||IsBaseline|SCCM.Ext.vex\_ConfigurationItems.CIType\_ID|

## Microsoft.SystemCenter.ConfigurationManager.DCM\_NoncompliantCI
The following table describes the mappings for the **Microsoft.SystemCenter.ConfigurationManager.DCM\_NoncompliantCI** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|Microsoft.SystemCenter.ConfigurationManager.DCM\_NoncompliantCI|UniqueID \[Key\]|SCCM.Ext.vex\_ConfigurationItems.CI\_UniqueID|
||Baseline\_UniqueID \[Key\]|SCCM.Ext.vex\_ConfigurationItems.CI\_UniqueID|
||MaxNonComplianceCriticality \[Key\]|SCCM.Ext.vex\_CICurrentComplianceStatus.MaxNoncomplianceCriticality|

## System.Domain.User
The following table describes the mappings for the **System.Domain.User** type.

|Configuration Manager class|Configuration Manager database value|Service Manager property|
|-------------------------------|----------------------------------------|----------------------------|
|System.Domain.User|Domain \[Key\]|Parse SCCM\_Ext.vex\_GS\_SYSTEM\_CONSOLE\_USER|
||UserName \[Key\]|Parse SCCM\_Ext.vex\_GS\_SYSTEM\_CONSOLE\_USER|

## Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf
The following table describes the mapping for the **Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.ConfigItem|DisplayName|SCCM\_Ext.vex\_Collection.CollectionName|
|Microsoft.SystemCenter.ConfigurationManagergr.CollectionInf|Count|Count of computers in collection|
||CollID \[Key\]|SCCM\_Ext.vex\_Collection.CollID|
||CollectionName|SCCM\_Ext.vex\_Collection.CollectionName|
||CollectionID|SCCM\_Ext.vex\_Collection.CollectionID|

## Microsoft.ConfigMgr.SoftwarePackage
The following table describes the mapping for the **Microsoft.ConfigMgr.SoftwarePackage** type.

|Service Manager type|Service Manager property|Column name of Configuration Manager database views|
|------------------------|----------------------------|-------------------------------------------------------|
|System.ConfigItem|DisplayName|SCCM\_Ext.vex\_Package.Name|
|Microsoft.ConfigMgr.SoftwarePackage|ID \[Key\]|SCCM\_Ext.vex\_Package.PackageID|
||Version|SCCM\_Ext.vex\_Package.Version|
||Language|SCCM\_Ext.vex\_Package.Language|
||Manufacturer|SCCM\_Ext.vex\_Package.Manufacturer|
||Description|SCCM\_Ext.vex\_Package.Description|


