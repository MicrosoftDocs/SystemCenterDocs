---
title: Disable support for SSL 2.0
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33dd388d-f131-4b38-969b-3b24f53953a2
---
# Disable support for SSL 2.0
SSL 2.0 was originally released in 1995. Since that time a number of security flaws have been discovered and therefore, SSL 2.0 no longer meets our security standards. [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] defaults to using SSL 3.1 however it is possible that during the SSL handshake process, the operating system might fall back to using SSL 2.0. To prevent this from occurring, you should explicitly disable the use of SSL 2.0 in the operating system. For more information see the Microsoft Knowledge Base article [How to disable PCT 1.0, SSL 2.0, SSL 3.0, or TLS 1.0 in Internet Information Services](http://support.microsoft.com/kb/187498).

## See Also
[Securing VMM resources](../Topic/Securing-VMM-resources.md)

