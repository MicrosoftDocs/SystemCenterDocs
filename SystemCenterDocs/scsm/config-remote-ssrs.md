---
title: Manual steps to configure SQL Server Reporting Services
description: When you deploy the Service Manager data warehouse management server, you can choose the server where Microsoft SQL Server Reporting Services is deployed.
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 8f0b7917-ba9f-49de-93bb-17d26fb2bf11
---

# Manual steps to configure SQL Server Reporting Services



During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you're prompted to follow this procedure to prepare the server. Preparing the remote computer to host SSRS involves the following steps, which are covered in detail in this section:

- Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

- Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

- Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you didn't use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS13.\<INSTANCE\_NAME\>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

## Copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file

Use the following steps:

1. On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2. For SQL Server 2016, locate the folder \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3. Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4. In the Prerequisites folder, select **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located in either step 2.

## Add a code segment to the rssrvpolicy.config file

Use the following steps:

1. On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer folder for SQL server 2016.

2. Using an XML editor of your choice (such as Notepad), open the rssrvpolicy.config file.

3. Scroll through the rssrvpolicy.config file and locate the `<CodeGroup>` code segments. The following code shows an example of a `<CodeGroup>` segment.

    ```xml
    <CodeGroup
       class="UnionCodeGroup"
       version="1"
       PermissionSetName="FullTrust">
       <IMembershipCondition
          class="UrlMembershipCondition"
          version="1"
          Url="$CodeGen$/*"
       />
    </CodeGroup>
    ```

4. Add the following `<CodeGroup>` segment in its entirety in the same section as the other `<CodeGroup>` segments.

    ```xml
    <CodeGroup
       class="UnionCodeGroup"
       version="1"
       PermissionSetName="FullTrust"
       Name="Microsoft System Center Service Manager Reporting Code Assembly"
       Description="Grants the SCSM Reporting Code assembly full trust permission.">
       <IMembershipCondition
          class="StrongNameMembershipCondition"
          version="1"
          PublicKeyBlob="0024000004800000940000000602000000240000525341310004000001000100B5FC90E7027F67871E773A8FDE8938C81DD402BA65B9201D60593E96C492651E889CC13F1415EBB53FAC1131AE0BD333C5EE6021672D9718EA31A8AEBD0DA0072F25D87DBA6FC90FFD598ED4DA35E44C398C454307E8E33B8426143DAEC9F596836F97C8F74750E5975C64E2189F45DEF46B2A2B1247ADC3652BF5C308055DA9"
    />
    </CodeGroup>
    ```

5. Save the changes and close the XML editor.

## Add an Extension tag to the Data segment in the rsreportserver.conf file

Use the following steps:

1. On the computer hosting SSRS, locate the file rsreportserver.config in the \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer folder for SQL server 2016.

2. Using an XML editor of your choice (such as Notepad), open the rsreportserver.config file.

3. Scroll through the rsreportserver.config file and locate the `<Data>` code segment. There's only one `<Data>` code segment in this file.

4. Add the following `Extension` tag to the `<Data>` code segment where all the other `Extension` tags are:

    ```xml
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />
    ```

5. Save the changes and close the XML editor.

## Verify SSRS installation

::: moniker range="sc-sm-2016"
In the Service Manager Data Warehouse (DW) version 2016 and later the following known issue is observed:
::: moniker-end

::: moniker range=">sc-sm-2016"
In the Service Manager Data Warehouse (DW), the following known issue is observed:
::: moniker-end

If SQL Server Reporting Services (SSRS) is running locally on the Data Warehouse Management Server, and SSRS is 2017 or later, the Data Warehouse Setup completes successfully, but might not configure the specified local SSRS instance properly.

Use the below script to verify if the **LOCAL** SSRS installation is configured correctly and can be used with the Service Manager Data Warehouse.

>[!NOTE]
>This PowerShell script can be executed after a Service Manager Data Warehouse installation. The script won't make any changes to the configuration but verifies it. You can run the script as many times as required.

```PowerShell
#region function definitions

function SelfElevate() {
    #got from http://www.expta.com/2017/03/how-to-self-elevate-powershell-script.html   and changed a bit
    if (-Not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] 'Administrator')) {
     if ([int](Get-WmiObject -Class Win32_OperatingSystem | Select-Object -ExpandProperty BuildNumber) -ge 6000) {
      $CommandLine = "-File `"" + $Script:MyInvocation.MyCommand.Path + "`" " + $Script:MyInvocation.UnboundArguments
      Start-Process -FilePath PowerShell.exe -Verb Runas -ArgumentList $CommandLine
      Exit
     }
    }
}
function EndScriptExecution() {
    Write-Host ""
    Read-Host "Press ENTER to stop execution" 
    Exit
}
#endregion
#region Init
SelfElevate
#endregion 

