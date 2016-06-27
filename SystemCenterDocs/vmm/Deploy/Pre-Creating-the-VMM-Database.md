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

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

In some organizations, the system administrator that is installing Virtual Machine Manager (VMM) does not have the necessary permissions to create the database that is required by VMM. In this case, the VMM database needs to be created by an authorized administrator before the installation starts. Later, during Setup, you can point at this pre-created database. The VMM database needs to be pre-created as described below.

You can create SQL Scripts with the specified parameters, and then hand these scripts to the SQL administrators to ensure that the database is configured correctly.

### How to pre-create the VMM database

1.  Create a new database with the following settings:

    -   Name: VirtualManagerDB

    -   Collation: Latin1_General_100_CI_AS, but aligned with the specific SQL Server instance collation

2.  Grant db_owner permissions for this database to the VMM service account

3.  Run Setup to install VMM, and on the **Database configuration** page, select to use an existing database. Enter the details of the pre-created database.

4.  Specify the VMM service account as the user for the database connection.



