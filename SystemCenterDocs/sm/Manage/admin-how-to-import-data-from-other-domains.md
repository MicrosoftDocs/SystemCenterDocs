---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Import Data from Other Domains
ms.technology:  service-manager
ms.assetid:  c5a328de-e3c2-44ce-ba4c-c5447c1cb9f9
---

# How to Import Data from Other Domains

>Applies To: System Center 2016 Technical Preview - Service Manager

You can import data from domains other than the domain in which Service Manager resides. For example, Service Manager is installed in domain A (where the fully qualified domain name [FQDN] is a.woodgrove.com), and you want to import data from domain B (where the FQDN is b.woodgrovetest.net). In this scenario, you must think about how to specify the data source path and how to specify the Run As account.

In domain B, either identify an existing service account or create a new one for this purpose. This service account must be a domain account and must be able to read from Active Directory Domain Services.

Next, in Service Manager, create a new Active Directory connector in the Active Directory Connector Wizard. Follow these steps on the **Domain or organizational unit** page.

### To specify the data source path and Run As account

1.  Use the appropriate method, according to where the domains are located:

    -   If the two domains are in the same forest, in the **Server Information** area, select **Let me choose the domain or OU**, and then click **Browse** to select the domain and organizational unit (OU).

    -   If the two domains are in different forests, in the **Server Information** area, select **Let me choose the domain or OU**, and then type the domain and OU in the box. For example, type **LDAP://b.woodgrovetest.net/OU=*OU Name*,DC=b,DC=woodgrovetest,DC=net**.

2.  In the **Credentials** area, click **New**.

3.  In the **Run As Account** dialog box, in the **User name**, **Password**, and **Domain** boxes, type the credentials for the service account from the b.woodgrovetest.net domain.

    > [!NOTE]
    > If the two domains are in different forests, you must type the domain name in the **User name** box. For example, type `b.woodgrovetest.net\UserName`.
