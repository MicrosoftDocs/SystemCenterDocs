---
title: Using SharePoint to View Operations Manager Data
description: This article describes how deploy the Operations Manager Web console SharePoint web part for viewing select dashboards in SharePoint from Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/03/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: d19b28c0-a346-4806-8973-18d5f40ce4fb
---

# Using SharePoint to view Operations Manager data

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager includes a SharePoint Web Part that displays selected dashboards from the Web console. A configured Web Part allows you to see at a glance the availability and performance metrics for applications in your environment.  
  
The Operations Manager Web Part is particularly useful for providing current status views to individuals in your organization who are not Operations Manager users. Use the following procedures, as applicable, to set up dashboards on a SharePoint page.  
  
## How to deploy the Operations Manager web part  

The following are the prerequisites for deploying the Operations Manager web part:  
  
-   The Operations Manager web console must be installed on a management server.  
  
-   The SharePoint farm must be running SharePoint 2013, SharePoint Server 2010 Standard, SharePoint Server 2010 Enterprise, or SharePoint Foundation 2010.  
  
    > [!NOTE]  
    > If the SharePoint farm is running SharePoint Foundation 2010, you can only deploy the web part in the same domain as the web console and you cannot use shared credentials.  
  
-   You must have SharePoint administrator permissions for the SharePoint farm; specifically, you must have permissions to perform the following tasks:  
  
    -   Run the SharePoint PowerShell client  
  
    -   Start and stop the SPAdminV4 and SPTimerV4 services  
  
    -   Run the Add-SPSolution and Install-SPSolution cmdlets for the farm, and run the Enable-SPFeature cmdlet for all sites on the farm  
  
The web part is a solution file named `Microsoft.EnterpriseManagement.SharePointIntegration.wsp`. To deploy the web part, you run a script named install-OperationsManager-DashboardViewer.ps1. This script is located in the Operations Manager installation folder under *Setup\amd64\SharePoint*.  
  
> [!NOTE]  
> You can get more information on the scripts included with Operations Manager by using the command shell and the get-help cmdlet. For example: **get-help install-OperationsManager-DashboardViewer.ps1**.  
  
Using the `install-OperationsManager-DashboardViewer.ps1` script, you can deploy the web part to all sites and web applications in the farm or to a specific site or web application.  
  
1.  Copy the `install-OperationsManager-DashboardViewer.ps1` file and the `Microsoft.Enterprisemanagement.Sharepointintegration.wsp` file from the Operations Manager installation folder under *Setup\amd64\SharePoint* to a location that the SharePoint  Management Shell can access.  
  
2.  Open the SharePoint Management Shell and navigate to the directory where you saved the `install-OperationsManager-DashboardViewer.ps1` file.  
  
3.  In the SharePoint Management Shell, type the following command, and then press **Enter**.  
  
    **.\install-OperationsManager-DashboardViewer.ps1 -solutionPath***<directory for Microsoft.EnterpriseManagement.SharePointIntegration.wsp>***-url***<optional, for installing to a specific portal address or website>*  
  
    Here is an example that deploys the web part to a specific portal address. In this example you are copying the files to "C:\Program Files\Microsoft System Center 2016\Operations Manager\".  
  
    **.\install-OperationsManager-DashboardViewer.ps1 "C:\Program Files\Microsoft System Center 2016\Operations Manager \" http://localhost:4096**  
  
    If an error occurs when you run the script, you must disable the RemoteSigned default code-signing execution policy for the SharePoint Management Shell. To allow the `install-OperationsManager-DashboardViewer.ps1` script to run, type the following command, and then press **enter**:  
  
    **Set-ExecutionPolicy Unrestricted**  
  
    You will see some confirmation messages, select **Y** to confirm, and then run the script.  
  
