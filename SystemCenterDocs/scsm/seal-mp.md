---
title: Seal a Service Manager management pack
description: Describes how to seal a Service Manager management pack for use with Service Manager authoring.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 08/07/2025
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 240ef642-dba3-416a-b048-df98d947cbaf

---

# Seal a Service Manager management pack



When a management pack in Service Manager contains base definitions that other management packs have to reference, such as a list, it must be sealed. After you seal a management pack, you can't directly modify objects in the sealed management pack, and you can't unseal the sealed management pack, but you can define references to objects in the sealed management packs.  

 For more information about how to modify objects that are stored in a management pack that you've already sealed, see [Management Packs: Key Concepts](mps-in-auth-tool.md).  

 Sealing a management pack requires using a key file that provides additional identity to a management pack, and it contains a public\/private key pair. Before you can seal a management pack, you must create this file in advance. For more information about how to create the required key file, see [How to: Create a Public/Private Key Pair](/dotnet/standard/assembly/create-public-private-key-pair). After you create the key file, store it in a safe location.  

 We recommend that you sign a management pack after it's sealed. Signing a management pack is important in ensuring that the file isn't modified when you transfer the file between locations. The key that you use for signing a management pack is the same key that is used in the process of cryptographically signing any file. You can use the same key for both sealing and signing a management pack, because the public portion of the key is used for sealing.  

## Seal a management pack

To seal a management pack, follow these steps:

1. Create a .snk key file that contains a public\/private key pair.  

2. In the Service Manager Authoring Tool, in **Management Pack Explorer**, right\-click the management pack that you want to seal, and select **Seal Management Pack**.  

3. In the **Seal Management Pack** dialog, in the **Key File** box, enter the location of the key file that you previously created. The file must have a .snk extension. You must also fill in the **Company** box. Filling in the other boxes is optional.  

4. Select **Seal** to create a sealed management pack, which will be stored in the folder that you specify in the **Output Directory** box.  

## Next steps

[Bundle management packs and resource files](bundle-mps.md).