#region Select SSRS service
$ssrsServicesAvailable = gwmi win32_service | ?{ $_.DisplayName -like 'SQL Server Reporting Services*' }
if ($ssrsServicesAvailable -eq $null) {
    Write-Host "No SSRS service(s) detected on this machine. " -NoNewline
    Write-Host "Aborting ..." -ForegroundColor Yellow
    EndScriptExecution
}

if ( ($ssrsServicesAvailable | Measure-Object).Count -eq 1) {
    $ssrsServiceToVerify = ($ssrsServicesAvailable | Select-Object -Property DisplayName, State, PathName) | Select-Object -First 1
}
else {
    $ssrsServiceToVerify = $ssrsServicesAvailable | Select-Object -Property DisplayName, State, PathName | Out-GridView  -Title 'Select the SSRS service to verify and then click OK...' -OutputMode Single
    if ($ssrsServiceToVerify -eq $null) {
        Write-Host "No SSRS service selected to verify. " -NoNewline
        Write-Host "Aborting ..." -ForegroundColor Yellow
        EndScriptExecution
    }
}
#endregion

#region Preparation
Write-Host "--------------------------------------------------------------------"
Write-Host "Verifiying selected SSRS service : " -NoNewline
Write-Host "'$($ssrsServiceToVerify.DisplayName)'"  -ForegroundColor Cyan
Write-Host "--------------------------------------------------------------------"
Write-Host ""

$ssrsExePath = $ssrsServiceToVerify.PathName.Replace('"','')
$ssrsExeFileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo($ssrsExePath)
$ssrsMajorVersion = $ssrsExeFileVersion.ProductMajorPart
$ssrsVersionDisplayName = switch ($ssrsMajorVersion)
{
    11 {"2012"}
    12 {"2014"}
    13 {"2016"}
    14 {"2017"}
    15 {"2019"}
    default {""}
}
if ($ssrsVersionDisplayName -eq "") {
    Write-Host "Unknown SSRS Version detected. " -NoNewline
    Write-Host "Aborting ..." -ForegroundColor Yellow
    EndScriptExecution
}

[System.IO.DirectoryInfo]$ssrsReportServerFolder = (Get-Item -Path $ssrsExePath).Directory.Parent
if ($ssrsMajorVersion -ge 14) {
    $ssrsReportServerFolder =    Join-Path $ssrsReportServerFolder.FullName "ReportServer"
}
[string]$ssrsReportServerFolder = $ssrsReportServerFolder.FullName 
[string]$ssrsReportServerBinFolder = Join-Path $ssrsReportServerFolder "bin"
#endregion

#region Checking DLL
$scsmDllFileExists = $false
$scsmDllFileName = "Microsoft.EnterpriseManagement.Reporting.Code.dll"
$scsmDllFilePath = Join-Path $ssrsReportServerBinFolder $scsmDllFileName
$scsmDllFileExists = (Test-Path -Path $scsmDllFilePath)
if (-not $scsmDllFileExists) {
    Write-Host "ERROR: "  -ForegroundColor Yellow -NoNewline
    Write-Host "The file '$scsmDllFileName' does *NOT* exist in '$ssrsReportServerBinFolder'"
}
else {
    Write-Host " Pass: The file '$scsmDllFileName' does exist in '$ssrsReportServerBinFolder'" 
}
Write-Host ""
#endregion

