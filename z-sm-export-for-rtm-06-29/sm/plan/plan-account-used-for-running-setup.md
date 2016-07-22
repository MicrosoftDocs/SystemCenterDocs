---
title: Account Used for Running Setup
ms.custom: na
ms.prod: system-center-2016
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45dff8a2-a4d5-4314-8385-c5037870ae0f
---
# Account Used for Running Setup
This topic describes the permissions that you need when you are installing a Service Manager management server and Service Manager console databases and when you are registering the Service Manager management group with the data warehouse management group in System Center 2016 - Service Manager.

> [!NOTE]  
>  The account that you use to run Setup is automatically made an administrator in Service Manager.

## Service Manager Management Server

You need the following permissions when you are installing a Service Manager management server:  

-   Local administrator on the computer that you run Setup on  
-   Local administrator on the computer that will host the Service Manager database if it is on a remote computer  
-   Logged\-on user must be a domain account  
-   The Sysadmin SQL&nbsp;Server role on the SQL&nbsp;Server instance where the Service Manager database is being created  


## Service Manager Console

You need the following permissions when you are installing the Service Manager console:  

-   Local administrator on the computer that you run Setup on  

## Data Warehouse Management Server

You need the following permissions when you are installing the data warehouse management server:  

-   Local administrator on the computer that you run Setup on  
-   Local administrator on the computer that will host the data warehouse database if it is on a remote computer  
-   Logged\-in user must be a domain account  
-   The Content Manager role in SQL&nbsp;Server Reporting Services \(SSRS\) at the site level \(root\)  
-   The Sysadmin SQL&nbsp;Server role on the SQL&nbsp;Server instance where the data warehouse database is being created  

## SQL Server Reporting Services

You need the following permissions when you are installing SSRS:  

-   Permissions to place a binary file into the \\Program Files\\Microsoft SQL Server\\*Instance Name*\Reporting Services\\ReportServer\\Bin folder on the computer hosting the data warehouse management server  

## Registering Service Manager with the Data Warehouse  

You need the following permissions when you are registering Service Manager with the data warehouse:  

-   The Sysadmin or security admin SQL&nbsp;Server role on the instance that is hosting the Service Manager database  
-   The Sysadmin or security admin SQL&nbsp;Server role on the instance that is hosting the data warehouse database  
-   Membership in the Service Manager Administrators user role on the Service Manager management server  
-   Membership in the Service Manager Administrators user role on the data warehouse management server
