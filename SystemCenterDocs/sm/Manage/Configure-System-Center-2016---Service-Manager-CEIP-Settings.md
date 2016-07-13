---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Configure System Center 2016   Service Manager CEIP Settings
ms.technology:  service-manager
ms.assetid:  4bb2487c-5a91-44d2-9a85-f4112aff40ac
---

# Configure System Center 2016 - Service Manager CEIP Settings

>Applies To: System Center 2016 Technical Preview - Service Manager

During setup in Service Manager, on the **Help improve System Center** page, you have the option to participate in the Customer Experience Improvement Program (CEIP). For a Service Manager management server, you can use the first following procedure to let Service Manager participate in the program or remove Service Manager from this program. For either a data warehouse management server or Service Manager management server, you use the second following procedure to modify the registry to join or leave the Customer Experience Improvement Program.

### To configure Service Manager CEIP settings using the Service Manager console

1.  In the Service Manager console, in the toolbar, click **Help**.

2.  In the **Help** menu, you can choose to either let Service Manager join the program or remove Service Manager from the program: Observe the entry **Join the Customer Experience Improvement Program**, and then do one of the following:

    -   If a check mark is displayed, click **Join the Customer Experience Improvement Program** to remove Service Manager from the CEIP program.

    -   If the check mark is not displayed, click **Join the Customer Experience Improvement Program** to join the CEIP program, and then in the System Center Service Manager dialog box, click **Yes** to confirm your decision.

### To configure CEIP settings using the registry

1.  On the Service Manager management server or data warehouse server, open Registry Editor.

2.  Create the following registry key if it does not already exist.

    **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient\SCSM**

3.  Create the following DWORD (32-bit) Value if it does not already exist.

    **CEIPEnable**

4.  Set the value to 1 to participate in the CEIP or set the value to 0 to leave the CEIP.



