---
description: Provides guidance and procedures for using global assets in an Automation runbook.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
ms.date: 11/01/2024
title: Simplify runbook authoring with global assets
ms.subservice: service-management-automation
ms.custom: UpdateFrequency2, engagement-fy24
---

# Simplify Service Management Automation runbook authoring with global assets

Global Assets are available to all the runbooks in an Automation environment.  You create and configure them using either the Automation workspace in the management portal or with the appropriate cmdlets in Windows PowerShell. From a runbook, you can retrieve and set values for global assets with activities in the **RunbookConstructs** module. The Windows PowerShell cmdlets are available to use in runbooks in Service Management Automation, but the activities are recommended as they're more efficient because they don't have to work through the Automation web service.

## Get or set credentials

An Automation Credential is either a username and password that can be used with Windows PowerShell commands or a certificate that is uploaded to the server. The properties for a credential are stored securely in the Automation database and can be accessed in the runbook with either the **Get-AutomationPSCredential** or **Get-AutomationCertificate** activity.

### PowerShell for managing credentials

You can use the cmdlets in the following table to create and manage credentials with Windows PowerShell in Service Management Automation.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaCertificate](/previous-versions/system-center/powershell/system-center-2012-r2/dn502568(v=sc.20))|Retrieves an Automation certificate.|
|[Get-SmaCredential](/previous-versions/system-center/powershell/system-center-2012-r2/dn502576(v=sc.20))|Retrieves an Automation PowerShell credential.|
|[Remove-SmaCertificate](/previous-versions/system-center/powershell/system-center-2012-r2/dn502583(v=sc.20))|Removes an Automation certificate.|
|[Remove-SmaCredential](/previous-versions/system-center/powershell/system-center-2012-r2/dn502593(v=sc.20))|Removes an Automation PowerShell credential.|
|[Set-SmaCertificate](/previous-versions/system-center/powershell/system-center-2012-r2/dn502572(v=sc.20))|Creates a new certificate or sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.|
|[Set-SmaCredential](/previous-versions/system-center/powershell/system-center-2012-r2/dn502575(v=sc.20))|Creates a new Automation PowerShell credential or sets the properties for an existing credential.|

###  PowerShell for working with credentials

You can use the activities in the following table to access the credentials in a runbook.

|Activities|Description|
|--------------|---------------|
|Get-AutomationCertificate|Gets a certificate to use in a runbook.|
|Get-AutomationPSCredential|Gets a username/password to use in a runbook.|

> [!NOTE]
> You should avoid using variables in the "Name parameter of **Get-AutomationPSCredential** and **Get-AutomationCertificate** since this can complicate discovering dependencies between runbooks and Automation variables.

### Create a PowerShell credential in the Management Portal

1. Select the **Automation** workspace.

2. At the top of the window, select **Assets**.

3. At the bottom of the window, select **Add Setting**.

4. Select **Add Credential**.

5. In the **Credential Type** dropdown, select **PowerShell Credential**.

6. Enter a name for the credential in the **Name** box.

7. Select the right arrow.

8. Enter the values for each property.

9. Select the check mark to save the credential.

### Create a certificate in the

 Management Portal

1. Select the **Automation** workspace.

2. At the top of the window, select **Assets**.

3. At the bottom of the window, select **Add Setting**.

4. Select **Add Credential**.

5. In the **Credential Type** dropdown, select **Certificate**.

6. Enter a name for the certificate in the **Name** box.

7. Select the right arrow.

8. Select **Browse for File** and navigate to either a .cer or .pfx file.

9. If you selected a .pfx file, then provide its password.

10. Select the check mark to save the certificate.

### Create a credential with PowerShell

The following sample commands show how to create a new credential.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$credName = 'MyCredential'
$user = 'contoso\MyUser'
$pwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $user,$pwd

