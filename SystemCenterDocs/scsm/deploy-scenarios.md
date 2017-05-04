---
title: Deploy Service Manager
description: You can install Service Manager for a variety of deployment scenarios.
manager:  carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91a72f45-07ff-41cd-80aa-7acde988f08f
---

# Deployment scenarios for System Center - Service Manager

>Applies To: System Center 2016 - Service Manager

System Center - Service Manager provides for many deployment scenarios. However, remember that you cannot deploy a Service Manager management server and a data warehouse management server on the same computer. In fact, Setup prevents you from installing both on a single server. The reason has to do with Service Manager architecture of the data warehouse, overall performance, and usage of the Operations Manager health service. The data warehouse was designed for quick data retrieval and hosting both the Service Manager management server and the data warehouse management server on a single server will negatively impact performance for both. Additionally, a single server doesn't scale out as Service Manager usage and data storage grow.  

 You will also specify the server that hosts SQL&nbsp;Server Reporting Services \(SSRS\). Do not attempt to use the same SSRS instance for both Operations Manager and Service Manager.  

 This deployment guide describes the following three deployment scenarios: installing Service Manager on one computer, installing Service Manager on two computers, and installing Service Manager on four computers.  

> [!NOTE]  
>  The collation settings for Microsoft SQL&nbsp;Server must be the same for the computers that host the Service Manager database, the computers that host the data warehouse databases, and the computers that host the Reporting Services database. If you intend to import data from Operations Manager, then the database collations must match between Service Manager and Operations Manager.  

 While we do not recommend it \(for performance reasons\), if you want to host the Service Manager management server and the Self-Service Portal on the same computer, you must deploy the Service Manager management server before you deploy the Self-Service Portal.  

 Performing an upgrade from technical preview versions of Service Manager is not supported. Furthermore, for this release, Service Manager setup installs files in predefined folders that might already exist if you have a previous version of Service Manager installed.  

 The user installing Service Manager has access to the Service Connection Point \(SCP\) object of Service Manager in the Active Directory. This SCP stores the information about the service. Client applications, such as Service Manager, can connect to services using the SCP. For more information about service connection points, see [Publishing Services in Active Directory](http://technet.microsoft.com/library/cc961733.aspx).  

## Next steps

- Review [Install on a single computer (minimum configuration)](install-one-computer.md) to install Service Manager on a single computer. This scenario requires you to use a virtual machine for the data warehouse management server. This scenario is useful for evaluation purposes.
