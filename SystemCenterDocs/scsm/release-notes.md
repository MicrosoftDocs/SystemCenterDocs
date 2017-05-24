---
description: Release Notes for System Center 2016 - Service Manager
manager:  carmonm
ms.topic: article
author:  bandersmsft
ms.author: banders
ms.prod:  system-center-threshold
ms.technology: Orchestrator
keywords:
ms.date: 05/24/2017
title:  Release Notes for System Center 2016 - Service Manager
---

# Release Notes for System Center 2016 - Service Manager

**The following release notes apply to System Center 2016 - Service Manager.**


## Silverlight based Self Service Portal for System Center Service Manager

- Status in System Center 2016: Removed.
- Replacement: A new HTML based Self Service Portal is available with System Center 2016 - Service Manager.

## Microsoft IT GRC Process Management Pack SP1 for Service Manager

- Status in System Center 2016 : Removed.
- Replacement: We recommend that you engage with proactive governance partners that can integrate into your current System Center investments.

## Chargeback reports

- Status in System Center 2016: Removed.
- Replacement: None.

## SQL Server 2014 Cardinality Estimation might affect the performance of Service Manager 2016
**Description:** If your Service Manager database is running on SQL Server 2014 with the cardinality estimator set to the SQL Server 2014 version you may experience slow performance.

