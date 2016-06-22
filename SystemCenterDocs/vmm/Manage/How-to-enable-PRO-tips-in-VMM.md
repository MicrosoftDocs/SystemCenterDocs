---
title: How to enable PRO tips in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99bb953e-941d-4f75-9199-77599c4a396b
---
# How to enable PRO tips in VMM
Virtual Machine Manager \(VMM\) supports Performance and Resource Optimization \(PRO\). To implement PRO, you need to establish a connection with a management server in the management group, as detailed in [How to connect VMM to Operations Manager](How-to-connect-VMM-to-Operations-Manager.md), and then enable PRO.

VMM includes default PRO monitors for dynamic memory to monitor virtual machine dynamic memory allocation issues and maximum virtual machine memory aggregations on Hyper\-V hosts. For more information, see [Configuring dynamic optimization and power optimization in VMM](Configuring-dynamic-optimization-and-power-optimization-in-VMM.md) and the VMM Management Pack documentation.

You can enable PRO when you first establish the connection with Operations Manager or use this procedure to enable it later.

**Account requirements** You must be a member of the Administrator user role to set up and modify the connection to an Operations Manager server.

### To enable Performance and Resource Optimization

1.  In the VMM console, open the **Settings** workspace.

2.  In the **Settings** pane, click **System Center Settings**, and then click **Operations Manager Server**.

3.  On the **Home** tab, in the **Properties** group, click **Properties**.

4.  In the **Details** page, under **Connection Settings**, select **Enable Performance and Resource Optimization \(PRO\)**, and then click **OK**.

If you have an Operations Manager agent installed on the VMM management server, as recommended, you can test whether PRO Tips are working by clicking **Test PRO** in the **Operations Manager Settings** dialog box. Check on the result of your test PRO Tip either in the **Jobs** workspace in the VMM console or in the operations console in Operations Manager.

> [!NOTE]
> Allow up to ten minutes before using **Test PRO**.

## See Also
[Integrating VMM and System Center Operations Manager](Integrating-VMM-and-System-Center-Operations-Manager.md)
[Monitoring and reporting for VMM resources](Monitoring-and-reporting-for-VMM-resources.md)


