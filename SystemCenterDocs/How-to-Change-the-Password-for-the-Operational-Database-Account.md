---
title: How to Change the Password for the Operational Database Account
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cc6e765-1cfd-4e0a-aac6-2b5fd3b671b5
---
# How to Change the Password for the Operational Database Account

### To change the log\-on password for the [!INCLUDE[smshort](./Token/smshort_md.md)] Data Access and [!INCLUDE[smshort](./Token/smshort_md.md)] Management Configuration services

1.  On the Windows desktop, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, in the **Open** box, type **services.msc**, and then click **OK**.

3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **System Center Data Access Service**, and then click **Properties**.

4.  In the **System Center Data Access Service Properties \(Local Computer\)** dialog box, click **Log On**.

5.  Type the new password in the **Password** and **Confirm Password** text boxes, and then click **OK**.

6.  Restart the [!INCLUDE[smshort](./Token/smshort_md.md)] Data Access Service.

7.  Right\-click **System Center Management Configuration**, and then click **Properties**.

8.  In the **System Center Management Configuration Properties \(Local Computer\)** dialog box, click **Log On**.

9. Type the new password in the **Password** and **Confirm Password** text boxes, and then click **OK**.

10. Restart the System Center Management Configuration service.


