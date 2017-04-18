---
title: Troubleshoot data warehouse jobs using cmdlets
description: Describes how you can troubleshoot Service Manager data warehouse jobs using cmdlets.
manager: carmonm
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
keywords:
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
ms.assetid: 56b7f6c9-7960-4a6c-b933-0fe8ca0475d6
---

# Troubleshoot Service Manager data warehouse jobs using cmdlets.

>Applies To: System Center 2016 - Service Manager

In System Center - Service Manager, after the Data Warehouse Registration Wizard is complete and after Reporting becomes available in the Service Manager console, you can start running reports. If you encounter a problem with reports \(for example, the incident management report you run does not show the current data\), you can use Windows&nbsp;PowerShell cmdlets to troubleshoot the problem. For example, you can use the following procedure to determine whether a transform job failed, and you can evaluate any error messages that the transform job created.  

### To troubleshoot data warehouse jobs by using Windows&nbsp;PowerShell cmdlets  

1.  On the computer that hosts the data warehouse management server, click **Start**, click **All Programs**, click **Accessories**, and then click **Windows PowerShell**.  

2.  Right\-click **Windows PowerShell**, and then click **Run as administrator**.  

3.  At the Windows&nbsp;PowerShell command prompt, type the following command, and then press ENTER:  

    ```  
    Import-Module .\Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1  

    ```  

4.  Type the following command, and then press ENTER:  

    ```  
    Get-SCDWJob  
    ```  

5.  Review the output, and locate any job with a status of "Failed."  

6.  Type the following command, and then press ENTER. In the command, specify the data warehouse job that failed as the value of the *JobName* parameter.  

    ```  
    Get-SCDWJobModule -JobName Transform.Common  
    ```  

7.  In the output, locate a status of "Failed," and then review the **Error Message** column for more information about why the data warehouse job failed.  

8.  When you are ready to retry the failed job, type the following command, and then press ENTER:  

    ```  
    Resume-SCDWJob -JobName Transform.Common  
    ```