4.  Verify that the web part is deployed and activated by performing the following steps:  
  
    1.  Open the site http://localhost.  
  
    2.  In the **Site Actions** dropdown menu, click **Site Settings**.  
  
    3.  In the **Site Collection Administration** section, click **Site collection features**.  
  
    4.  Locate **Operations Manager Dashboard Web Part**.  
  
        -   If the button to the right says **Activate**, then the feature was not automatically activated during deployment. To activate the web part, click the **Activate** button.  
  
        -   If the button to the right says **Deactivate**, no steps are required.  The Operations Manager Dashboard web part can now be inserted into site pages.  
  
5.  If you disabled the RemoteSigned default code-signing execution policy to run the `install-OperationsManager-DashboardViewer.ps1` script, you should re-enable it after the script runs. Type the following command and then press **enter**:  
  
    **Set-ExecutionPolicy Restricted**  
  
    You will see some confirmation messages, select **Y** to confirm.  
  
## How to configure the web part to connect to a Web console  

After the web part is deployed and activated, you must configure the web part to connect to a web console or *environment*. You can add more environments at any time. Use the following procedure to configure the environment for a web part.  
  
1.  On the SharePoint central administration site, in the **Site Actions** dropdown menu, click **View All Site Content**.  
  
2.  In **Lists**, click **Operations Manager Web Console Environments**.  
  
3.  Click **Add new item**.  
  
4.  In the **Name** field, enter a unique name.  
  
5.  In the **HostURI** field, enter the URI of a server hosting the Operations Manager web console. For example: **http://ServerName/OperationsManager/**  
  
6.  Click **Save**.  
  
## How to add the Operations Manager web part to a SharePoint page  

After you deploy the Operations Manager web part to a SharePoint site, you can add the web part to pages. When you add the web part, you configure it to display a specific dashboard view. For the configuration, you will need the URI for the dashboard view that you want displayed.  
  
To obtain the URI, open the web console and navigate to the desired dashboard view. The address bar will display an address such as the following:  
  
**http://localhost/OperationsManager/#/dashboard%7Btype=Microsoft.SystemCenter.Visualization.Library!Visualization.SlaDashboardViewInstanceDaily%7D**  
  
