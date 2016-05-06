---
title: Configure System Center 2016 - Service Manager CEIP Settings
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb2487c-5a91-44d2-9a85-f4112aff40ac
---
# Configure System Center 2016 - Service Manager CEIP Settings
During setup in Service Manager, on the **Help improve System Center** page, you have the option to participate in the Customer Experience Improvement Program \(CEIP\). For a [!INCLUDE[smshort](./Token/smshort_md.md)] management server, you can use the first following procedure to let [!INCLUDE[smshort](./Token/smshort_md.md)] participate in the program or remove [!INCLUDE[smshort](./Token/smshort_md.md)] from this program. For either a data warehouse management server or [!INCLUDE[smshort](./Token/smshort_md.md)] management server, you use the second following procedure to modify the registry to join or leave the Customer Experience Improvement Program.

### To configure [!INCLUDE[smshort](./Token/smshort_md.md)] CEIP settings using the [!INCLUDE[smcons](./Token/smcons_md.md)]

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], in the toolbar, click **Help**.

2.  In the **Help** menu, you can choose to either let [!INCLUDE[smshort](./Token/smshort_md.md)] join the program or remove [!INCLUDE[smshort](./Token/smshort_md.md)] from the program: Observe the entry **Join the Customer Experience Improvement Program**, and then do one of the following:

    -   If a check mark is displayed, click **Join the Customer Experience Improvement Program** to remove [!INCLUDE[smshort](./Token/smshort_md.md)] from the CEIP program.

    -   If the check mark is not displayed, click **Join the Customer Experience Improvement Program** to join the CEIP program, and then in the System Center [!INCLUDE[smshort](./Token/smshort_md.md)] dialog box, click **Yes** to confirm your decision.

### To configure CEIP settings using the registry

1.  On the [!INCLUDE[smshort](./Token/smshort_md.md)] management server or data warehouse server, open Registry Editor.

2.  Create the following registry key if it does not already exist.

    **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\SQMClient\\SCSM**

3.  Create the following DWORD \(32\-bit\) Value if it does not already exist.

    **CEIPEnable**

4.  Set the value to 1 to participate in the CEIP or set the value to 0 to leave the CEIP.


