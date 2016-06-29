---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Disable support for SSL 2.0
ms.technology:  virtual-machine-manager
ms.assetid:  33dd388d-f131-4b38-969b-3b24f53953a2
---

# Disable support for SSL 2.0

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

SSL 2.0 was originally released in 1995. Since that time a number of security flaws have been discovered and therefore, SSL 2.0 no longer meets our security standards. Virtual Machine Manager (VMM) defaults to using SSL 3.1 however it is possible that during the SSL handshake process, the operating system might fall back to using SSL 2.0. To prevent this from occurring, you should explicitly disable the use of SSL 2.0 in the operating system. For more information see the Microsoft Knowledge Base article [How to disable PCT 1.0, SSL 2.0, SSL 3.0, or TLS 1.0 in Internet Information Services](http://support.microsoft.com/kb/187498).

## See Also
[Securing VMM resources](Securing-VMM-resources.md)



