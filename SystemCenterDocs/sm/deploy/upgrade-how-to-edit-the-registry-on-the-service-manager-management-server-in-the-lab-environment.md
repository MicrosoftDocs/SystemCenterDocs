---
title: Edit the registry on the Service Manager management server in the lab environment
description: Edit the registry on the Service Manager management server in the lab environment before you upgrade.
manager: carmonm
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
ms.assetid: 7aa3ae77-88e7-4ff8-bb63-814286b7089d
---

# Edit the registry on the Service Manager Management Server in the lab environment before you upgrade.

>Applies To: System Center 2016 - Service Manager

Use the following procedure to edit the registry on the Service Manager management server in the lab environment.

>[!CAUTION]
Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.

## To edit the registry

1. On the computer hosting the Service Manager management server in the lab environment, log on to the computer as a user with administrative credentials.
2. On the Windows desktop, click **Start**, and then click **Run**.
3. In the **Run** dialog box, in the **Open** box, type *regedit*, and then click **OK**.
4. In the Registry Editor window, expand **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2012\Common\Database**.
5. In the right pane, double-click **DatabaseServerName**.
6. In the **Edit String** box, in the **Value data** box, type the name of the computer hosting the Service Manager database SQL Server in the lab environment. If you are using a named instance of SQL Server, use the Computer Name\Instance name format.
7. Click **OK**, and then close the Registry Editor.
