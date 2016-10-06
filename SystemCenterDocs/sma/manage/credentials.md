---
description:  
manager:  cfreeman
ms.topic:  article
author:  bwren
ms.author: bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  10/12/2016
title:  Credentials
ms.technology:  service-management-automation
ms.assetid:  978a72d8-a446-42e5-b2bb-53a838623ee0
---

# Credentials

>Applies To: Windows Azure Pack for Windows Server, System Center 2016 - Service Management Automation

An Automation Credential is either a username and password that can be used with Windows PowerShell commands or a certificate that is uploaded to the server.  The properties for a credential are stored securely in the Automation database and can be accessed in the runbook with either the **Get-AutomationPSCredential** or **Get-AutomationCertificate** activity.

## Windows PowerShell Cmdlets
The cmdlets in the following table are used to create and manage credentials with Windows PowerShell in Service Management Automation.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaCertificate](http://go.microsoft.com/fwlink/?LinkID=306447)|Retrieves an Automation certificate.|
|[Get-SmaCredential](http://go.microsoft.com/fwlink/?LinkID=306451)|Retrieves an Automation PowerShell credential.|
|[Remove-SmaCertificate](http://go.microsoft.com/fwlink/?LinkID=306464)|Removes an Automation certificate.|
|[Remove-SmaCredential](http://go.microsoft.com/fwlink/?LinkID=306466)|Removes an Automation PowerShell credental.|
|[Set-SmaCertificate](http://go.microsoft.com/fwlink/?LinkID=306473)|Creates a new certificate or sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.|
|[Set-SmaCredential](http://go.microsoft.com/fwlink/?LinkID=306475)|Creates a new Automation PowerShell credential or sets the properties for an existing credential.|

## Runbook Activities
The activities in the following table are used to access credentials in a runbook.

|Activities|Description|
|--------------|---------------|
|Get-AutomationCertificate|Gets a certificate to use in a runbook.|
|Get-AutomationPSCredential|Gets a username/password to use in a runbook.|

> [!NOTE]
> You should avoid using variables in the "Name parameter of **Get-AutomationPSCredential** and **Get-AutomationCertificate** since this can complicate discovering dependencies between runbooks and Automation variables.

## Creating a new credential

### To create a new PowerShell credential with the Management Portal

1.  Select the **Automation** workspace.

2.  At the top of the window, click **Assets**.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Credential**.

5.  In the **Credential Type** dropdown, select **PowerShell Credential**.

6.  Type a name for the credential in the **Name** box.

7.  Click the right arrow.

8.  Type in values for each property.

9. Click the check mark to save the credential.

### To create a new certificate with the Management Portal

1.  Select the **Automation** workspace.

2.  At the top of the window, click **Assets**.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Credential**.

5.  In the **Credential Type** dropdown, select **Certificate**.

6.  Type a name for the certificate in the **Name** box.

7.  Click the right arrow.

8.  Click **Browse for File** and navigate to either a .cer or .pfx file.

9. If you selected a .pfx file, then provide its password.

10. Click the check mark to save the certificate.

### To create a new PowerShell credential with Windows PowerShell in Service Management Automation
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

Set-SmaCertificate -WebServiceEndpoint $webServer -port $port -Name $certName "Path $certPath "Password $certPwd
```

## Using a PowerShell Credential in a Runbook
You retrieve a PowerShell Credential in a runbook with the **Get-AutomationPSCredential** activity. This returns a PSCredential object that you can use in the workflow.

#### To use a PowerShell credential in a runbook

-   The following sample commands show how to use a PowerShell credential in a runbook. In this example, the credential is used with an [InlineScript](Windows-PowerShell-Workflow-Concepts.md#bkmk_InlineScript) activity to run a set of commands using alternate credentials.

    ```powershell
    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    InlineScript {
       <Commands>
    } -PSComputerName $ServerName -PSCredential $myCredential
    ```

## See Also
[Service Management Automation](../Service-Management-Automation.md)

[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)

[Global Assets](Global-Assets.md)
