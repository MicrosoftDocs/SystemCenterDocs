---
title: Perform Client Action activity
description: Describes the configurable properties for the Perform Client Action activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 392c31ad-7e51-46c4-b153-3db61993a160
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---

# Perform Client Action activity for Configuration Manager Integration Pack

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Perform Client Action activity is used to initiate Configuration
Manager client actions by communicating directly with the client. These
client actions can be used to enable more rapid processing of
assignments or policies by the client by bypassing the normal client
polling interval.

This activity connects to the client computer using a remote WMI
connection and doesn't connect to the Configuration Manager Site
server. Specific firewall settings are a prerequisite for this activity
to function correctly. For more information about remote WMI, see
[Connecting to WMI on a Remote Computer in the Microsoft MSDN
Library](/windows/win32/wmisdk/connecting-to-wmi-on-a-remote-computer).

Connecting remotely using WMI also requires appropriate credentials. If
the account used for the Orchestrator Management Service doesn't have
rights to access WMI on the target computer, you'll need to specify an
account that does by using the optional properties on the Connection
tab. For more information about WMI security and connection settings,
see [Securing a Remote WMI Connection in the Microsoft MSDN
Library](/windows/win32/wmisdk/securing-a-remote-wmi-connection).

>[!IMPORTANT]
>Avoid using this activity to refresh a large number of clients simultaneously.

Because this activity targets individual computers and bypasses the normal communication processes of Configuration Manager, including client polling intervals that might be configured for optimal site performance, the use of this activity should be limited to individual computers or small groups of computers targeted by a runbook.

## Perform Client Action properties

- Computer: The NetBIOS name, fully qualified domain name (FQDN), or IP address of the Configuration Manager client.
- Action: The client action to be performed. Options are:
    -   Machine Policy Retrieval & Evaluation Cycle
    -   Software Updates Scan and Deployment Re-evaluation
    -   Application Deployment Evaluation Cycle
    -   Discovery Data Collection Cycle
    -   File Collection Cycle
    -   Hardware Inventory Cycle
    -   Software Inventory Cycle

## Perform Client Action required properties
- Authentication Level: The authentication level used to connect to WMI. Options are:
    -   Packet
    -   Call
    -   Connect
    -   Default
    -   None
    -   Packet Integrity
    -   Packet Privacy (default value)
    -   Unchanged

  For more information, see [Authentication Level Enumeration](/dotnet/api/system.management.authenticationlevel) in the Microsoft MSDN Library.
- Enable Privileges: True or False. When set to True, indicates that user privileges need to be enabled for the connection operation. This property should only be used when the operation performed requires a certain user privilege to be enabled; for example, a computer restart.
- Impersonation Level: Defines the security impersonation level for the WMI connection. Options are:
    -   Impersonate
    -   Anonymous
    -   Default (default value)
    -   Identify
    -   Delegate

  For more information, see [Impersonation Level Enumeration](/dotnet/api/system.management.impersonationlevel) in the Microsoft MSDN Library.
- Locale: The client can request data from the WMI server in a client-preferred locale. This string is specified as MS\_xxx format. The default value for this property is “MS\_409”.

    For more information, see [Locale IDs](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c) in the Microsoft MSDN Library.
- Timeout (Seconds).

## Perform Client Action optional properties
- Authority: Sets the authority used to authenticate the specified user. Options are:
    1.  Kerberos: &lt;Principal name&gt;
    2.  NTLMDOMAIN: &lt;domain name&gt;

  For more information, see [Connection Options Authority](/dotnet/api/system.management.connectionoptions.authority) in the Microsoft MSDN Library.
- Password: The password for the account credentials specified in the Username property
- Username: The account credentials with WMI access to the remote client, in the format domain\\username

## Configuring the Perform Client Action activity

1.  From the **Activities** pane, drag a **Perform Client Action**
    activity to the active runbook.

2.  Double-click the **Perform Client Action** activity icon. The
    **Properties** dialog opens.

3.  Configuring the **Details** tab:

    1.  In the **Connection** section, select the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Select **OK**.

    2.  In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        select the ellipsis **(…)** button next to the text box to browse
        for a value.

        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.

4.  Select the **Connection** tab. Enter a value for each of the required
    properties. If the property is Lookup-enabled, you can select the
    ellipsis button **(…)** next to the text box to browse for a value.
    You can also use published data to automatically populate the value
    of the property from the data output by a previous activity in the
    runbook.

5.  To use additional properties, select **Optional Fields**.

    1.  In the **Select Properties** dialog, select the properties you
        want to apply to this activity from the **Available Properties**
        list, and select the right arrow button **(&gt;&gt;)**. The
        properties appear in the **Selected Properties** list.

    2.  To remove a property from the **Selected Properties** list,
        select the property, and select the left arrow button
        **(&lt;&lt;)**.

    3.  Select **OK** to save the changes.

    4.  Assign values to the properties or **Subscribe** to **Published data** from the previous activity in the runbook.

6.  Select **Finish**.