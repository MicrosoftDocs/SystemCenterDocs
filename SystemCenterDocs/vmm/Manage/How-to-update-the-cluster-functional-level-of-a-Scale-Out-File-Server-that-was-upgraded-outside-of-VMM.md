---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to update the cluster functional level of a Scale Out File Server that was upgraded outside of VMM
ms.technology:  virtual-machine-manager
ms.assetid:  da460702-9f28-4850-af7f-494370b047d8
---

# How to update the cluster functional level of a Scale-Out File Server that was upgraded outside of VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

If you use the upgrade wizard to upgrade a Windows Server 2012 R2 Scale-Out File Server to Windows Server Technical Preview, the wizard performs this step automatically.  However, you may encounter circumstances where you need to perform this operation manually. For example, if a Scale-Out File Server's nodes were upgraded before you brought the Scale-Out File Server into VMM but the it is still functioning as a Windows Server 2012 R2 Scale-Out File Server, you can use this procedure to update it to a Windows Server Technical Preview Scale-Out File Server.

### To update the cluster functional level of a Scale-Out File Server whose nodes were upgraded outside of VMM

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage** > **File Servers**, and in the **File Servers** pane, locate the Scale-Out File Server.

3.  Right-click the Scale-Out File Server you want to update, and click **Update Version**.

## See Also
[Upgrading Windows Server 2012 R2 Scale-Out File Servers to Windows Server 2016 Technical Preview in VMM](Upgrading-Windows-Server-2012-R2-Scale-Out-File-Servers-to-Windows-Server-2016-Technical-Preview-in-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



