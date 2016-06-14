---
title: How to connect VMM to Operations Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43c1b9f1-a8cf-4075-81df-2e78d64c3cfb
---
# How to connect VMM to Operations Manager
You can connect [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)] to [!INCLUDE[om12short](../../includes/om12short_md.md)] so that they work in an integrated way. To connect [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to [!INCLUDE[om12short](../../includes/om12short_md.md)], you must choose a supported version of [!INCLUDE[om12short](../../includes/om12short_md.md)], as described in [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Deploy/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

You must also configure the [!INCLUDE[om12short](../../includes/om12short_md.md)] server to work with [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

> [!NOTE]
> The version of the [!INCLUDE[om12short](../../includes/om12short_md.md)] operations console that is installed on the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server must match the version of [!INCLUDE[om12short](../../includes/om12short_md.md)] with which you intend to integrate.

This topic contains the following sections:

-   [Prerequisites](How-to-connect-VMM-to-Operations-Manager.md#BKMK_prerequisites)

-   [Set up integration with Operations Manager](How-to-connect-VMM-to-Operations-Manager.md#BKMK_integration)

-   [Update management packs](How-to-connect-VMM-to-Operations-Manager.md#BKMK_packs)

-   [Remove an Operations Manager server connection](How-to-connect-VMM-to-Operations-Manager.md#BKMK_remove)

## <a name="BKMK_prerequisites"></a>Prerequisites
Before you connect [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to [!INCLUDE[om12short](../../includes/om12short_md.md)], perform the following actions:

1.  Ensure that the version of Windows PowerShell that's on all [!INCLUDE[om12short](../../includes/om12short_md.md)] management servers is the most recent version supported by that version of [!INCLUDE[om12short](../../includes/om12short_md.md)].

    To determine which version of Windows PowerShell is on a server, run the following:

    **Get\-Host | Select\-Object Version**

2.  Make sure that port 5724 is open between [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] and [!INCLUDE[om12short](../../includes/om12short_md.md)].

3.  Install an [!INCLUDE[om12short](../../includes/om12short_md.md)] operations console on the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server.

4.  Install [!INCLUDE[om12short](../../includes/om12short_md.md)] agents on the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server and all hosts under management by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] \(managed hosts\). For more information, see[Operations Manager Agent Installation Methods](http://technet.microsoft.com/library/hh551142.aspx).

5.  Verify that the managed hosts on which you installed agents are visible in [!INCLUDE[om12short](../../includes/om12short_md.md)] by performing the following actions:

    1.  In the **Operations** console, click **Administration**.

    2.  In the **Administration** pane, under **Device Management**, click **Agent Managed**. Verify that the expected hosts are listed.

    3.  Double\-click a host in the list, click the **Security** tab, and then ensure that **Allow this agent to act as a proxy and discover managed objects on other computers** has been selected. Repeat this step for each of the hosts.

6.  In [!INCLUDE[om12short](../../includes/om12short_md.md)], import the necessary management packs, as described in [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx). You can find management packs, sometimes called “monitoring packs,” by searching the [Microsoft Download Center](http://www.microsoft.com/downloads/default.aspx). The necessary management packs are as follows:

    -   Windows Server Internet Information Services 2003

    -   Management packs that are required by the management pack for Windows Server 2008 Internet Information Services 7:

        -   Windows Server 2008 Operating System \(Discovery\)

        -   Windows Server Operating System Library

    -   Windows Server 2008 Internet Information Services 7

    -   Windows Server Internet Information Services Library

    -   SQL Server Core Library

> [!IMPORTANT]
> You can get the following three prerequisite management packs in one download from [Windows Server Internet Information Services 7 Management Pack for System Center Operations Manager 2007](http://www.microsoft.com/download/details.aspx?id=9815):
> 
> -   Microsoft.Windows.InternetInformationServices.2000.MP
> -   Microsoft.Windows.InternetInformationServices.2003.MP
> -   Microsoft.Windows.InternetInformationServices.2008.MP
> 
> These management packs allow you to maintain monitoring data from previous releases when you upgrade to [!INCLUDE[sc_threshold_1](../../includes/sc_threshold_1_md.md)].

**Account requirements** You must be a member of the Administrator user role to set up and modify the connection to an [!INCLUDE[om12short](../../includes/om12short_md.md)] server.

## <a name="BKMK_integration"></a>Set up integration with Operations Manager

#### To set up integration with Operations Manager

1.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, open the **Settings** workspace.

2.  In the **Settings** pane, click **System Center Settings**, and then click **Operations Manager Server**.

3.  On the **Home** tab, in the **Properties** group, click **Properties**.

    > [!NOTE]
    > If the [!INCLUDE[om12short](../../includes/om12short_md.md)] connection has already been established, clicking **Properties** opens the **Operation Manager Settings** dialog box. If this dialog box appears and does not describe the correct connection, remove the current connection before you enter the correct information.

4.  Review the information in the **Introduction** page, and then click **Next**.

5.  In the **Connection to Operations Manager** page, enter the **Server name** for a management server in the management group, and select an account to use to connect. You can use the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] server service account or specify a Run As account.

    > [!IMPORTANT]
    > This account must be a member of the [!INCLUDE[om12short](../../includes/om12short_md.md)] Administrator role.

6.  Select **Enable Performance and Resource Optimization \(PRO\)**, if desired.

7.  Select **Enable maintenance mode integration with Operations Manager**, if desired.

    When hosts are placed in maintenance mode using the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server, [!INCLUDE[om12short](../../includes/om12short_md.md)] places them in maintenance mode as well. In this mode, the [!INCLUDE[om12short](../../includes/om12short_md.md)] agent suppresses alerts, notifications, rules, monitors, automatic responses, state changes, and new alerts.

    [!INCLUDE[om12short](../../includes/om12short_md.md)] automatically places virtual machines in maintenance mode when they are moved to the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] library.

8.  Click **Next**.

9. Enter credentials for [!INCLUDE[om12short](../../includes/om12short_md.md)] to connect with the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server, and then click **Next**.

    This account will be added to the Administrator user role in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

10. Review the information in the **Summary** page, and click **Finish**.

    You can view the status of the new connection in the **Jobs** workspace.

11. With **System Center Settings** still selected, in the results pane, right\-click **Operations Manager Server**, and then click **Properties**.

    The **Operation Manager Settings** dialog box opens.

12. Click the **Details** tab. Next to **Connection Status**, confirm that the connection is **OK**.

Verify that the integration is complete by opening the Operations console in [!INCLUDE[om12short](../../includes/om12short_md.md)] and selecting the **Monitoring** workspace. In the navigation pane, review the following entries:

-   **Virtual Machine Manager**

    Includes health and performance information for virtual machines, hosts, and [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] servers.

-   **Virtual Machine Manager Views**

    Displays diagrams for managed systems.

    > [!NOTE]
    > The diagrams themselves will not be available until several hours after you complete this procedure.

When you use the preceding procedure to set up integration with [!INCLUDE[om12short](../../includes/om12short_md.md)], the monitoring pack for [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] is imported into [!INCLUDE[om12short](../../includes/om12short_md.md)]. For more information about the monitoring pack, see [Guide for System Center Monitoring Pack for System Center 2012 - Virtual Machine Manager](http://technet.microsoft.com/library/jj126982.aspx).

When you set up integration with [!INCLUDE[om12short](../../includes/om12short_md.md)], the Fabric Health Dashboard is also imported into [!INCLUDE[om12short](../../includes/om12short_md.md)]. For more information about the Fabric Health Dashboard, see [Fabric Monitoring](http://technet.microsoft.com/library/dn458592.aspx).

## <a name="BKMK_packs"></a>Update management packs

#### To update management packs

1.  On the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server, open the management packs directory. By default, the directory location is C:\\Program Files\\Microsoft System Center 2012\\Virtual Machine Manager\\ManagementPacks.

2.  Back up the existing .mp files.

3.  Extract the new .mp files to the management pack directory, overwriting the existing .mp files.

4.  If you have already integrated [!INCLUDE[om12short](../../includes/om12short_md.md)] with [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], in the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, in the **Settings** workspace, remove the [!INCLUDE[om12short](../../includes/om12short_md.md)] server by using the procedure in this topic.

5.  Connect to the [!INCLUDE[om12short](../../includes/om12short_md.md)] server, by using the procedure in this topic.

After the connection has been set up, open the **Settings** workspace. In the **Settings** pane, click **System Center Settings**.  In the results pane, right\-click **Operations Manager Server**, and then click **Properties**. On the **Management Pack** page, verify the installed version of the management packs.

## <a name="BKMK_remove"></a>Remove an Operations Manager server connection

#### To remove an [!INCLUDE[om12short](../../includes/om12short_md.md)] server connection

1.  In the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, open the **Settings** workspace.

2.  In the **Settings** pane, click **System Center Settings**, right\-click **Operations Manager Server**, and then click **Remove**.

    When prompted, verify that you want to remove the server.

You can check the progress of the removal in the **Jobs** workspace.

> [!NOTE]
> The [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management packs are not removed from [!INCLUDE[om12short](../../includes/om12short_md.md)], but any Connectors that have been added are removed. \(A Connector is a custom service or program that makes it possible for [!INCLUDE[om12short](../../includes/om12short_md.md)] to communicate with other software.\)

If you want to reconnect [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to the [!INCLUDE[om12short](../../includes/om12short_md.md)] server, see [To set up integration with Operations Manager](How-to-connect-VMM-to-Operations-Manager.md#BKMK_integration).

## See Also
[Integrating VMM and System Center Operations Manager](Integrating-VMM-and-System-Center-Operations-Manager.md)
[Monitoring and reporting for VMM resources](Monitoring-and-reporting-for-VMM-resources.md)


