---
title: Pre-Creating the VMM Database
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b11a59c-0a54-4815-93f4-3eca84d47da0
---
# Pre-Creating the VMM Database
In some organizations, the system administrator that is installing [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] does not have the necessary permissions to create the database that is required by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. In this case, the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database needs to be created by an authorized administrator before the installation starts. Later, during Setup, you can point at this pre\-created database. The VMM database needs to be pre\-created as described below.

You can create SQL Scripts with the specified parameters, and then hand these scripts to the SQL administrators to ensure that the database is configured correctly.

### How to pre\-create the VMM database

1.  Create a new database with the following settings:

    -   Name: VirtualManagerDB

    -   Collation: Latin1\_General\_100\_CI\_AS, but aligned with the specific SQL Server instance collation

2.  Grant db\_owner permissions for this database to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] service account

3.  Run Setup to install [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], and on the **Database configuration** page, select to use an existing database. Enter the details of the pre\-created database.

4.  Specify the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] service account as the user for the database connection.


