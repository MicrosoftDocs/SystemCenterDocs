---
title: Set SNMP Variable
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe39d6e7-10e3-470f-aa06-b5307a13a871
---
# Set SNMP Variable
The Set SNMP Variable activity will modify a variable, specified by its MIB, on a network device. Use the Set SNMP Variable to update a variable that reports on the failure or success of a critical runbook.

## Configuring the Set SNMP Variable Activity
Before you configure the Set SNMP Variable activity you need to determine the following:

-   IP address of the device as well as the port number, SNMP MIB, and the SNMP version

-   Community string required to update the variable

> [!NOTE]
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.

Use the following information to configure the Set SNMP Variable activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**IP address**|Type the IP address of the device hosting the MIB variable.|
|**Port**|Type port used to communicate with the network device.|
|**Object identifier**|Type the MIB identifier of the variable whose value you want to change.|
|**Object value**|Type the new value of the variable you are changing. Make sure that the new value matches the constraints that are set out by device manufacturer. This field is case\-sensitive and supports only alphanumeric characters.|
|**SNMP version**|Select the SNMP version to use when connecting to the network device. You can select **SNMPv1** or **SNMPv2c**.|
|**Community string**|Type the community string that will be used to authenticate against the network device. The community should have rights of Read write or higher. This field is case\-sensitive and supports only alphanumeric characters.|

### Advanced Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Timeout**|Type the number of seconds the Set SNMP Variable will wait for a response from the network device. If the operation times out, then it will attempt to retry the action. The number of retries is specified in the **Retry** box.|
|**Retry**|Type the number of times to attempt to set the SNMP variable.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|MIB identifier|The MIB identifier of the variable that was set.|
|MIB value|The new value of the variable that was set.|
|Device IP address|The IP address of the device where the variable was set.|
|Timeout|The timeout period specified in the Set SNMP variable operator interface.|
|Retry attempts|The number of attempts made to set the SNMP variable.|
|SNMP Version|The SNMP version that was specified to set this variable. This value can be SNMPv1, or SNMPv2c.|
|Community string|The community string that was used to authenticate against this SNMP variable.|
|Request port|The port used to communicate to the SNMP device.|

