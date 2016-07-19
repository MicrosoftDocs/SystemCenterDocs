---
title: Use Sysprep to Deploy Orchestrator
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a59d9a-6c39-4e47-a9e6-58ed51e7e815
author:bwren
manager:cfreemanwa
---
# Use Sysprep to Deploy Orchestrator
You can deploy Orchestrator using Sysprep. This enables you to deploy any component in Orchestrator in a distributed environment in an automatic process.  
  
For Orchestrator components you can create a Sysprep image by performing the following steps:  
  
1.  Prepare the Windows 2008 R2 image  
  
2.  Create the Orchestrator answer file for sysprep  
  
3.  Install Orchestrator using sysprep.  
  
## <a name="SCO_sysprep1"></a>Prepare the Windows 2008 R2 image  
Use the following steps to prepare the Windows 2008 R2 image.  
  
#### To prepare the Windows 2008 R2 image  
  
1.  Install Windows Server 2008 R2.  
  
2.  Install .NET Framework 4 from [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=246814](http://go.microsoft.com/fwlink/?LinkId=246814). \(This is only required for the web feature components of Orchestrator.\)  
  
## <a name="SCO_sysprep2"></a>Create the Orchestrator answer file for sysprep  
Before you can use the Sysprep tool to install Orchestrator on Windows Server 2008 R2, install Orchestrator as part of the Sysprep process using an answer file.  
  
See [Sample Orchestrator.xml file](../../orch/deploy/Use-Sysprep-to-Deploy-Orchestrator.md#SCO_sysprep4) for sample unattend.xml file. You can customize this sample file and import it into the Windows System Image Manager.  
  
#### To create the answer file  
  
1.  Create the Orchestrator.xml unattend file using the sample provided.  
  
2.  Copy the file to %systemdrive%\\windows\\system32\\sysprep.  
  
3.  Create the Orchestrator batch file that will install the Orchestrator components on this computer. An example of this file is available in [Sample Orchestrator.xml file](../../orch/deploy/Use-Sysprep-to-Deploy-Orchestrator.md#SCO_sysprep4). This is referred to in the Orchestrator.xml file. See [Install with the Orchestrator Command Line Install Tool](../../orch/deploy/Install-with-the-Orchestrator-Command-Line-Install-Tool.md) for the available command line options that can be used to install Orchestrator.  
  
4.  Run the following command:  
  
    ```  
    sysprep /generalize /oobe /shutdown /unattend:%systemdrive%\windows\system32\sysprep\Orchestrator.xml  
    ```  
  
## <a name="SCO_sysprep3"></a>Install Orchestrator using sysprep  
You now have a Windows 2008 R2 Sysprep image that you can use to automatically deploy Orchestrator in the environment.  
  
For information on creating a SQL Sysprep image for use with Orchestrator, refer to [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=246815](http://go.microsoft.com/fwlink/?LinkId=246815).  
  
## <a name="SCO_sysprep4"></a>Sample Orchestrator.xml file  
This is a sample Orchestrator.xml to be used for deploying Orchestrator with sysprep. Customize this using the Windows System Image Manager \(available in the Windows Automated Installation Kit, at [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=246813](http://go.microsoft.com/fwlink/?LinkId=246813)\).  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<unattend xmlns="urn:schemas-microsoft-com:unattend">  
    <settings pass="oobeSystem">  
        <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="http://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <AutoLogon>  
                <Password>  
                    <Value>password</Value>  
                    <PlainText>true</PlainText>  
                </Password>  
                <LogonCount>1</LogonCount>  
                <Enabled>true</Enabled>  
                <Username>Administrator</Username>  
            </AutoLogon>  
            <FirstLogonCommands>  
                <SynchronousCommand wcm:action="add">  
                    <CommandLine>cmd /c %systemdrive%\sco\install.bat</CommandLine>  
                    <Order>1</Order>  
                    <RequiresUserInput>false</RequiresUserInput>  
                </SynchronousCommand>  
            </FirstLogonCommands>  
        </component>  
    </settings>  
    <cpi:offlineImage cpi:source="wim:c:/windowsenterprise/extracted/sources/install.wim#Windows Server 2008 R2 SERVERENTERPRISE" xmlns:cpi="urn:schemas-microsoft-com:cpi" />  
</unattend>  
  
```  
  
This is a sample install.bat file that is referenced in the Orchestrator.xml unattend file for the FirstLogonCommand. Create this batch file in the %systemdrive%\\sco directory along with the Orchestrator setup files. This file can be customized by using the command line install tool. For more information, see [Install with the Orchestrator Command Line Install Tool](../../orch/deploy/Install-with-the-Orchestrator-Command-Line-Install-Tool.md).  
  
```  
%systemdrive%\sco\setup\setup.exe /Silent /ServiceUserName:%computername%\administrator /ServicePassword:password /Components:All /DbServer:%computername%  /DbPort:1433 /DbNameNew:OrchestratorSysPrep /WebConsolePort:82 /WebServicePort:81 /OrchestratorRemote /UseMicrosoftUpdate:1 /SendCEIPReports:1 /EnableErrorReporting:always  
  
```  
  
