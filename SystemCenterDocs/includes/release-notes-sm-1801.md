---
description: include file to detail the release notes for Service Manager 1801
ms.topic: include
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service:  system-center-threshold
ms.subservice: service-manager
keywords:
ms.date: 05/07/2018
title: include file
ms.assetid: 135c0449-c04a-4329-a67e-38f7abe82896
---

## Release Notes for System Center 1801 - Service Manager

The following sections detail the release notes for SM 1801 and include the known issues and workarounds.

## SQL Server 2014 cardinality estimation might affect the performance of SM
**Description:** If your Service Manager database is running on SQL Server 2014 with the cardinality estimator set to the SQL Server 2014 version, you may experience slow performance.

**Workaround:** Switch the Cardinality Estimator (CE) for the SQL Server to use the SQL Server 2012 version. For more information on changing the Cardinality Estimator, see [New functionality in SQL Server 2014 - Part 2 - New Cardinality Estimation](/archive/blogs/saponsqlserver/new-functionality-in-sql-server-2014-part-2-new-cardinality-estimation).

## Prerequisite for installing SM Authoring Tool
**Description:** Microsoft Visual C++ 2012 Redistributable should be installed before deploying Service Manager 1801 Authoring Tool.

**Workaround:** None

## Create Exchange Connector wizard might crash
**Description:** Creating a new Exchange Connector via Service Manager 1801 console throws an exception if the admin selects the "Test Connection" button in the "Server Connection" pane of "Create Exchange Connector" wizard.

**Workaround:** To work around this issue, avoid selecting "Test Connection" button in the "Create Exchange Connector" wizard. Instead, directly select the "Next" button, which internally tests the connection and doesn't crash the wizard.

If the crash has already occurred, you can restart the wizard and use this workaround.

## Browsing domain in AD connector wizard raises error
**Description:** Error is raised on selecting “Browse” while choosing Domain or OU in AD connector wizard of Service Manager 1801 console.

**Workaround:** Install Microsoft Visual C++ 2012 Redistributable on the affected machine.

## Error while creating a new software type configuration item
**Description:** The property “Is Virtual Application" in create Software configuration item form is mandatory, but the asterix (\*) symbol isn't shown for this property. Hence, on selecting **Ok** or **Apply** button without setting this field throws an error and makes the form unusable.

**Workaround:** Reopen the create Software configuration item form, and fill all the details including the field "Is Virtual Application", before selecting **Ok** or **Apply** button.

## Manual steps to configure remote SQL Server 2014 reporting services
**Description:** During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you're prompted to follow a procedure in the Deployment Guide to prepare the server. However, if you use SQL Server 2014, you should instead use the following information to prepare the remote computer to host SSRS.

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-   Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you didn't use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS12.<INSTANCE_NAME>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

**To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file**

1.  On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2.  For SQL Server 2014, locate the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3.  Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4.  In the Prerequisites folder, select **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located previously.

**To add a code segment to the rssrvpolicy.config file**

1.  On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the following folder:

    - For SQL Server 20014, locate \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer.

2.  Using an XML editor of your choice (such as Notepad), open the rssrvpolicy.config file.

3.  Scroll through the rssrvpolicy.config file and locate th code segments. The following code shows an example of a segment.

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

4.  Add the following segment in its entirety in the same section as the other segments.

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

5.  Save the changes and close the XML editor.

### To add an Extension tag to the Data segment in the rsreportserver.conf file

1.  On the computer hosting SSRS, locate the file rsreportserver.config in the following folder:

    -   For SQL Server 2014, locate \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer.

2.  Using an XML editor of your choice (such as Notepad), open the rsreportserver.config file.

3.  Scroll through the rsreportserver.config file and locate the code segment. There's only one code segment in this file.

4.  Add the following **Extension** tag to the code segment where all the other **Extension** tags are:

    ```
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />
    ```

5.  Save the changes and close the XML editor.


## SM console installed on a VMM Server causes VMM connector failure
**Description:** If the Service Manager console is installed on the same server as VMM, then you can't use that Service Manager console to create a VMM connector to that VMM server.

**Workaround:** None; however, you can use a different Service Manager console to create the VMM connector.

## SM console installed on an Operations Manager management server causes an error

**Description:** Installing the Service Manager console on an Operations Manager management server isn't supported.

**Workaround:** None.


## Data Warehouse Setup might fail if the DB or log path has a single quote
**Description:** During Setup, if you specify a database or log path that includes a single quotation mark character ('), Setup might fail.

**Workaround:** None. The path that you specify can't include a single quotation mark character.

## Setup might fail if the SM Authoring Tool was installed earlier
**Description:** Setup might fail if you've previously installed any version of the Service Manager Authoring Tool.

**Workaround:** Remove the Service Manager Authoring Tool, and then retry Setup.

## Setup does not install the Report Viewer language pack
**Description:** Setup includes a prerequisite checker that checks for and, if necessary, installs the Microsoft Report Viewer. However, Setup doesn't install the Report Viewer Language Pack, which makes the Microsoft Report Viewer compatible with Windows operating systems that are configured to use languages other than English.

**Workaround:** If your system is configured to use a language other than English, you should manually install the Report Viewer Language Pack for that language.

## SM Setup fails if a SQL Server instance contains a $ character
**Description:** If you attempt to install Service Manager using a named Structured Query Language (SQL) instance that contains a dollar sign ($) character, Setup fails.

**Workaround:** Use a SQL instance that doesn't contain the $ character in its name.

## Orchestrator Connector Account Password cannot contain $ characters
**Description:** If the Orchestrator connector account password contains a $ character, the sync job completes; however, runbooks aren't updated in the Service Manager database.

**Workaround:** If your Orchestrator connector account password contains a $ character, change the password to one that doesn't include the $ character.

## Information linked from Setup might not display localized content
**Description:** Information that is linked from Setup to the Setup log and to technical documentation might not display localized content. Setup logs in Service Manager are available in English only. Technical documentation is available in various localized languages. Where available, localized technical documentation is displayed on TechNet; however, not all languages are available.

**Workaround:** None.


## Errors might occur when you modify or delete Service Request template items
**Description:** When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround:** When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.


## Configuration of Reporting Server might take a longer time
**Description:** When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround:** None.

## Double-Byte characters are sent incorrectly to search provider
**Description:** When you perform a knowledge search and you enter double-byte characters in the Search Provider box, they aren't sent correctly to the search website. Instead, erroneous characters are sent.

**Workaround:** None.

## Sorting knowledge articles by date does not work
**Description:** When you try to sort knowledge articles by date, sorting doesn't work.

**Workaround:** None.

## Active directory group expansion selection after upgrade
**Description:** When upgrading from System Center 2012 R2 - Service Manager to System Center 1801 - Service Manager, don't change the AD group expansion selection value in any AD connector (if it's OFF, let it remain OFF; if it's ON, let it remain ON), until the connector has run at least one time after the upgrade.

**Workaround:** None.

## SM authoring tool console crashes while creating workflows
This issue is fixed.