---
title: Changes made to AD DS for end-user recovery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0a2b505-95b0-4094-a34e-2450743c1b6e
---
# Changes made to AD DS for end-user recovery
When you enable end\-user recovery [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] performs a number of actions in AD DS:

-   Extends the schema

-   Creates a container \(MS\-ShareMapConfiguration\)

-   Grants the [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] server permissions to change the contents of the container

-   Adds mappings between source shares and shares on the replicas

If DPM administrators are also schema and domain administrators in AD DS, end\-user recovery can be enabled in a couple of clicks. For DPM administrators who aren’t schema and domain administrators, the DPMADSchemaExtension tool runs to configure AD DS.

This topic describes the classes and attributes that are added when end\-user recovery is enabled by either an AD DS schema and domain administrator, or when the DPMADSchemaExtension tool runs.

[Classes Added by DPM](#BKMK_Class) describes the classes that are added to Active Directory when you enable end\-user recovery on [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)].

[Attributes Added by DPM](#BKMK_Att) describes the attributes that are added to Active Directory when you enable end\-user recovery on [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)].

## <a name="BKMK_Class"></a>Classes added by DPM
[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] adds one class, **ms\-SrvShareMapping**, to the Active Directory directory service when you enable end\-user recovery. This class contains the mapping from the protected computer \(and share\) to the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server \(and share\).

> [!CAUTION]
> It is recommended that you do not modify this class.

The following table provides a detailed description of the **ms\-SrvShareMapping** class:

|Attribute|Value|
|-------------|---------|
|objectClass|Top|
|objectClass|classSchema|
|instanceType|4|
|possSuperiors|Container|
|possSuperiors|organizationalUnit|
|subClassOf|Top|
|governsID|1.2.840.113556.1.6.33.1.22|
|mustContain|ms\-backupSrvShare|
|mustContain|ms\-productionSrvShare|
|rDNAttID|Cn|
|showInAdvancedViewOnly|TRUE|
|adminDisplayName|ms\-SrvShareMapping|
|lDAPDisplayName|ms\-SrvShareMapping|
|adminDescription|Maps servers with shared resources.|
|objectClassCategory|1|

## <a name="BKMK_Att"></a>Attributes added by DPM
[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] adds two attributes to Active Directory when you enable end\-user recovery. The following table lists the added attributes:

|Attribute|Description|
|-------------|---------------|
|ms\-BackupSrv\-Share Attribute|Provides the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] share name and [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] computer name in a string.|
|ms\-ProductionSrv\-Share Attribute|Provides the protected computer share name and protected computer computer name in a string.|

### ms\-BackupSrv\-Share Attribute
The following table provides a detailed description of the **ms\-BackupSrv\-Share** attribute:

|Attribute|Value|
|-------------|---------|
|objectClass|Top|
|objectClass|attributeSchema|
|attributeID|1.2.840.113556.1.6.33.2.23|
|attributeSyntax|2.5.5.12|
|rangeUpper|260|
|isSingleValued|TRUE|
|showInAdvancedViewOnly|TRUE|
|adminDisplayName|ms\-BackupSrv\-Share|
|adminDescription|Identifies a server with shared resources.|
|oMSyntax|64|
|IDAPDisplayName|ms\-backupSrvShare|
|objectCategory|CN\=Attribute\-Schema,<SchemaContainerDN>|

### ms\-ProductionSrv\-Share Attribute
The following table provides a detailed description of the **ms\-ProductionSrv\-Share** attribute:

|Attribute|Value|
|-------------|---------|
|objectClass|Top|
|objectClass|attributeSchema|
|attributeID|1.2.840.113556.1.6.33.2.24|
|attributeSyntax|2.5.5.12|
|rangeUpper|260|
|isSingleValued|TRUE|
|showInAdvancedViewOnly|TRUE|
|adminDisplayName|ms\-ProductionSrv\-Share|
|adminDescription|Identifies a computer with shared resources.|
|oMSyntax|64|
|IDAPDisplayName|ms\-productionSrvShare|
|objectCategory|CN\=Attribute\-Schema,<SchemaContainerDN>|