The following procedure creates a SharePoint page with the Operations Manager Dashboard Viewer web part that can only be accessed by users who have an Operations Manager user role, such as an Operator or Administrator. To configure the Operations Manager Dashboard Viewer web part so that those who are not Operations Manager users can view it, perform the following steps and then see the procedure [How to configure the web part to use shared credentials](#how-to-configure-the-web-part-to-use-shared-credentials) below.  
  
### Add the web part to a page  
  
1.  Open an Internet browser, and then navigate to the SharePoint server.  
  
2.  In the **Site Actions** dropdown menu, click **New Page**.  
  
3.  Enter a name for the page, and then click **Create**.  
  
4.  The new page opens with editing tools available. Below **Editing Tools**, click **Insert**.  
  
5.  On the **Insert** toolbar, click **Web Part**.  
  
6.  In **Categories**, click **Microsoft System Center**.  
  
7.  In **Web Parts**, click **Operations Manager Dashboard Viewer Web Part**, and then click **Add**.  
  
8.  Click the arrow in the top right of the web part, and then click **Edit web part**.  
  
9. Select the web console server in the **Dashboard Server** field, and enter the URI for the dashboard in the **Dashboard Parameters** field, and then click **OK**.  
  
10. On the menu bar, click **Page**.  
  
11. Click **Save & Close**.  
  
> [!NOTE]  
> After you correctly set up a dashboard web part in SharePoint, you might receive an error message saying "ticket has expired". This is because there is a very narrow time-out for an override ticket (by default, 5 seconds). If the time on the server running SharePoint and the Web console server differ by more than this value, the connection fails. This is a likely situation if the computers are in different domains and are using a different time source. You can increase the time-out on the SharePoint Server in the web console list, but this would make the server more vulnerable to attack. The best solution is to synchronize the time between the server running SharePoint and the web console server.  
  
## How to configure the web part to use shared credentials  

To configure the Operations Manager Dashboard Viewer web part so that those who are not Operations Manager users can view it, perform the following procedures. In the first procedure, you configure credentials by creating a Target Application ID in SharePoint. Next, you configure the web part environment.  
  
> [!NOTE]  
> Operations Manager provides two scripts in the *setup\amd64\SharePoint* directory to allow users to add and update the SharePoint web environment keys from the web config file: `add-OperationsManager-WebConsole-Environment.ps1` and `update-OperationsManager-WebConsole-Environment.ps1`. These scripts strip the encryptionAlgorithm and encryptionValidationAlgorithm for the override ticket from the web config file and add or update it in the sharepoint environment. This allows you to automate the creation and rotation of keys. Procedures for using these scripts are in this section.  
  
> [!NOTE]  
> You cannot configure shared credentials in SharePoint Foundation 2010 or 2013.  
  
### Create a target application ID  
  
1.  In SharePoint Central Administration, in the **Application Management** section, click **Manage service applications**.  
  
2.  Double-click **Secure Store Service**.  
  
3.  Click **New**.  
  
4.  On the **Application settings** page, enter a Target Application ID, a display name, and an email contact address. The Target Application ID is a unique text string that is used by the Secure Store Service application to identify this target application. The display name is displayed in the user interface. The contact can be any legitimate email address and does not have to be the identity of an administrator of the Secure Store Service application. In **Target Application Type**, select **Group**. Click **Next**.  
  
5.  On the **Add Field** page, accept the default of **Windows User Name** and **Windows Password**, and click **Next**.  
  
6.  In **Target Application Administrators**, enter a domain account, and click **OK**.  
  
7.  Click the dropdown arrow to the right of the name of the Target Application ID that you created, and click **Set Credentials**.  
  
8.  In the **Windows User Name** field, enter the user name of the account you want the web part to use. Enter the password for the account and confirm the password, and then click **OK**.  
  
### Configure the Web Part environment to use shared credentials  
  
1.  On the server hosting the Web console, in the installation folder for the Operations Manager web console, locate the Web.config file. The default installation path is C:\\Program Files\Microsoft System Center 2016\Operations Manager\WebConsole\WebHost.  
  
2.  Open Web.config in a text editor.  
  
3.  Locate the <encryption> section.  
  
4.  Locate the OverrideTicketEncryptionKey entry. In the following example, the first bold value is the encryption algorithm key and the second bold value is the encryption validation algorithm key:  
  
    Example: <key name="OverrideTicketEncryptionKey" algorithm="3DES" value="**92799B26F0BF54EE76A40CFECDB29868927D2DA4D7E57EBD**"> <validation algorithm="HMACSHA1" value="**7526BAC9FC9562835A3872A3DC12CB8B**"/>  
  
5.  Copy both keys and close Web.config.  
  
6.  On the SharePoint site, in the **Site Actions** dropdown menu, click **View All Site Content**.  
  
7.  In **Lists**, click **Operations Manager Web Console Environments** .  
  
8.  Click the web part that you want to configure, and then click **Edit Item**.  
  
9. In the **TargetApplicationID** field, enter the Target Application ID that you created in the previous procedure.  
  
10. In the **Encryption Algorithm Key** field, enter the encryption algorithm key that you copied from Web.config.  
  
11. In the **Encryption Validation Algorithm Key** field, enter the encryption validation algorithm key that you copied from Web.config.  
  
12. Click **Save**.  
  
Repeat this procedure for each Operations Manager management group.  
  
### Configure the management group for a Web Part by using a script  
  
1.  Copy the `add-OperationsManager-WebConsole-Environment.ps1` file, which is in the Operations Manager installation folder under *Setup\amd64\SharePoint*, to the SharePoint server.  
  
2.  Open Operations Manager Shell.  
  
3.  Run `add-OperationsManager-WebConsole-Environment.ps1` using the following parameters:  
  
    **-title***the name of the dashboard view*  
  
    **-webconsoleUNC** "*path to the web.config file, not including filename*"  
  
    > [!NOTE]  
    > The web.config file is found under Program Files\Microsoft System Center 2016\Operations Manager\WebConsole\WebHost on the computer running the web console.  
  
    **-targetApplicationID***the Target Application ID*  
  
## How to add additional management groups to the web part  

Adding new management groups to the Web Part enables you to display dashboards from multiple management groups.  
  
1.  On the SharePoint site, in the **Site Actions** dropdown menu, click **View All Site Content**.  
  
2.  In **Lists**, click **Operations Manager Web Consoles**.  
  
3.  Click **Add new item**.  
  
4.  In the **Name** field, enter a unique name.  
  
5.  In the **HostURI** field, enter the URI of a server hosting the Operations Manager web console. For example: **http://localhost/OperationsManager/**  
  
6.  Click **Save**.  
  
### Add additional management groups to a web part by using a script  
  
1.  Copy the `update-OperationsManager-WebConsole-Environment.ps1` file, which is in the Operations Manager installation folder under *Setup\amd64\SharePoint*, to the SharePoint server.  
  
2.  Open Operations Manager Shell.  
  
3.  Run `update-OperationsManager-WebConsole-Environment.ps1` using the following parameters:  
  
    **-title***the name of the dashboard view*  
  
    **-webconsoleUNC** "*path to the web.config file, not including filename*"  
  
    > [!NOTE]  
    > The web.config file is found under Program Files\Microsoft System Center 2016\Operations Manager\WebConsole\WebHost on the computer running the web console.  
  
    **-targetApplicationID***the Target Application ID*  
  
## How to uninstall the Operations Manager web part  

As with deploying the Operations Manager Web Part, you can uninstall the Web Part from all sites and web applications in the farm or from a specific site or web application. The Web Part can be uninstalled by using a script or retracted by using the SharePoint Central Administration site.  
  
### Uninstall the web part by using a Script  
  
1.  Copy the `install-OperationsManager-DashboardViewer.ps1` file to a location that the SharePoint Management Shell can access.  
  
2.  Open the SharePoint Management Shell and navigate to the directory where you saved the `install-OperationsManager-DashboardViewer.ps1` file.  
  
3.  In the SharePoint Management Shell, type the following command, and then press **Enter**.  
  
    **.\uninstall-OperationsManager-DashboardViewer.ps1 -solutionPath***<directory for Microsoft.EnterpriseManagement.SharePointIntegration.wsp>***-url***<optional, for uninstalling from a specific portal address or website>*  
  
    Example that uninstalls the Web Part from a specific portal address:  
  
    **.\uninstall-OperationsManager-DashboardViewer.ps1 "C:\Program Files\Microsoft System Center 2016\Operations Manager\" http://localhost:4096**  
  
    If an error occurs when you run the script, you must disable the RemoteSigned default code-signing execution policy for the SharePoint Management Shell. To allow the `install-OperationsManager-DashboardViewer.ps1` script to run, type this command, and then press **enter**:  
  
    **Set-ExecutionPolicy Unrestricted**  
  
    You will see some confirmation messages, select **Y** to confirm, and then run the script.  
  
4.  If you disabled the RemoteSigned default code-signing execution policy to run the `install-OperationsManager-DashboardViewer.ps1` script, you should re\-enable it after the script runs. Type this command, and then press **enter**:  
  
    **Set-ExecutionPolicy Restricted**  
  
    You will see some confirmation messages, select **Y** to confirm.  
  
### Retract the web part by using SharePoint Central Administration  
  
1.  Open the SharePoint Central Administration site.  
  
2.  Click **System Settings**.  
  
3.  Click **Manage Farm Solutions**.  
  
4.  Right-click the `Microsoft.EnterpriseManagement.SharePointIntegration.wsp` file, and then click **Retract**.  
  
## Next steps 

* You can use views and dashboards to visualize operational data from different perspectives to make meaningful decisions. To understand how to do this, see [Using Views and Dashboards in Operations Manager](using-views-and-dashboards-in-operations-manager.md). 
  
* To learn how you can use use reports in Operations Manager to view historical operational data, see [Using reports in Operations Manager](using-reports-in-operations-manager.md). 