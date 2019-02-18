---
description: include file to detail the release notes for Service Manager 2019
manager:  vvithal
ms.topic: include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center
ms.technology: service-manager
keywords:
ms.date: 01/30/2019
title: include file
ms.assetid: df2f12b4-ccbe-459e-815c-c70ad97fd0e1
---

## Release Notes for System Center 2019 - Service Manager
The following sections detail the release notes for Service Manager 2019 and include the known issues and workarounds.


## Known issues and workarounds

### Manual steps to activate Data Warehouse Server

**Description**: Service Manager Data Warehouse is not activated as part of the Management Server license activation. You must manually update the Data Warehouse.

**Workaround**:
You must manually update the Data Warehouse. Follow these steps:  
1. Open Windows Powershell.
2. Change directory to Installation folder/Powershell.
3. Run the following command to import PowerShell module;
   `– Import-Module .\System.Center.Service.Manager.psm1`
4. Run `Set-SCSMLicense powershell` cmdlet to activate the license.

### SCSM doesn’t work with default SSAS mode on SQL 2017
**Description:**
System Center Service Manager 2019 requires SQL Server Analysis Services (SSAS) to work with Microsoft Online Analytical Processing (OLAP) cubes. With SQL 2017 the default SSAS mode is **Tabular**. Service Manager’s Management Server and Data Warehouse only work with SSAS mode **Multi-Dimensional** and not **Tabular**.

**Workaround:**
In case of fresh installation of SQL Server 2017, select the SSAS mode as **Multi-Dimensional**. In case of an upgrade from an earlier version of SQL Server to SQL Server 2017, the older SSAS mode persists. Hence, no manual step is required for SQL Server upgrade scenario.

### Installation of SM 2019 on TLS 1.2 machine fails
**Description**: Fresh Installation of System Center Service Manager 2019 or an upgrade from a previous version to SM 2019 fails if the computer is TLS 1.2 hardened.

**Workaround**: Disable TLS 1.2 before the installation/upgrade and re-enable it after the upgrade is complete.

### Prerequisite for installing SM Authoring Tool
**Description**: Install Microsoft Visual C++ 2012 redistributable before you deploy Service Manager Authoring Tool 2019.

**Workaround**: None.

### Create Exchange Connector wizard might crash
**Description**: When you create a new Exchange Connector using Service Manager 2019 console, it gives an exception if the admin selects the **Test Connection** in the **Server Connection** pane of **Create Exchange Connector** wizard.

**Workaround**: Do not select **Test Connection** in the **Create Exchange Connector** wizard. Instead, click the **Next** button, which internally tests the connection and does not crash the wizard. If the crash has occurred, restart the wizard and use this workaround.

### Domain selection through Browse options fails in AD connector wizard
**Description**: An error occurs when you select **Browse** to choose the domain or OU in Active Directory connector wizard of Service Manager 2019 console.

**Workaround**: Install Microsoft Visual C++ 2012 Redistributable on the computer and use the AD connector wizard.

### Error while creating a new software type configuration item
**Description**: The property **Is Virtual Application** field in **Create Software configuration item** form is mandatory, but it does not carry the asterix (\*) that indicates a mandatory item.

When you do not fill this field and click **Ok** or **Apply**, an error appears and you cannot use the form.

**Workaround**: Reopen the create Software configuration item form, and fill all the details including the field **Is Virtual Application**, and then click **OK** or **Apply**.

### Manual steps to configure remote SQL Server reporting services
**Description**: During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During this setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you are prompted to follow a procedure in the Deployment Guide to prepare the server. You should instead use the following information to prepare the remote computer to host SSRS.

- Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-	Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

-	Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS14.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you did not use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS14.<INSTANCE_NAME>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

#### To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file
1. On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2. Locate the folder \Program Files\Microsoft SQL Server\MSRS14.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3. Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4. In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located previously.

#### To add a code segment to the rssrvpolicy.config file
1. On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the following folder:

  -	Locate \Program Files\Microsoft SQL Server\MSRS14.MSSQLSERVER\Reporting Services\ReportServer.

2. Using an XML editor of your choice (such as Notepad), open the rssrvpolicy.config file.

3. Scroll through the rssrvpolicy.config file and locate the code segments. The following code shows an example of a segment.

  ```

    class="UnionCodeGroup"
    version="1"
    PermissionSetName="FullTrust">
    <IMembershipCondition
       class="UrlMembershipCondition"
       version="1"
       Url="$CodeGen$/*"
    />

  ```

