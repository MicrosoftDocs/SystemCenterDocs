---
title: How to Deploy ACS Reporting
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d8e668e-087e-4117-916b-48aac65ab72b
---
# How to Deploy ACS Reporting
You deploy Audit Collection Services \(ACS\) Reporting on a supported version of Microsoft SQL Server Reporting Services \(SSRS\) instance. If [!INCLUDE[om12long](Token/om12long_md.md)] Reporting has also been installed on the same SSRS instance, you can view the ACS Reports in the Operations console. Before you deploy ACS, there are a number of prerequisite steps you must perform, such as ensuring that a ACS is configured on management server within your management group. For more information, see [Deploying ACS and ACS Reporting](assetId:///acbe8dba-82f5-447b-a01c-9abb337e378c).

### To deploy ACS Reporting

1.  Log on to the server that will be used to host ACS reporting as a user that is an administrator of the SSRS instance.

2.  Create a temporary folder, such as **C:\\acs**.

3.  On your installation media, go to **\\ReportModels\\acs** and copy the directory contents to the temporary installation folder.

    There are two folders \(**Models** and **Reports**\) and a file named **UploadAuditReports.cmd**.

4.  On your installation media, go to **\\SupportTools** and copy the file **ReportingConfig.exe** into the temporary **acs** folder.

5.  Open a Command Prompt window by using the **Run as Administrator** option, and then change directories to the temporary **acs** folder.

6.  Run the following command. 
    **UploadAuditReports “<AuditDBServer\\Instance>” “<Reporting Server URL>” “<path of the copied acs folder>”**
    For example: **UploadAuditReports “myAuditDbServer\\Instance1” “http:\/\/myReportServer\/ReportServer$instance1” “C:\\acs”**

    This example creates a new data source called **Db Audit**, uploads the reporting models **Audit.smdl** and **Audit5.smdl**, and uploads all reports in the **acs\\reports** directory.

    > [!NOTE]
    > The reporting server URL needs the reporting server virtual directory \(**ReportingServer\_<InstanceName>**\) instead of the reporting manager directory \(**Reports\_<InstanceName>**\).

7.  Open Internet Explorer and enter the following address to view the **SQL Reporting Services Home** page. **http:\/\/<yourReportingServerName>\/Reports\_<InstanceName>**

8.  Click **Audit Reports** in the body of the page and then click **Show Details** in the upper right part of the page.

9. Click the **Db Audit** data source.

10. In the **Connect Using** section, select **Windows Integrated Security** and click **Apply**.

## See Also
[Deploying ACS and ACS Reporting](assetId:///acbe8dba-82f5-447b-a01c-9abb337e378c)
[How to Install an Audit Collection Services \(ACS\) Collector and Database](assetId:///ff3c1d14-2ead-472f-967b-c827544437f1)
[How to Deploy ACS on a Secondary Management Server](assetId:///d1b8064f-01dd-4c54-94c4-b64f61b994d5)
[How to Install Audit Collection Services \(ACS\)](assetId:///7686cf46-0792-4057-8d47-920063fc8928)


