---
title: Backing Up Service Manager Management Servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fd32574-f1fd-44c7-b466-620d18998b12
 

















---
# Backing Up Service Manager Management Servers
When you deploy System Center 2012 - Service Manager, an encryption key is created and stored in the registry on the management servers. A matching encryption key is created in the associated databases. The encryption keys for the Service Manager and data warehouse management servers are stored in the Service Manager database. The matching encryption key for the data warehouse management server is stored in the DWStagingAndConfig database. By backing up the SQL Server databases, you back up the encryption key.  
  
 In addition, the computer name of the management server and Self-Service Portal is stored in the associated databases. Regardless of whether you encounter a software or hardware failure of a management server or Self-Service Portal, your recovery process is based on restoring a computer that has the same computer name as the computer that failed.  
  
 The steps for recovering from a management server failure are as follows:  
  
1.  Restore the encryption keys before you run Setup, and install the new management servers.  
  
2.  Install the new management server on a computer that has the same name as the original computer.  
  
3.  When you install the management server, select **Use an existing database**, and then specify the name of the computer that hosts the associated database.  
  
 For more information about these steps, see the topic [Management Server Disaster Recovery in Service Manager](../../../sm/manage/disaster/Management-Server-Disaster-Recovery-in-Service-Manager.md) in this guide.  
  
## In This Section  
 [How to Back Up the Encryption Key in Service Manager](../../../sm/manage/disaster/How-to-Back-Up-the-Encryption-Key-in-Service-Manager.md)  
 Describes how to back up the Service Manager encryption key.
