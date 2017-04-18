---
title: Seal a Service Manager management pack
description: Describes how to seal a Service Manager management pack for use with Service Manager authoring.
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
ms.assetid: 240ef642-dba3-416a-b048-df98d947cbaf
---

# Seal a Service Manager management pack

>Applies To: System Center 2016 - Service Manager

When a management pack in Service Manager contains base definitions that other management packs have to reference, such as a list, it must be sealed. After you seal a management pack, you cannot directly modify objects in the sealed management pack, and you cannot unseal the sealed management pack, but you can define references to objects in the sealed management packs.  

 For more information about how to modify objects that are stored in a management pack that you have already sealed, see [Management Packs: Key Concepts](../../scsm/mps-in-auth-tool.md).  

 Sealing a management pack requires using a key file that provides additional identity to a management pack, and it contains a public\/private key pair. Before you can seal a management pack, you must create this file in advance. For more information about how to create the required key file, see [How to: Create a Public/Private Key Pair](http://go.microsoft.com/fwlink/p/?LinkID=193188). After you create the key file, store it in a safe location.  

 We recommend that you sign a management pack after it is sealed. Signing a management pack is important in ensuring that the file is not modified when you transfer the file between locations. The key that you use for signing a management pack is the same key that is used in the process of cryptographically signing any file. You can use the same key for both sealing and signing a management pack, because the public portion of the key is used for sealing.  

### To seal a Service Manager management pack  

1.  Create an .snk key file that contains a public\/private key pair.  

2.  In the Service Manager Authoring Tool, in **Management Pack Explorer**, right\-click the management pack that you want to seal, and then click **Seal Management Pack**.  

3.  In the **Seal Management Pack** dialog box, in the **Key File** box, enter the location of the key file that you previously created. The file must have an .snk extension. You must also fill in the **Company** box. Filling in the other boxes is optional.  

4.  Click **Seal** to create a sealed management pack, which will be stored in the folder that you specify in the **Output Directory** box.  
