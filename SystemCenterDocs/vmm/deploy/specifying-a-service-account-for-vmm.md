---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Specifying a Service Account for VMM
ms.technology:  virtual-machine-manager
ms.assetid:  edaf90db-563d-4fd3-b6ef-55ea5abc7835
---

# Specifying a Service Account for VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

During the installation of a VMM management server, on the **Configure service account and distributed key management** page, you will need to configure the System Center Virtual Machine Manager service to use either the Local System account or a domain account.

Consider the following before you configure the account that is used by the Virtual Machine Manager service:

-   It is not supported to change the identity of the Virtual Machine Manager service account after installation. This includes changing from the local system account to a domain account, from a domain account to the local system account, or changing the domain account to another domain account. To change the Virtual Machine Manager service account after installation, you must uninstall VMM (selecting the **Retain data** option if you want to keep the SQL Server database), and then reinstall VMM by using the new service account.

-   If you specify a domain account, the account must be a member of the local Administrators group on the computer.

-   If you specify a domain account, it is strongly recommended that you create an account that is specifically designated to be used for this purpose. When a host is removed from the VMM management server, the account that the System Center Virtual Machine Manager service is running under is removed from the local Administrators group of the host. If the same account is used for other purposes on the host, this can cause unexpected results.

-   If you plan to use shared ISO images with Hyper-V virtual machines, you must use a domain account.

-   If you are using a disjointed namespace, you must use a domain account. For more information about disjointed namespaces, see [Naming conventions in Active Directory for computers, domains, sites, and OUs](http://support.microsoft.com/kb/909264).

-   If you are installing a highly available VMM management server, you must use a domain account.



