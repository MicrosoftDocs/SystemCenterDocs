---
title: Manual steps to configure remote SQL Server Reporting Services
description: When you deploy the Service Manager data warehouse management server, you can choose the server where Microsoft SQL Server Reporting Services is deployed.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f0b7917-ba9f-49de-93bb-17d26fb2bf11
---

# Manual steps to configure remote SQL Server Reporting Services

>Applies To: System Center 2016 - Service Manager

During deployment of the Service Manager data warehouse management server, you can specify the server to which Microsoft SQL&nbsp;Server Reporting Services \(SSRS\) will be deployed. During setup, the computer that is hosting the data warehouse management server is selected by default. If you specify a different computer to host SSRS, you are prompted to follow this procedure to prepare the server. Preparing the remote computer to host SSRS involves the following steps, which are covered in detail in this section:  

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.  

-   Add a code segment to the rssrvpolicy configuration file on the computer that is hosting SSRS.  

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.  

 If you used the default instance of SQL&nbsp;Server, use Windows&nbsp;Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll \(which is located in the Prerequisites folder on your Service Manager installation media\) to the folder \\Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin on the computer that is hosting SSRS. If you did not use the default instance of SQL&nbsp;Server, the path of the required folder is \\Program Files\\Microsoft SQL Server\\MSRS13.\<INSTANCE\_NAME\>\\Reporting Services\\ReportServer\\Bin. In the following procedure, the default instance name is used.  

### To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file  

1.  On the computer that will host the remote SSRS, open an instance of Windows&nbsp;Explorer.  

2.  For SQL&nbsp;Server&nbsp;2016, locate the folder \\Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin.  

3.  Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.  

4.  In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll**, and drag it to the folder that you located in either step 2.  

### To add a code segment to the rssrvpolicy.config file  

1.  On the computer that will be hosting SSRS, locate the file rssrvpolicy.config in the \\Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer folder for SQL server 2016.  


2.  Using an XML editor of your choice \(such as Notepad\), open the rssrvpolicy.config file.  

3.  Scroll through the rssrvpolicy.config file and locate the `<CodeGroup>` code segments. The following code shows an example of a `<CodeGroup>` segment.  

    ```  
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

4.  Add the following `<CodeGroup>` segment in its entirety in the same section as the other `<CodeGroup>` segments.  

    ```  
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

5.  Save the changes and close the XML editor.  

### To add an Extension tag to the Data segment in the rsreportserver.conf file  

1.  On the computer hosting SSRS, locate the file rsreportserver.config in the \Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer folder for SQL server 2016.


2.  Using an XML editor of your choice \(such as Notepad\), open the rsreportserver.config file.  

3.  Scroll through the rsreportserver.config file and locate the `<Data>` code segment. There is only one `<Data>` code segment in this file.  

4.  Add the following `Extension` tag to the `<Data>` code segment where all the other `Extension` tags are:  

    ```  
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />  
    ```  

5.  Save the changes and close the XML editor.
