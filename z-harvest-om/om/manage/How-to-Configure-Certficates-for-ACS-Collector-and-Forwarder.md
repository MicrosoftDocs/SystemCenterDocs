---
title: How to Configure Certficates for ACS Collector and Forwarder
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57f8e8e1-ec41-4128-9920-6bebb1b5ed26
author:mgoedtel
manager:cfreemanwa
---
# How to Configure Certficates for ACS Collector and Forwarder
When the Audit Collection Service \(ACS\) Forwarder is located in a domain separate from the domain where the ACS Collector is located, and no two\-way trust exists between the two domains, certificates must be used so that authentication can take place between the ACS Forwarder and the ACS Collector.  
  
Before you configure certificates, ensure that the following actions have been completed:  
  
-   On the ACS Forwarder:  
  
    -   An agent is installed on the computer that will serve as the ACS Forwarder. For more information, see [Operations Manager Agent Installation Methods](../Topic/Operations%20Manager%20Agent%20Installation%20Methods.md).  
  
    -   A certificate and certification authority \[CA\] certificate is installed on the computer hosting the agent. For more information, see [Authentication and Data Encryption for Windows Computers](https://go.microsoft.com/fwlink/p/?LinkID=227146) in the Deployment Guide.  
  
-   On the ACS Collector:  
  
    -   A certificate \(and CA certificate\) is installed on the management server hosting the ACS Collector. For more information, see [Authentication and Data Encryption for Windows Computers](https://go.microsoft.com/fwlink/p/?LinkID=227146) in the Deployment Guide.  
  
    -   The pending agent is approved and communication between the agent and the management server is operating properly. For more information, see [Process Manual Agent Installations](../Topic/Process%20Manual%20Agent%20Installations.md).  
  
    -   The ACS Collector and database is installed. For more information, see [How to Install an Audit Collection Services \(ACS\) Collector and Database](https://go.microsoft.com/fwlink/?LinkID=229042) in the Deployment Guide.  
  
The following is a high\-level overview of the steps that need to be performed to use certificates with ACS.  
  
> [!IMPORTANT]  
> Certificates used on various components in Operations Manager&nbsp;\(for example, ACS Collector, ACS Forwarder, agent, gateway server, or management server\) must be issued by the same CA.  
  
On the computer hosting the ACS Collector:  
  
-   Run ADTServer \-c.  
  
-   Map the ACS Forwarder Certificate in Active Directory.  
  
-   In the Operations console, enable ACS.  
  
On the computer hosting the ACS Forwarder:  
  
-   Export the certificate to a disk, USB flash drive, or network share.  
  
-   Run ADTAgent \-c.  
  
### To assign a certificate to the ACS Collector  
  
1.  On the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, type **cmd**, and then click **OK**.  
  
3.  At the command prompt, type <*drive\_letter*>: \(where <*drive\_letter*> is the drive where the operating system is installed\), and then press ENTER.  
  
4.  Type **cd %systemroot%**, and then press ENTER.  
  
5.  Type **cd system32\\security\\adtserver**, and then press ENTER.  
  
6.  Type **net stop adtserver**, and then press ENTER.  
  
7.  Type **adtserver \-c**, and then press ENTER.  
  
8.  In the numbered list of certificates, find the certificate used for Operations Manager, type the number in the list \(should be 1\), and then press ENTER.  
  
9. Type **net start adtserver** and then press ENTER.  
  
### To configure named mapping to the certificate  
  
1.  Log on to the computer hosting Active Directory.  
  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Active Directory Users and Computers**.  
  
3.  Expand the domain name, right\-click **Computers**, point to **New**, and then click **Computer**.  
  
4.  In the **New Object \- Computer** dialog box, enter the NetBIOS name of the computer that is hosting the ACS Forwarder, and then click **Next**. Repeat this step for every computer that hosts an ACS Forwarder.  
  
5.  In the **Managed** dialog box, ensure that **This is a managed computer** is not selected, and then click **Next**.  
  
6.  In the **New Object \- Computer** dialog box, click **Finish**.  
  
7.  In **Active Directory Computers and Users**, in the right pane, right\-click the computer \(or computers\) you added, and then click **Name Mappings**.  
  
8.  In the **Security Identity Mapping** dialog box, click **X.509 Certificates**, and then click **Add**.  
  
9. In the **Add Certificate** dialog box, click the **Look in** menu, select the location where the exported certificate is located, and then click **Open**.  
  
10. In the **Add Certificate** dialog box, ensure that **Use Subject for alternate security identity** is selected, and then click **OK**.  
  
11. In the **Security Identity Mapping** dialog box, click **OK**.  
  
12. Repeat steps 4-11 for each computer you have added.  
  
After you complete these procedures, you need to enable the ACS Forwarders. For more information, see [How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md).  
  
### To export the certificate  
  
1.  On the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, type **mmc**, and then click **OK**.  
  
3.  On the **File** menu, click **Add\/Remove Snap\-in**.  
  
4.  In the **Add\/Remove Snap\-in** dialog box, click **Add**.  
  
5.  In the **Add Standalone Snap\-in** dialog box, click **Certificates**, and then click **Add**.  
  
6.  In the **Certificates snap\-in** dialog box, select **Computer account**, and then click **Next**.  
  
7.  In the **Select Computer** dialog box, select **Local computer \(the computer this console is running on\)**, and then click **Finish**.  
  
8.  In the **Add Standalone Snap\-in** dialog box, click **Close**.  
  
9. In the **Add\/Remove Snap\-in** dialog box, click **OK**.  
  
10. In the Console Root\\Certificates \(Local Computer\) pane, expand **Certificates \(Local Computer\)**, expand **Personal**, and then click **Certificates**.  
  
11. In the results pane, right\-click the certificate you are using for Operations Manager, point to **All Tasks**, and then click **Export**.  
  
12. In the **Certificate Export Wizard**, on the **Welcome** page, click **Next**.  
  
13. On the **Export Private Key** page, select **No, do note export the private key**, and then click **Next**.  
  
14. On the **Export File Format** page, select **DER encoded binary X.509 \(.CER\)**, and then click **Next**.  
  
15. On the **File to Export** page, click **Browse**.  
  
16. On the **Save As** page, select a folder and file name for the certificate, ensure that the **Save as type** is set to **DER Encoded Binary X.509 \(\*.cer\)**, and then click **Save**.  
  
    > [!NOTE]  
    > You will need to copy this certificate to the computer hosting the ACS Collector, so choose a location that the ACS Collector can read from, or consider saving the certificate to a disk, USB flash drive, or network share. In addition, it is recommended that you include the computer name in the file name if you are exporting certificates from more than one computer.  
  
17. On the **File to Export** page, ensure that the path and file name are correct, click **Next**, and then click **Finish**.  
  
### To run the adtagent command  
  
1.  On the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, type **cmd**, and then click **OK**.  
  
3.  At the command prompt, type <*drive\_letter*>: \(where <*drive\_letter*> is the drive where the Operating System is installed\), and then press ENTER.  
  
4.  Type **cd %systemroot%** and then press ENTER.  
  
5.  Type **cd system32** and then press ENTER.  
  
6.  Type **adtagent \-c** and then press ENTER.  
  
7.  You will see a numbered list of certificates. Find the certificate used for Operations Manager, type the number in the list \(should be 1\), and then press ENTER.  
  
8.  Type **exit** to close the command window.  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)  
[How to Enable Event Logging and ACS Rules on Solaris and AIX Computers](../../om/manage/How-to-Enable-Event-Logging-and-ACS-Rules-on-Solaris-and-AIX-Computers.md)  
[How to Filter ACS Events for UNIX and Linux Computers](../../om/manage/How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[How to Remove Audit Collection Services &#40;ACS&#41;](../../om/manage/How-to-Remove-Audit-Collection-Services--ACS-.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