4. Add the following segment in its entirety in the same section as the other segments.

   ```

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

   ```

5. Save the changes and close the XML editor.

#### To add an Extension tag to the Data segment in the rsreportserver.conf file
1.	On the computer hosting SSRS, locate the file rsreportserver.config in the following folder:

   -	Locate \Program Files\Microsoft SQL Server\MSRS14.MSSQLSERVER\Reporting Services\ReportServer.

2. Using an XML editor of your choice (such as Notepad), open the rsreportserver.config file.

3. Scroll through the rsreportserver.config file and locate the code segment. There is only one code segment in this file.

4. Add the following **Extension** tag to the code segment where all the other **Extension** tags are:
   ```
      <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />

    ```

5. Save the changes and close the XML editor.

### SM console installed on a VMM Server causes VMM connector failure
**Description**: If you install Service Manager console on the same server as VMM, then you cannot use that Service Manager console to create a VMM connector to that VMM server.

**Workaround**: Use a different Service Manager console to create the VMM connector.

### SM console installed on an Operations Manager management server causes an error
**Description**: You cannot install the Service Manager console on an Operations Manager management server. This capability is currently not supported.

**Workaround**: None.

### Data Warehouse Setup might fail if the DB or log path has a single quote
**Description**: During setup, if you specify a database or log path that includes a single quotation mark character ('), setup might fail.

**Workaround**: Use the path without a single quotation.

### Setup might fail if the SM Authoring Tool was installed earlier
**Description**: Setup of SM Authoring tool might fail if you have previously installed any version of the Service Manager Authoring Tool.

**Workaround**: Remove the earlier version of Service Manager Authoring Tool, and then retry the setup.

### Setup does not install the Report Viewer language pack
**Description**: Setup includes a prerequisite checker that checks for and - if necessary, installs - the Microsoft Report Viewer. However, Setup does not install the Report Viewer language pack, which makes the Microsoft Report Viewer compatible with Windows operating systems that are configured to use languages other than English.

**Workaround**: If your system is configured to use a language other than English, you should manually install the Report Viewer Language Pack for that language.

### SM Setup fails if a SQL Server instance contains a *$* character
**Description**: If you attempt to install Service Manager using a named Structured Query Language (SQL) instance that contains a dollar sign (*$*) character, setup fails.

**Workaround**: Use a SQL instance that does not contain the *$* character in its name.

### Orchestrator Connector Account Password cannot contain *$* characters
**Description**: If the Orchestrator connector account password contains a *$* character, the sync job completes, however runbooks are not updated in the Service Manager database.

**Workaround**: If your Orchestrator connector account password contains a *$* character, change the password to one that does not include the *$* character.

### Information linked from Setup might not display localized content
**Description**: Information that is linked from Setup to the Setup log and to technical documentation might not display localized content. Setup logs in Service Manager are available in English only. Technical documentation is available in a variety of localized languages. Where available, localized technical documentation is displayed on TechNet; however, not all languages are available.

**Workaround**: None.

### Errors might occur when you modify or delete Service Request template items
**Description**: When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround**: When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.

### Configuration of Reporting Server might take a longer time
**Description**: When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround**: None.

### Double-Byte characters are sent incorrectly to search provider
**Description**: When you perform a knowledge search and you type double-byte characters in the Search Provider box, they are not sent correctly to the search website. Instead, erroneous characters are sent.

**Workaround**: None.

### Sorting knowledge articles by date does not work
**Description**: When you try to sort knowledge articles by date, sorting does not work.

**Workaround**: None.

### Inconsistent formats for time in some areas
**Description**: The time format in some views, such as Workitems/IncidentManagement/All Incident, is not consistent with the system local settings. This issue might occur when you work with the views in unsealed management packs (MP).

**Workaround**:
To resolve this issue, follow the steps:

1. Export the Service Manager Incident Management Configuration Library management pack.

2. Modify the management pack. Locate the **LastModified** column and modify the binding as shown below:

**Before modification**

<mux:Column Name="lastModified" DisplayMemberBinding="{Binding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

**After modification**

<mux:Column Name="lastModified" DisplayMemberBinding="{datebinding:DateBinding Path=$LastModified$, Mode=OneWay}" Width="150" DisplayName="Header_Last_Modified" Property="$LastModified$" DataType="s:DateTime" />

1.	Repeat steps 1–2 for columns that are named **LastModified**.
2.	Re-import the modified management pack.
3.	Restart the console.