**Workaround:** Switch the Cardinality Estimator (CE) for the SQL Server to use the SQL Server 2012 version. See the following article for more information on changing the Cardinality Estimator: [New functionality in SQL Server 2014 - Part 2 - New Cardinality Estimation](https://blogs.msdn.microsoft.com/saponsqlserver/2014/01/16/new-functionality-in-sql-server-2014-part-2-new-cardinality-estimation/).

## Microsoft Visual C++ 2012 Redistributable is a pre-requisite for installing Service Manager 2016 Authoring Tool
**Description:** Microsoft Visual C++ 2012 redistributable should be installed before deploying Service Manager 2016 Authoring Tool.

**Workaround:** None

## Create Exchange Connector wizard might crash
**Description:** Creating a new Exchange Connector via Service Manager 2016 console throws an exception if the admin clicks on the "Test Connection" button in the "Server Connection" pane of "Create Exchange Connector" wizard.

**Workaround:** To work around this issue, avoid clicking "Test Connection" button in the "Create Exchange Connector" wizard. Instead, directly click the "Next" button, which internally tests the connection and does not crash the wizard.

If the crash has already occurred, you can restart the wizard and use this workaround.

## Browsing domain in AD connector wizard raises error
**Description:** Error is raised on clicking “Browse” while choosing Domain or OU in AD connector wizard of Service Manager 2016 console.

**Workaround:** Install Microsoft Visual C++ 2012 Redistributable on the affected machine.

## Creating a new Software type configuration item throws the error - "The form could not be submitted for the following reasons: Property Is Virtual Application must be set"
**Description:** The property “Is Virtual Application" in create Software configuration item form is mandatory, but the asterix (\*) symbol is not shown for this property. Hence on clicking "Ok" or "Apply" button without setting this field throws an error and makes the form unusable.

**Workaround:** Reopen the create Software configuration item form, and fill all the details including the field "Is Virtual Application", before clicking on "Ok" or "Apply" button.

## Manual steps to configure remote SQL Server 2014 Reporting Services
**Description:** During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL Server Reporting Services (SSRS) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you are prompted to follow a procedure in the Deployment Guide to prepare the server. However, if you use SQL Server 2014, you should instead use the following information to prepare the remote computer to host SSRS.

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-   Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll (which is located in the Prerequisites folder on your Service Manager installation media) to the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin on the computer that is hosting SSRS. If you did not use the default instance of SQL Server, the path of the required folder is \Program Files\Microsoft SQL Server\MSRS12.<INSTANCE_NAME>\Reporting Services\ReportServer\Bin. In the following procedure, the default instance name is used.

**To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file**

1.  On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2.  For SQL Server 2014, locate the folder \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\Bin.

3.  Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.

4.  In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located previously.

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

3.  Scroll through the rsreportserver.config file and locate the code segment. There is only one code segment in this file.

4.  Add the following **Extension** tag to the code segment where all the other **Extension** tags are:

    ```
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />
    ```

5.  Save the changes and close the XML editor.


## Service Manager console installed on a VMM Server causes VMM connector failure
**Description:** If the Service Manager console is installed on the same server as VMM, then you cannot use that Service Manager console to create a VMM connector to that VMM server.

**Workaround:** None, however you can use a different Service Manager console to create the VMM connector.


## Data Warehouse Setup Might Fail if the Database or Log Path Includes a Single Quotation Mark Character
**Description:** During Setup, if you specify a database or log path that includes a single quotation mark character ('), Setup might fail.

**Workaround:** None. The path that you specify cannot include a single quotation mark character.

## Setup Might Fail if the Service Manager Authoring Tool Has Been Installed
**Description:** Setup might fail if you have previously installed any version of the Service Manager Authoring Tool.

**Workaround:** Remove the Service Manager Authoring Tool, and then retry Setup.

## Setup Does Not Install the Report Viewer Language Pack
**Description:** Setup includes a prerequisite checker that checks for and - if necessary, installs - the Microsoft Report Viewer. However, Setup does not install the Report Viewer Language Pack, which makes the Microsoft Report Viewer compatible with Windows operating systems that are configured to use languages other than English.

**Workaround:** If your system is configured to use a language other than English, you should manually install the Report Viewer Language Pack for that language.

## Service Manager Setup Fails if a SQL Server Instance Contains a $ Character
**Description:** If you attempt to install Service Manager using a named Structured Query Language (SQL) instance that contains a dollar sign ($) character, Setup fails.

**Workaround:** Use a SQL instance that does not contain the $ character in its name.

## Orchestrator Connector Account Password Cannot Contain $ Characters
**Description:** If the Orchestrator connector account password contains a $ character, the sync job completes, however runbooks are not updated in the Service Manager database.

**Workaround:** If your Orchestrator connector account password contains a $ character, change the password to one that does not include the $ character.

## Information Linked from Setup Might Not Display Localized Content
**Description:** Information that is linked from Setup to the Setup log and to technical documentation might not display localized content. Setup logs in Service Manager are available in English only. Technical documentation is available in a variety of localized languages. Where available, localized technical documentation is displayed on TechNet; however, not all languages are available.

**Workaround:** None.


## Errors Might Occur When You Modify or Delete Service Request Template Items
**Description:** When you create a service request using a request offering template and you modify or delete activities that are contained in the template, various errors might occur that prevent you from saving the service request.

**Workaround:** When you create service requests, avoid modifying or deleting activities that are contained in a request offering template. If necessary, you can create a new request offering template with only the activities that are necessary and configured properly for your intended use.


## Configuring the Reporting Server Might Take a Long Time
**Description:** When you install the data warehouse, validation of the default web server URL might take as long as 25 seconds to complete.

**Workaround:** None.

## Double-Byte Characters Are Sent Incorrectly to Search Provider
**Description:** When you perform a knowledge search and you type double-byte characters in the Search Provider box, they are not sent correctly to the search website. Instead, erroneous characters are sent.

**Workaround:** None.

## Sorting Knowledge Articles by Date Does Not Work
**Description:** When you try to sort knowledge articles by date, sorting does not work.

**Workaround:** None.

## Do not change Active Directory group expansion selection after upgrade until the connector has run at least one time.
**Description:** When upgrading from System Center 2012 R2 - Service Manager to System Center 2016 - Service Manager, do not change the AD group expansion selection value in any AD connector (if it is OFF, let it remain OFF, if it is ON, let it remain ON), until the connector has run at least one time after the upgrade.

**Workaround:** None.