#region Checking rssrvpolicy.config
$rssrvpolicy_configIsCorrect = $false
$rssrvpolicy_configFileName = "rssrvpolicy.config"
$rssrvpolicy_configFilePath = Join-Path $ssrsReportServerFolder $rssrvpolicy_configFileName
$rssrvpolicy_configFileExists = (Test-Path -Path $rssrvpolicy_configFilePath)
if (-not $rssrvpolicy_configFileExists) {
    Write-Host "$rssrvpolicy_configFileName does *NOT* exist in $ssrsReportServerFolder" -ForegroundColor Yellow
}
if ($rssrvpolicy_configFileExists) {    
    
    [xml]$xml = Get-Content $rssrvpolicy_configFilePath
    
    $tagNameToFind = "CodeGroup"
    $attributeNameToFind = "Name"
    $attributeValueToFind = "Microsoft System Center Service Manager Reporting Code Assembly"
    $nodeToFind = Select-Xml -XPath "//$tagNameToFind[@$attributeNameToFind='$attributeValueToFind']" -Xml $xml

    if ($nodeToFind -eq $null) {
        Write-Host "ERROR: "  -ForegroundColor Yellow -NoNewline
        Write-Host "The file '$rssrvpolicy_configFileName' in '$ssrsReportServerFolder' does *NOT* contain the correct <$tagNameToFind> node." 
    }
    else {

        $CodeGroup_NodeToVerify = [System.Xml.XmlNode]$nodeToFind.Node
        $IMembershipCondition_NodeToVerify = [System.Xml.XmlNode]$CodeGroup_NodeToVerify.IMembershipCondition

        $rssrvpolicy_configIsCorrect =  ( $CodeGroup_NodeToVerify.class -eq "UnionCodeGroup" `
            -and $CodeGroup_NodeToVerify.version -eq "1" `
            -and $CodeGroup_NodeToVerify.PermissionSetName -eq "FullTrust" `
            -and $IMembershipCondition_NodeToVerify.class -eq "StrongNameMembershipCondition" `
            -and $IMembershipCondition_NodeToVerify.version -eq "1" `
            -and $IMembershipCondition_NodeToVerify.PublicKeyBlob -eq "0024000004800000940000000602000000240000525341310004000001000100B5FC90E7027F67871E773A8FDE8938C81DD402BA65B9201D60593E96C492651E889CC13F1415EBB53FAC1131AE0BD333C5EE6021672D9718EA31A8AEBD0DA0072F25D87DBA6FC90FFD598ED4DA35E44C398C454307E8E33B8426143DAEC9F596836F97C8F74750E5975C64E2189F45DEF46B2A2B1247ADC3652BF5C308055DA9"
        ) 

        if (-not $rssrvpolicy_configIsCorrect) {
            Write-Host "ERROR: "  -ForegroundColor Yellow -NoNewline
            Write-Host "The <$tagNameToFind> node in '$rssrvpolicy_configFileName' in '$ssrsReportServerFolder' does exists but its content is *NOT* correct."
        }
        else {
            Write-Host " Pass: The content of '$rssrvpolicy_configFileName'    in '$ssrsReportServerFolder' is correct."             
        }
    }

}
Write-Host ""
#endregion

#region Checking rsreportserver.config
$rsreportserver_configIsCorrect = $false
$rsreportserver_configFileName = "rsreportserver.config"
$rsreportserver_configFilePath = Join-Path $ssrsReportServerFolder $rsreportserver_configFileName
$rsreportserver_configFileExists = (Test-Path -Path $rsreportserver_configFilePath)
if (-not $rsreportserver_configFileExists) {
    Write-Host "$rsreportserver_configFileName does *NOT* exist in $ssrsReportServerFolder" -ForegroundColor Yellow
}
if ($rsreportserver_configFileExists) {
     
    [xml]$xml = Get-Content $rsreportserver_configFilePath
    
    $tagNameToFind = "Extension"
    $attributeNameToFind = "Name"
    $attributeValueToFind = "SCDWMultiMartDataProcessor"
    $nodeToFind = Select-Xml -XPath "//$tagNameToFind[@$attributeNameToFind='$attributeValueToFind']" -Xml $xml

    if ($nodeToFind -eq $null) {
        Write-Host "ERROR: "  -ForegroundColor Yellow -NoNewline
        Write-Host "The file '$rsreportserver_configFileName' in '$ssrsReportServerFolder' does *NOT* contain the correct <$tagNameToFind> node."
    }
    else {

        $Extension_NodeToVerify = [System.Xml.XmlNode]$nodeToFind.Node
        $rsreportserver_configIsCorrect =  ( $Extension_NodeToVerify.Type.Replace(" ","") -eq "Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code".Replace(" ","") ) 

        if (-not $rsreportserver_configIsCorrect) {
            Write-Host "ERROR: "  -ForegroundColor Yellow -NoNewline
            Write-Host "The <$tagNameToFind> node in '$rsreportserver_configFileName' in '$ssrsReportServerFolder' does exists but its content is *NOT* correct." 
        }
        else {
            Write-Host " Pass: The content of '$rsreportserver_configFileName' in '$ssrsReportServerFolder' is correct."             
        }
    }

}
Write-Host ""
#endregion

#region Conclusion
""
Write-Host "Conclusion:" -ForegroundColor Cyan
Write-Host "==========="
if ($scsmDllFileExists -and $rsreportserver_configIsCorrect -and $rssrvpolicy_configIsCorrect) {
    Write-Host "The selected SSRS instance is configured correctly."
}
else {
    Write-Host "The selected SSRS instance is " -NoNewline
    Write-Host "*NOT* configured correctly." -ForegroundColor Yellow
    Write-Host "Please follow the steps at  " -NoNewline
    Write-Host "https://learn.microsoft.com/system-center/scsm/config-remote-ssrs" -ForegroundColor Yellow
}
EndScriptExecution
#endregion
```

## Next steps

- To use AlwaysOn availability groups with Service Manager to support a failover environment, review [Use SQL Server AlwaysOn availability groups to support failover](sql-always-on.md).
