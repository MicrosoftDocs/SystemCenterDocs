---
title: Optionally Disable ECL Logging for Faster Connector Synchronization
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 805b479a-9312-4039-be44-01dda07086d8
---
# Optionally Disable ECL Logging for Faster Connector Synchronization
The Active Directory and SCCM connectors in Service Manager can import large amounts of data into the Service Manager database. In doing so, they not only increase the size of the data table, which is where the data from the connectors are stored, but they also increase the size of the EntityChangeLog \(ECL\) table and history tables considerably. A large ECL table size can be a problem—in some cases, it can slow down the system significantly.

The ECL table, and the history tables in this case, store details about when the data was brought into Service Manager and the properties that were added or updated for each data item.

Disabling ELC logging, doesn’t affect importing data from connectors. Instead, most logging data doesn’t get written to the ECL and history tables, which can result is significant performance improvement.
 
Disabled ECL logging is not automatically turned on. In other words, by default, ECL logging is enabled. However, you can easily turn on Disabled ECL logging by using a PowerShell cmdlet.

-   Disabling ECL logging doesn’t turn off logging history data about work items like incident, change requests etc. They will continue to work as\-is.

-   Any *explicit change made by the user* to the data imported by the connectors, such as a user or a computer, is still recorded in the ECL and history.

-   *History of using the data* that is imported by the connector is also recorded despite disabling ECL logging. For example, if a computer that was imported by the SCCM connector is added to an incident or a user is assigned as the affected user, then those changes are still recorded in the system.

-   Disabling ECL logging is currently limited to the SCCM and Active Directory connectors only.

-   When Service Manager is installed, by default, ECL logging is *enabled*.

## Benefits of Disabling ECL Logging
When you disable ECL logging:

-   The connector sync time is reduced significantly. During testing at Microsoft, a 65% increase in performance for the SCCM connector and a 55% increase in performance for the Active Directory connector was verified.

-   The size of the ECL table and the history tables will not increase. During the Active Directory connector test, it brought in 2.2 million rows and in the SCCM connector test, it brought in 11.6 million rows in ECL and history table. With the feature enabled, no rows are added into these tables.

## Disadvantages of Disabling ECL Logging
Here are some disadvantages of this feature:

You cannot create DCM incidents when you disable ECL logging.

Some Service Manager users have created user\-defined workflows that monitor data being imported by connectors. If you have defined workflows that need to be triggered when the data is imported by connectors, then enabling this feature will not trigger those workflows. Because the workflows look into the ECL table for entries and this feature doesn’t log entries in the ECL table, these workflows will not work. In this case, you should not disable ECL logging.

Because entries are not written to the ECL and history table, the history of the creation and\/or the changes to data items imported by connectors in Service Manager are not recorded. In other words, if you disable ECL logging you cannot determine when a user or a computer object was imported into the Service Manager database and\/or when changes to these objects are imported into the Service Manager database.

In some cases, changes to data like users and computers need be recorded in the database for auditing purposes. In this example, an alternative is to get the change history from the source. For example, would need to get the history of changes made to the user from Active Directory or get the history of changes made to the computer from System Center Configuration Manager.

## Additional Information About Disabling ECL Logging
With Service Manager 2016 Technical Preview 5, ECL logging is disabled by default for both a new installation and an upgrade, regardless of whether your disabled ECL logging in Technical Preview 4. Settings that you might have use for Technical Preview 4 with a registry entry are no longer used. You'll need the use the procedure below to disable ECL logging. 

If you used a registry entry for Technical Preview 4 to disable ECL logging, the registry value remains on your management server. You can manually delete the `ConnectorLoggingDisabled` REG_DWORD under the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2010\Common\SDK Service` key. 
 

## Disabling ECL Logging
Use the following procedure to disable ECL logging for connectors.

### To disable ECL logging for SCCM and Active Directory connectors

>[!TIP] You can read the *ECL logging disable for SCCM and AD connector* status with the `- Get-SCSMClassInstance (Get-SCSMClass -Name "System.GlobalSetting.ConnectorEclLogSettings")` cmdlet in the Service Manager shell. The value of `ConnectorEclLogDisabled` in your output when set to 0 means that all the ECL logs are enabled. The value of `ConnectorEclLogDisabled` in your output when set to 1 means that ECL logs are disabled for SCCM and AD connectors.
  

1. Open a Service Manager PowerShell command as an administrator on the primary Management Server.
2. Run the following command in the Service Manager shell:

    ```
    Get-SCSMClassInstance (Get-SCSMClass -Name "System.GlobalSetting.ConnectorEclLogSettings") | %{$_.ConnectorEclLogDisabled = 1 ; $_}  | Update-SCSMClassinstance
    ```
### To re-enable ECL logging
- Replace the value `1` in the previous procedure with `0` and run the command.  

