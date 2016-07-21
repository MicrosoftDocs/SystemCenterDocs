---
title: Disaster Recovery Scenarios Overview
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 21a896b4-ce2c-4d5b-90eb-7d6d024b5eef
 

















---
# Disaster Recovery Scenarios Overview
This topic provides an overview of the disaster recovery processes for each of the major parts of a System Center 2012 - Service Manager installation:  
  
1.  Service Manager Management Server  
  
2.  Data Warehouse Management Server  
  
3.  Service Manager Databases  
  
## Service Manager Management Server  
 You can take two approaches to restoring a failed Service Manager management server. You can replace the management server, or you can promote an additional management server to the primary role if an additional management server exists. The option of replacing the management server or promoting it depends largely on your time frame. If you can bring up another computer quickly, you might choose that option. Otherwise, you can promote an additional management server to the primary role and then add another management server later.  
  
 Promoting an additional management server involves the following procedures:  
  
1.  Promote an additional Service Manager management server. For more information, see [How to Promote a Service Manager Management Server](../../../sm/manage/disaster/How-to-Promote-a-Service-Manager-Management-Server.md) in this guide.  
  
2.  When a replacement server is available, install an additional Service Manager management server. For more information, see "How to Install an Additional Management Server" in the [Deployment Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkId=209670).  
  
 If promoting an additional Service Manager management server is not an option, you have to install a replacement management server. Installing a replacement Service Manager management server involves the following procedures:  
  
1.  Start with a new computer that has the same computer name as the computer that failed.  
  
2.  Restore the encryption key that you saved from the original Service Manager management server. For more information, see [How to Restore the Service Manager Encryption Key](../../../sm/manage/disaster/How-to-Restore-the-Service-Manager-Encryption-Key.md) in this guide.  
  
3.  Install a Service Manager management server. For more information, see "Service Manager for System Center 2012 Deployment Scenarios" in the [Deployment Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209670).  
  
## Data Warehouse Management Server  
 Only one recovery scenario is possible for the data warehouse management server: you must install a new data warehouse management server on a computer with the same computer name as the computer that failed. Installing a replacement data warehouse management server involves the following procedures:  
  
1.  Start with a new computer that has the same computer name as the computer that failed.  
  
2.  Restore the encryption key that you saved from the original data warehouse management server. For more information, see [How to Restore the Service Manager Encryption Key](../../../sm/manage/disaster/How-to-Restore-the-Service-Manager-Encryption-Key.md) in this guide.  
  
3.  Install a data warehouse management server. For more information, see "Service Manager for System Center 2012 Deployment Scenarios" in the [Deployment Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209670).  
  
## Service Manager Databases  
 Recovery procedures are the same for both the Service Manager database and the data warehouse database. You use a computer with the same name, and then you restore the Microsoft SQL&nbsp;Server databases using the same instance as the original. Recovery of a Service Manager database and a data warehouse database involves the following procedures:  
  
1.  Start with a new computer with the same computer name and with the same SQL&nbsp;Server instance as the computer that failed.  
  
2.  Restore the SQL&nbsp;Server database or databases using the same instance name as the original. For more information, see [Database Recovery in Service Manager](../../../sm/manage/disaster/Database-Recovery-in-Service-Manager.md) in this guide.
