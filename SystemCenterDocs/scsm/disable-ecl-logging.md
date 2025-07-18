---
title: Optionally disable ECL logging for faster connector synchronization
description: Describes how you can optionally disable Service Manager ECL logging for faster connector synchronization.
ms.custom: UpdateFrequency3, engagement-fy24
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.assetid: 805b479a-9312-4039-be44-01dda07086d8
---

# Optionally disable Service Manager ECL logging for faster connector synchronization



You can watch this [video](https://channel9.msdn.com/Blogs/hybrid-it-management/Demo-Optionally-Disable-ECL-Logging-for-Faster-Connector-Synchronization-with-Service-Manager?ocid=player) for a quick overview of this feature. For more details, continue reading the article.

The Active Directory (AD) and System Center Configuration Manager (SCCM) connectors in Service Manager can import large amounts of data into the Service Manager database. In doing so, they not only increase the size of the data table, which is where the data from the connectors are stored, but they also increase the size of the EntityChangeLog (ECL) table and history tables considerably. A large ECL table size can be a problem in some cases; it can slow down the system significantly.

The ECL table, and the history tables in this case, store details about when the data was brought into Service Manager and the properties that were added or updated for each data item.

Disabling ECL logging doesn't affect importing data from connectors. Instead, most logging data doesn't get written to the ECL and history tables, which can result is significant performance improvement.

Disabled ECL logging isn't automatically turned on. In other words, by default, ECL logging is enabled. However, you can easily turn on Disabled ECL logging by using a PowerShell cmdlet.

- Disabling ECL logging doesn't turn off logging history data about work items like incident, change requests, and so on. They'll continue to work as-is.

- Any *explicit change made by the user* to the data imported by the connectors, such as a user or a computer, is still recorded in the ECL and history.

- *History of using the data* that is imported by the connector is also recorded despite disabling ECL logging. For example, if a computer that was imported by the SCCM connector is added to an incident or a user is assigned as the affected user, then those changes are still recorded in the system.

- Disabling ECL logging is currently limited to the SCCM and Active Directory connectors only.

- When Service Manager is installed, by default, ECL logging is *enabled*.

## Benefits of disabling ECL logging

When you disable ECL logging:

- The connector sync time is reduced significantly. During testing at Microsoft, a 65% increase in performance for the SCCM connector and a 55% increase in performance for the Active Directory connector was verified.

- The size of the ECL table and the history tables won't increase. During the Active Directory connector test, it brought in 2.2 million rows and in the SCCM connector test, it brought in 11.6 million rows in ECL and history table. With the feature enabled, no rows are added into these tables.

## Disadvantages of disabling ECL logging

Here are some disadvantages of this feature:

You can't create DCM incidents when you disable ECL logging.

Some Service Manager users have created user-defined workflows that monitor data being imported by connectors. If you've defined workflows that need to be triggered when the data is imported by connectors, then enabling this feature won't trigger those workflows. Because the workflows look into the ECL table for entries and this feature doesn't log entries in the ECL table, these workflows won't work. In this case, you shouldn't disable ECL logging.

Because entries aren't written to the ECL and history table, the history of the creation and/or the changes to data items imported by connectors in Service Manager aren't recorded. In other words, if you disable ECL logging you can't determine when a user or a computer object was imported into the Service Manager database and/or when changes to these objects are imported into the Service Manager database.

In some cases, changes to data like users and computers need be recorded in the database for auditing purposes. In this example, an alternative is to get the change history from the source. For example, would need to get the history of changes made to the user from Active Directory or get the history of changes made to the computer from Configuration Manager.

## Additional information about disabling ECL logging

With System Center 2016 - Service Manager, ECL logging is disabled by default for both the new installations and upgrades, regardless of whether your disabled ECL logging previously. Settings that you might have used previously are no longer used. You'll need to use the procedure below to disable ECL logging.

If you used a registry entry previously to disable ECL logging, the registry value remains on your management server. You can manually delete the `ConnectorLoggingDisabled` REG_DWORD under the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2010\Common\SDK Service` key.

## Disable ECL logging

Use the following procedure to disable ECL logging for connectors.

### Disable ECL logging for SCCM and Active Directory connectors

> [!TIP]
> You can read the *ECL logging disable for SCCM and AD connector* status with the `- Get-SCSMClassInstance (Get-SCSMClass -Name "System.GlobalSetting.ConnectorEclLogSettings")` cmdlet in the Service Manager shell. The value of `ConnectorEclLogDisabled` in your output when set to 0 means that all the ECL logs are enabled. The value of `ConnectorEclLogDisabled` in your output when set to 1 means that ECL logs are disabled for SCCM and AD connectors.

1. Open a Service Manager PowerShell command as an administrator on the primary Management Server.
2. Run the following command in the Service Manager shell:

    ```powershell
    Get-SCSMClassInstance (Get-SCSMClass -Name "System.GlobalSetting.ConnectorEclLogSettings") | %{$_.ConnectorEclLogDisabled = 1 ; $_}  | Update-SCSMClassinstance
    ```

### Re-enable ECL logging

- Replace the value `1` in the previous procedure with `0` and run the command.  

## Next steps

- Read [Configuration items](config-items.md) to learn about how they store information about services, computers, software, software updates, users, and other undefined imported objects in the Service Manager database.
