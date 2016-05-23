---
title: How to configure SQL Server Analysis Services for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3af9228e-96a3-4eea-a97c-0c5bfa95d937
---
# How to configure SQL Server Analysis Services for VMM
You can integrate [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] with SQL Server Analysis Service \(SSAS\) in order to provide forecasting reports. Be sure that SQL Server Analysis Services are installed on the [!INCLUDE[om12short](../../Token/om12short_md.md)] Reporting server.

Before you enable SSAS, you need to connect to an [!INCLUDE[om12short](../../Token/om12short_md.md)] management server, as described in [How to connect VMM to Operations Manager](How-to-connect-VMM-to-Operations-Manager.md).

> [!IMPORTANT]
> SSAS requires Analysis Management Objects \(AMO\) be installed on the VMM management server. To download AMO, see the[Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) or the [Microsoft SQL Server 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295).

**Account requirements** You must be a member of the Administrator user role to configure SSAS.

### To configure SQL Server Analysis Service

1.  In the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console, open the **Settings** workspace.

2.  In the **Settings** pane, click **System Center Settings**, and then click **Operations Manager Server**.

3.  On the **Home** tab, in the **Properties** group, click **Properties** to open the **Operations Manager Settings** dialog box.

4.  On the **SQL Server Analysis Services** page, click **Enable SSAS**.

5.  Enter the **SSAS server**, **SSAS instance**, and SSAS **Port**.

    The instance name must be the same as the SQL Server Reporting Services, by default MSSQLSERVER.

    The default port is 0.

    > [!IMPORTANT]
    > Make sure that SQL Server Reporting Services allows reports access using default port 80 and has HTTP access to reports.

6.  Select either a Run As account or enter a user name and password, and then click **OK**.

    This user must belong to the [!INCLUDE[om12short](../../Token/om12short_md.md)] Report Security Administrator profile.

## See Also
[Integrating VMM and System Center Operations Manager](Integrating-VMM-and-System-Center-Operations-Manager.md)
[Monitoring and reporting for VMM resources](Monitoring-and-reporting-for-VMM-resources.md)


