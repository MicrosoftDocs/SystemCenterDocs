---
title: Troubleshooting OM Agent installation on a Nano Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ad93e36-e6b9-44d5-bdc3-440b2ed44483
---
# Troubleshooting OM Agent installation on a Nano Server
If you encounter any difficulties with setting up the Operations Manager Agent on a Nano Server you can use the checklist below for possible solutions.

## Troubleshooting list
**Installation Issues**

||||
|-|-|-|
|Error Message|Possible Reason|Resolution|
|There was an error opening the firewall port|Insufficient permissions for setting the Remote Event Log Management firewall rule.|Make sure the account the script is running under has sufficient permissions to set the firewall rule.|
|Agent directory already present in Nano Server. Please uninstall the agent using the uninstallation script and then try again.|If you ran the installation script already and it did not complete, the Agent directory might have been created already.|Run the uninstallation script as suggested by the error message.|
|Setting up and importing the registry failed.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the installation script again.|
|Failed to install performance counters.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the installation script again.|

**Uninstallation Issues**

||||
|-|-|-|
|Error Message|Possible Reason|Resolution|
|HealthService was not found on the Nano Server. Assuming previous uninstall didn't complete.|If the installation did not complete the HealthService might not have been setup. Another process could also be using the HealthService.|Make sure the HealthService is not being used and run the Uninstallation script again.|
|Unable to delete HealthService on Nano Server.|The HealthService may be busy or another process is using the HealthService.|Make sure the HealthService is not in use and run the Uninstallation script again.|
|Unable to kill the MonitoringHost(s) on the Nano Server.|The SCOM Agent runs in the MonitoringHost process. If that process is active the Uninstallation script will not be able to terminate it.|Make sure the MonitoringHost process is not running, and run the Uninstallation script again.|
|Unable to uninstall the performance counters.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the Uninstallation script again.|
|Unable to remove registry changes done by the SCOM agent on Nano Server.|Insufficient permissions to edit the registry.|Make sure the account the script is running under has sufficient permissions to edit the registry and run the Uninstallation script again.|
|Unable to delete the agent directory.|Insufficient permissions to access the NanoAgent directory.|Make sure the account the script is running under has sufficient permissions to access the NanoAgent directory and run the Uninstallation script again.|
|Unable to locate agent folder on the Nano Server.|Either the NanoAgent directory has been moved, or the account has insufficient permissions to access the NanoAgent directory.|Make sure the account the script is running under has sufficient permissions to access the NanoAgent directory and that the NanoAgent directory is present and run the Uninstallation script again.|
|Unable to remove the agent directory. Try restarting the Nano Server and then re-running this script.|A process may be using the SCOM Agent.|Make sure there are no processes attached to the SCOM agent and run the Uninstallation script again.|


