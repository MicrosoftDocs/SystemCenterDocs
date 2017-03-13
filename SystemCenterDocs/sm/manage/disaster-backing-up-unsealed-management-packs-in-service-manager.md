---
title: Back up unsealed management packs
description: Describes how to back up Service Manager unsealed management packs for disaster recovery.
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
ms.assetid: 368ac173-ab92-4ce7-a494-76c48c466976
---

# Back up Service Manager unsealed management packs

>Applies To: System Center 2016 - Service Manager

Part of the disaster recovery plan for your Service Manager management server involves backing up your unsealed management packs. The following procedure describes how to back up your unsealed management packs.  

## Back up unsealed management packs

You can use the Windows&nbsp;PowerShell command\-line interface to identify and copy your unsealed management packs to a folder on your hard disk drive. After you copy them, save these management packs so that-as part of your disaster recovery plan for Service Manager-you can later import these management packs.  

### To back up unsealed management packs  

1.  On the computer that hosts the Service Manager management server, create a folder on the hard disk drive where you will store the backup copy of the management packs. For example, create the folder C:\\mpbackup.  

2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Windows&nbsp;PowerShell&nbsp;1.0**, right\-click **Windows&nbsp;PowerShell**, and then click **Run as administrator**.  

3.  In the Service Manager console, click **Administration**.  

4.  In the **Tasks** pane, click **Start PowerShell Session**  

5.  At the Windows&nbsp;PowerShell command prompt, type the following command:  

    ```  
    Get-SCSMManagementPack | where {$_.Sealed -eq $false}|Export-SCSMManagementPack -Path c:\mpbackup  
    ```  

6.  Save the unsealed management packs on a separate physical computer.