Set-SmaCredential -WebServiceEndpoint $webServer -port $port -Name $credName -Value $cred
```

### To create a new PowerShell certificate with Windows PowerShell in Service Management Automation

The following sample commands show how to create a new certificate by importing a certificate file.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$certName = 'MyCertificate'
$path = 'c:\certs\MyCertificate.pfx'
$certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force

Set-SmaCertificate -WebServiceEndpoint $webServer -port $port -Name $certName -Path $certPath -Password $certPwd
```

## Use a PowerShell credential in a runbook

You retrieve a PowerShell Credential in a runbook with the **Get-AutomationPSCredential** activity. This returns a PSCredential object that you can use in the workflow.

- The following sample commands show how to use a PowerShell credential in a runbook. In this example, the credential is used with an [InlineScript](overview-powershell-workflows.md#inlinescript) activity to run a set of commands using alternate credentials.

  ```powershell
  $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
  InlineScript {
     <Commands>
  } -PSComputerName $ServerName -PSCredential $myCredential
  ```

## Manage SMA connections

An Automation Connection contains the information required to connect to a service or application from a runbook. This information is defined in the module for the application and typically includes such information as the username and password and the computer to connect to. Other information may also be required such as a certificate or a subscription ID. The properties for a connection are stored securely in the Automation database and can be accessed in the runbook with the **Get-AutomationConnection** activity.

### Windows PowerShell Cmdlets

You can create and manage credentials with the Windows PowerShell cmdlets in the following table.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaConnection](/previous-versions/system-center/powershell/system-center-2012-r2/dn502599(v=sc.20))|Retrieves the values for each field in a particular connection.|
|[Get-SmaConnectionField](/previous-versions/system-center/powershell/system-center-2012-r2/dn502590(v=sc.20))|Retrieves the field definitions for a particular connection type.|
|[Get-SmaConnectionType](/previous-versions/system-center/powershell/system-center-2012-r2/dn502586(v=sc.20))|Retrieves the available connection types.|
|[New-SmaConnection](/previous-versions/system-center/powershell/system-center-2012-r2/dn502592(v=sc.20))|Creates a new connection.|
|[Remove-SmaConnection](/previous-versions/system-center/powershell/system-center-2012-r2/dn502581(v=sc.20))|Remove an existing connection.|
|[Set-SmaConnectionFieldValue](/previous-versions/system-center/powershell/system-center-2012-r2/dn502584(v=sc.20))|Sets the value of a particular field for an existing connection.|

### Runbook activities

You can access connections in a runbook with the activities in the following table.

|Activities|Description|
|--------------|---------------|
|Get-AutomationConnection|Gets a connection to use in a runbook.|

### Create a connection in the management portal

1. Select the **Automation** workspace.

2. At the top of the window, select **Assets**.

3. At the bottom of the window, select **Add Setting**.

4. Select **Add Connection**.

5. In the **Connection Type** dropdown, select a connection type.

6. Enter a name for the connection in the **Name** box.

7. Select the right arrow.

8. Enter a value for each property.

9. Select the check mark to save the connection.

### Create a connection with Windows PowerShell

The following sample commands create a new Virtual Machine Manager connection with the name MyVMMConnection.  

> [!NOTE]
> We use a hash table to define the properties of the connection. This is because different types of connections require different sets of properties. A connection of another type would use a different set of field values.

