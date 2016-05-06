---
title: Set up end-user and self-service recovery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92414f96-dcc3-4630-a9b5-094039a8f422
---
# Set up end-user and self-service recovery
You can enable the end\-user recovery option to allow end users to independently recover data by retrieving recovery points of files. Users can recover data through shared folders on the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, through a Distributed File System \(DFS\) namespace, or by using the **Document Recovery** task pane in Microsoft Office. Enabling end\-user recovery involves enabling the end\-user recovery feature on the DPM server and installing the shadow copy client software on the client computers.

End\-user recovery is supported in the Active Directory Domain Services \(AD DS\) domains in which the domain controllers are running either Windows Server 2003 or Windows 2000 Server with Service Pack 4 or later, Windows Server 2003, Windows Server 2008, Windows Server 2012, and Windows Server 2012 R2 with schema modifications enabled.

## In this section
[Configure end-user recovery and recover file data](../Topic/Configure-end-user-recovery-and-recover-file-data.md)—Describes how to set up end\-user recovery for file data, the changes required in AD DS, and how to recover file data.

[Configure self-service recovery and recover SQL Server data](../Topic/Configure-self-service-recovery-and-recover-SQL-Server-data.md)—Describes how to setup self\-service recovery for SQL Server databases, and how to recover database data.

