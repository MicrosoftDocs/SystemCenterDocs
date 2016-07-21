---
title: How to Configure a Management Server for Client Monitoring
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b05d6505-9d00-4a25-8763-5f51977d9784
author:mgoedtel
manager:cfreemanwa
---
# How to Configure a Management Server for Client Monitoring
Use the following procedures to configure a management server for the server component of the Client Monitoring feature of [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)].  
  
> [!IMPORTANT]  
> If you plan to configure the management server to forward error reports to Microsoft and receive links to available solutions for those errors or participate in the Customer Experience Improvement Program \(CEIP\), you must first configure the management server's proxy settings if it uses a proxy server to access the Internet.  
  
The Operations Manager&nbsp;Client Monitoring Configuration Wizard is used to configure the server component of Client Monitoring on an Operations Manager&nbsp;management server. To configure the server component of Client Monitoring on multiple management servers, run the wizard once for each management server. An example of when you might configure multiple management servers for Client Monitoring is if the connection between specific clients and management servers is less expensive.  
  
> [!IMPORTANT]  
> The management server and error reporting clients must be in the same or fully trusted domains.  
  
### To open the Client Monitoring Configuration Wizard  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the **Administration** workspace, click **Management Servers**.  
  
4.  In the **Management Servers** pane, right\-click the management server on which you want to enable Client Monitoring, and then click **Configure Client Monitoring**. This will start the **Client Monitoring Configuration Wizard**. Use the same procedure to **Disable Client Monitoring** on the management server. You must also disable Client Monitoring on the clients.  
  
    > [!NOTE]  
    > The **Configure Client Monitoring** option will be unavailable if the selected computer is a gateway server.  
  
### To configure Client Monitoring using the Client Monitoring Configuration Wizard  
  
1.  On the **Introduction** page of the **Client Monitoring Configuration Wizard**, click **Next**. The Introduction page is skipped if the wizard has run previously and the **Do not show this page again** check box was selected.  
  
2.  On the **Customer Experience Improvement Program** page, do one of the following:  
  
    -   Leave the default option of **No** if you do not want your organization to participate in the program, and then click **Next**.  
  
    Or  
  
    1.  Select **Yes**, if you want your organization to participate in the program.  
  
    2.  Leave **Use Secure Socket Layer \(SSL\) protocol** selected if you have installed a certificate on your management server, leave **Use Windows Authentication** selected if you want the client computers to authenticate with the management server; otherwise, clear the options.  
  
    3.  Type the appropriate **Port**, or leave the default of 51907, and then click **Next**.  
  
3.  On the **Error Collection** page, do the following:  
  
    1.  Type the local or attached **File Share Path**, such as C:\\ErrorData, for the management server that will be used to collect error reports. The file share will be created at the local path on the management server and shared with the necessary permissions.  
  
        > [!IMPORTANT]  
        > The file share path must be on an NTFS partition and have at least 2 GB of free disk space. It is recommended that the path is no longer than 120 characters. The file share path can be a local drive path on the selected management server such as C:\\ErrorData, or a UNC path to an existing network share such as \\\\Server\\FileShare\\ErrorData.  
  
    2.  Select **Collect application errors from Windows Vista or later computers** if you are managing Windows Vista or later operating systems with Operations Manager. Type a **Port** number, or leave the default 51906. Leave **Use Secure Socket Layer protocol** selected if you have installed a certificate on your management server, leave **Use Windows Authentication** selected if you want the client computers to authenticate with the management server; otherwise, clear the options.  
  
    3.  Type the **Organization Name**, using no more than 22 characters, and then click **Next**. The Organization Name can display on computers experiencing errors that are running Windows Server&nbsp;2003 and earlier operating systems.  
  
4.  On the **Error Forwarding** page, do one of the following:  
  
    -   Leave the **Automatically forward all collected errors to Microsoft** check box cleared, and then click **Next**.  
  
    -   Or  
  
    1.  Select **Automatically forward all collected errors to Microsoft** if the management server is connected to the Internet and you want to forward error reports to Microsoft and receive links to available solutions for those errors.  
  
    2.  Select **Detailed** to help ensure Microsoft can provide a solution to the issue, or leave the default setting of **Basic**.  
  
    3.  Click **Next**.  
  
5.  On the **Create File Share** page, do one of the following:  
  
    -   Select an **Existing User Account** from the list, and then click **Next**.  
  
    -   Select **Other user account**, type the **User name** and **Password**, select the **Domain** from the list, and then click **Next**.  
  
        > [!IMPORTANT]  
        > The account must have the permissions necessary to create a file share on the path provided in step 3a.  
  
6.  On the **Create file Share: Task Status** page, after the file share is successfully created, click **Next**.  
  
    > [!NOTE]  
    > To modify the Client Monitoring settings on the management server, such as the file share, you must disable and then re\-enable Client Monitoring on the management server. You must also then modify the Client Monitoring Group Policy settings on the clients.  
  
7.  On the **Client Configuration Settings** page, type or **Browse** to the location you want to save the settings from the Client Monitoring Configuration Wizard. These settings are saved in a Group Policy template file named *ServerName*.ADM. Click **Finish**.  
  
    > [!IMPORTANT]  
    > You must use the *ServerName*.ADM file to configure clients to redirect their Client Monitoring data to the management server. For more information, see [How to Configure Clients for Client Monitoring](../../om/manage/How-to-Configure-Clients-for-Client-Monitoring.md).  
  
## See Also  
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](../../om/manage/Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)  
[How to Configure Clients for Client Monitoring](../../om/manage/How-to-Configure-Clients-for-Client-Monitoring.md)  
[How to Customize Client Monitoring Data Collection and Solution Response URLs for Error Groups](../../om/manage/How-to-Customize-Client-Monitoring-Data-Collection-and-Solution-Response-URLs-for-Error-Groups.md)  
[How to Configure Error Transmission Settings for Client Monitoring in Operations Manager](../../om/manage/How-to-Configure-Error-Transmission-Settings-for-Client-Monitoring-in-Operations-Manager.md)  
[Forwarding Client Error Reports &#40;Client Monitoring&#41;](../../om/manage/Forwarding-Client-Error-Reports--Client-Monitoring-.md)  
  
