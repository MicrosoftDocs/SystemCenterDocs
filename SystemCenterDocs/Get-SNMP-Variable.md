---
title: Get SNMP Variable
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bb233a2-aa1f-4739-8f43-fb5004ba4342
---
# Get SNMP Variable
The Get SNMP Variable activity will query a network device for the value of variable that is assigned to the Management Information Base address that you specify. You can use the Get SNMP Variable activity to retrieve information about a network device to determine if an administrator needs to be notified.

## Configuring the Get SNMP Variable Activity
Before you configure the Get SNMP Variable activity, you need to determine the following:

-   The IP address of the device, as well as the port number, SNMP MIB, and SNMP version

-   The community string required to retrieve the variable.

> [!NOTE]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.

Use the following information to configure the Get SNMP Variable activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**IP address**|Type the IP address of the device hosting the MIB variable.|
|**Port**|Type port used to communicate with the network device. The default port is 161.|
|**Object identifier**|Type the MIB identifier of the variable whose value you want to retrieve.|
|**SNMP Version**|Select the SNMP version to use when connecting to the network device.|
|**Community string**|Type the community string that will be used to authenticate against the network device. The community should have rights of Read only or higher. This field is case\-sensitive and supports only alphanumeric characters.|

### Advanced Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Timeout**|Type the number of seconds the Get SNMP Variable will wait for a response from the network device. If the operation times out, then it will attempt to retry the action. The number of retries is specified in the **Retry** box.|
|**Retry**|Type the number of times to attempt to retrieve the SNMP variable|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|MIB identifier|The MIB identifier of the variable that was retrieved.|
|MIB value|The value of the variable that was retrieved.|
|Device IP address|The IP address of the device where the variable was retrieved.|
|Timeout|The timeout period specified in the Get SNMP variable operator interface.|
|Retry attempts|The number of attempts made to retrieve the SNMP Variable.|
|SNMP Version|The SNMP version that was specified to retrieve this variable. This value can be **SNMPv1** or **SNMPv2c**.|
|Community string|The community string that was used to authenticate against this SNMP variable.|
|Request port|The port used to communicate to the SNMP device.|

