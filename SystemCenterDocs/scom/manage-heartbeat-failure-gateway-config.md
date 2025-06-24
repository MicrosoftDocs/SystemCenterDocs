---
ms.assetid:
title: Configure Computer Not Reachable Recovery Task for Gateway Servers
description: This article describes how to configure the diagnostic task to ping computer on heartbeat failure for agents reporting to an Operations Manager gateway server.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Configure Computer Not Reachable recovery task for gateway servers


When an agent fails to send a heartbeat, a Health Service Heartbeat Failure alert is generated and the management server attempts to contact the computer by performing a ping using Windows Management Instrumentation (WMI) based on its recovery task **Ping Computer on Heartbeat Failure**. If the computer doesn't respond to the ping, a Failed to Connect to Computer alert is generated. By default, this recovery task is performed from its assigned management server.  But when agents report to a gateway server that communicates with its assigned management server through a firewall, the attempt to ping the remote agent will fail.  The following steps describe how to configure the gateway server in this scenario to attempt to contact the computer and verify it's responding to a ping.  

## Prerequisites

RPC port 135 (DCOM/RPC) must be open between the management server and the gateway server in order for it to remotely connect to the WMI provider on the gateway server. Initially the management server binds to port 135 and then a dynamically assigned port above 1024 is selected.  For further information, review [How to configure RPC dynamic port allocation to work with firewalls](https://support.microsoft.com/help/154596/how-to-configure-rpc-dynamic-port-allocation-to-work-with-firewalls).

## Configuration

1. Sign in to the computer hosting the Operations Manager Operations console. Use an account that is a member of the Operations Manager Administrators role for the Operations Manager management group.
2. In the Operations console, select **Authoring**.
    >[!NOTE]
    >When you run the Operations console on a computer that isn't a management server, the **Connect To Server** dialog appears. In the **Server name** box, enter the name of the management server to which you want to connect.

3. In the **Authoring** workspace, in the navigation pane under **Management Pack Objects**, select **Monitors**.
4. From the toolbar, select **Change Scope...** and in the **Scope Management Pack Objects** window, select the option **View all targets** and select **Clear All** if enabled, to deselect any preselected classes you might have filtered earlier.
5. Search for the class **Health Service Watcher** and select it by selecting the checkbox to the left of the class name under the **Target** column. Select **OK** to accept your selection.  
6. Expand the health category **Availability** and select the **Health Service Heartbeat Failure** monitor.  From the Operations console toolbar, select **Overrides** and then point to **Override Diagnostic**, select **Ping Computer on Heartbeat Failure** and then choose to override **For a group...** or **For all objects of class: Health Service Watcher**.
7. Override the value for **Source Computer** parameter with the Fully Qualified Domain Name (FQDN) of the gateway server that you want the ping to be performed from when this monitored object reports a heartbeat failure.

For agents reporting to a gateway server, you need to configure the **Automatic Agent Management Account** Run As account that is used to automatically diagnose agent failures (for example, heartbeat failures and failure to receive data) so the Run As account has privileges to both the management server and the gateway. Otherwise, the recovery task will fail on a gateway server.  This scenario is only supported if:

1. The gateway server is a member of an Active Directory trusted forest, but outside the Kerberos trust boundary of the management group.
2. The gateway server is a member of the same Active Directory forest as the Operations Manager management servers. The gateway server in this case is used because of a firewall or a member of a local resource pool.

Perform the following steps to configure the Run As account.

1. Create a new Run As account of type Windows.  To perform this task, see [How to create a Run As account and associate with a Run As profile](manage-security-create-runas-link-profile.md).  When you're at the step to configure distribution of the account, select **More Secure** and distribute the credentials to the gateway servers and **All Management Servers Resource Pool**.  
2. Add the Run As account to the **Automatic Agent Management Account Profile** and then choose the option **All targeted objects**.

    >[!NOTE]
    >While the gateway server pings the agent, initiation occurs from management server using a WMI query that runs against agents reporting to the gateway server.  For this reason, the **Automatic Agent Management Account** Run As account needs to have the necessary privileges on both the management and gateway server to execute this WMI query from both roles. For more information on how to properly configure privileges to remotely connect to a computer using WMI, see [Securing a Remote WMI Connection](/windows/win32/wmisdk/securing-a-remote-wmi-connection).

## Next steps

To learn more about how to investigate an agent heartbeat failure and ways to resolve them, review [Resolving Heartbeat Alerts](manage-agent-resolve-heartbeat.md).