For more information about hash tables, see [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$connectionName = 'MyConnection'
$fieldValues = @{"Username"="MyUser";"Password"="password";"ComputerName"="MyComputer"}
New-SmaConnection -WebServiceEndpoint $webServer -port $port -Name $connectionName -ConnectionTypeName "VirtualMachineManager" -ConnectionFieldValues $fieldValues
```

### Use a connection in a runbook

Use the **Get-AutomationConnection** activity to use a connection in a runbook.  This activity retrieves the values of the different fields in the connection and returns them as a hash table, which can then be used with the appropriate commands in the runbook.

For more information about hash tables, see [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).

The following sample code shows how to use a connection to provide the computer name and credentials for an [InlineScript](overview-powershell-workflows.md#inlinescript) block that runs commands on another computer.

```powershell
$con = Get-AutomationConnection -Name 'MyConnection'
$securepassword = ConvertTo-SecureString -AsPlainText -String $con.Password -Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $con.Username, $securepassword
InlineScript {
   <Commands>
} -PSComputerName $con.ComputerName -PSCredential $cred
```

## Simplify runbook development with global variables

Automation variables are values that are available to all the runbooks.  You can create, modify, and retrieve them from the management portal, Windows PowerShell, or from within a runbook. Automation variables are useful for the following scenarios:

- Share a value between multiple runbooks.

- Share a value between multiple jobs from the same runbook.

- Manage a value from the management portal or from the Windows PowerShell command line that is used by runbooks.

Automation Variables are persisted so that they continue to be available even if the runbook fails. This also allows a value to be set by one runbook that is then used by another or is used by the same runbook the next time that it's run.

When a variable is created, you must specify its data type from the following list. This is so that the management portal can display the appropriate control for the variable value. You can only assign a value of the correct type to a variable.

- String

- Integer

- Boolean

- Datetime

When a variable is created, you can specify that it be stored encrypted. When a variable is encrypted, it's stored securely in the SMA database, and its value can't be retrieved from the **Get-SmaVariable** cmdlet. The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook. You can store multiple values of the defined type to a single variable by creating a hash table.

### Windows PowerShell Cmdlets

You can create and manage variables with the Windows PowerShell cmdlets in the following table.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaVariable](/previous-versions/system-center/powershell/system-center-2012-r2/dn502600(v=sc.20))|Retrieves the value of an existing variable.|
|[Set-SmaVariable](/previous-versions/system-center/powershell/system-center-2012-r2/dn502569(v=sc.20))|Creates a new variable or sets the value for an existing variable.|

### Runbook activities

You can access variables in a runbook with the activities in the following table.

|Activities|Description|
|--------------|---------------|
|Get-AutomationVariable|Retrieves the value of an existing variable.|
|Set-AutomationVariable|Sets the value for an existing variable.|

> [!NOTE]
> You should avoid using variables in the "Name parameter of Get-AutomationVariable since this can complicate discovering dependencies between runbooks and Automation variables.

### Create a new variable in the management portal

1. Select the **Automation** workspace.

2. At the top of the window, select **Assets**.

3. At the bottom of the window, select **Add Setting**.

4. Select **Add Variable**.

5. In the **Type** dropdown, select a data type.

6. Enter a name for the variable in the **Name** box.

7. Select the right arrow.

8. Enter a value for the variable and specify whether to encrypt it.

9. Select the check mark to save the new variable.

### To create a new variable with Windows PowerShell

The [Set-SmaVariable](/previous-versions/system-center/powershell/system-center-2012-r2/dn502569(v=sc.20)) cmdlet both creates a new variable and sets the value for an existing variable.  The following sample commands show how to create a variable of type string.

```powershell
$web = 'https://MySMAServer'
$port = 9090

Set-SMAVariable -WebServiceEndpoint $web -Port $port -Name 'MyVariable' -Value 'My String'
```

### Use a variable in a runbook

- The following sample code shows how to set and retrieve a variable in a runbook. In this sample, it's assumed that variables of type integer named NumberOfIterations and NumberOfRunnings and a variable of type string named SampleMessage have already been created.

    ```powershell
    $NumberOfIterations = Get-AutomationVariable -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AutomationVariable -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    Write-Output "Runbook has been run $NumberOfRunnings times."
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AutomationVariable -Name NumberOfRunnings -Value (NumberOfRunnings += 1)
    ```

## Next steps

- Read about [building an integration module](manage-integration-modules.md).
- Read about [authoring automation runbooks](authoring-automation-runbooks.md).
