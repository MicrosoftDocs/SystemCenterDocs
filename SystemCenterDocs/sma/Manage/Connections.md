---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Connections
ms.technology:  service-management-automation
ms.assetid:  d82d70df-2de2-4d1f-9e9d-a033af8e6b05
---

# Connections

>Applies To: Windows Azure Pack for Windows Server, System Center 2012 R2 Orchestrator

An Automation Connection contains the information required to connect to a service or application from a runbook.  This information is defined in the module for the application and typically includes such information as the username and password and the computer to connect to.  Other information may also be required such as a certificate or a subscription Id.  The properties for a connection are stored securely in the Automation database and can be accessed in the runbook with the **Get-AutomationConnection** activity.

## Windows PowerShell Cmdlets
The cmdlets in the following table are used to create and manage credentials with Windows PowerShell in Service Management Automation.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaConnection](http://go.microsoft.com/fwlink/?LinkID=306448)|Retrieves the values for each field in a particular connection.|
|[Get-SmaConnectionField](http://go.microsoft.com/fwlink/?LinkID=306449)|Retrieves the field definitions for a particular connection type.|
|[Get-SmaConnectionType](http://go.microsoft.com/fwlink/?LinkID=306450)|Retrieves the available connection types.|
|[New-SmaConnection](http://go.microsoft.com/fwlink/?LinkID=306461)|Creates a new connection.|
|[Remove-SmaConnection](http://go.microsoft.com/fwlink/?LinkID=306465)|Remove an existing connection.|
|[Set-SmaConnectionFieldValue](http://go.microsoft.com/fwlink/?LinkID=306474)|Sets the value of a particular field for an existing connection.|

## Runbook Activities
The activities in the following table are used to access connections in a runbook.

|Activities|Description|
|--------------|---------------|
|Get-AutomationConnection|Gets a connection to use in a runbook.|

## Creating a New Connection

### To create a new connection with the management portal

1.  Select the **Automation** workspace.

2.  At the top of the window, click **Assets**.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Connection**.

5.  In the **Connection Type** dropdown, select a connection type.

6.  Type a name for the connection in the **Name** box.

7.  Click the right arrow.

8.  Type in a value for each property.

9. Click the check mark to save the connection.

### To create a new connection with Windows PowerShell in Service Management Automation
The following sample commands create a new Virtual Machine Manager connection with the name MyVMMConnection.  Note that we use a hashtable to define the properties of the connection. This is because different types of connections require different sets of properties. A connection of another type would use a different set of field values.

For more information about hash tables, see [about_Hash_Tables](http://go.microsoft.com/fwlink/?LinkID=324844).

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$connectionName = 'MyConnection'
$fieldValues = @{"Username"="MyUser";"Password"="password";"ComputerName"="MyComputer"} 
New-SmaConnection "WebServiceEndpoint $webServer "port $port "Name $connectionName "ConnectionTypeName "VirtualMachineManager" "ConnectionFieldValues $fieldValues
```

## Using a connection in a runbook
Use the **Get-AutomationConnection** activity to use a connection in a runbook.  This activity retrieves the values of the different fields in the connection and returns them as a hashtable which can then be used with the appropriate commands in the runbook.

For more information about hash tables, see [about_Hash_Tables](http://go.microsoft.com/fwlink/?LinkID=324844).

The following sample code shows how to use a connection to provide the computer name and credentials for an [InlineScript](Windows-PowerShell-Workflow-Concepts.md#bkmk_InlineScript) block that runs commands on another computer.

```powershell
$con = Get-AutomationConnection -Name 'MyConnection'
$securepassword = ConvertTo-SecureString -AsPlainText -String $con.Password -Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $con.Username, $securepassword
InlineScript {
   <Commands>
} -PSComputerName $con.ComputerName -PSCredential $cred
```

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Global Assets](Global-Assets.md)



