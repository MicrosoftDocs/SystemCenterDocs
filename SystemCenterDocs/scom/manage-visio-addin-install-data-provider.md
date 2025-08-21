---
title: Install and Configure the Visio Services Data Provider
description: This article describes how to install and configure the Visio Services Data Provider in a SharePoint farm.
author: jyothisuri
ms.author: jsuri
ms.date: 04/17/2025
ms.custom: UpdateFrequency2, intro-installation
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
ms.assetid: 8b1c21ab-529b-4c04-9384-717a503f3df7
---

# Install and configure the Visio Services Data Provider



The Visio Services Data Provider for System Center - Operations Manager uses SharePoint's Visio Services to enable Visio diagrams to show live health state from Operations Manager in SharePoint.   

The Visio Services Data Provider for Operations Manager has the following prerequisites:  

-   System Center - Operations Manager, Operations or Authoring console  

-   SharePoint 2010, 2013, or 2016 Enterprise  

-   Microsoft .NET Framework 3.5 SP1.  For Windows 2012 and 2012 R2, see [Enable .NET Framework 3.5 by using the Add Roles and Features Wizard](/previous-versions/windows/it-pro/windows-8.1-and-8/dn482071(v=win.10)).

> [!NOTE]  
> You must install SharePoint Server 2010, 2013, or 2016 in a farm environment versus standalone (on a single server with a built-in database by using the default settings) so that Visio Services can be configured to run as a domain account with Operations Manager access. For more information about installing SharePoint Server on a single server farm, see [Install SharePoint Server 2013 on a single server with SQL Server)](/SharePoint/install/install-sharepoint-server-2016-on-one-server). For more information about installing SharePoint Server 2013 on a multiple server farm, see [Install SharePoint 2013 across multiple servers for a three-tier farm](/SharePoint/install/install-sharepoint-server-2016-across-multiple-servers), and for SharePoint 2016, see [Install SharePoint 2016 across multiple servers](/SharePoint/install/install-sharepoint-server-2016-across-multiple-servers).  

## Install the Visio Services data provider  

To install the Visio Services data provider, follow these steps:

1.  In Windows Explorer, navigate to the directory where you downloaded the Add-in and then double-click **the OpsMgrDataModuleSetup.msi**.  

2.  Read the license agreement, select **I Agree**, and select **Next**.  

3.  Specify the installation location, and select **Next**.  

    By default, files are extracted to the C:\Program Files\ directory. You can change this to any location.  

    > [!NOTE]  
    > The .msi program doesn't install or deploy the data provider to the SharePoint servers in the server farm. This program simply extracts the SharePoint deployment package to a location specified by the SharePoint administrator.  

4.  Open the SharePoint Management Shell as an administrator.  

5.  Run the following command:  

    ```  
    .\InstallOpsMgrDataModule.ps1  
    ```  

    > [!NOTE]  
    > The SharePoint Administration service must be running prior to running `.\InstallOpsMgrDataModule.ps1`  

    The `InstallOpsMgrDataModule` cmdlet installs the deployment package to the solution store for the server farm and then deploys the data module to each of the SharePoint servers in the server farm.  

6.  After the cmdlet has completed, you can verify that the package was successfully deployed by running the `get-spsolution` cmdlet. You should see "True" in the Deployed column next to the opsmgrdatamodule.wsp entry.  

7.  Start SharePoint Central Administration to verify that the data provider is listed as a Trusted Data Provider for Visio Services.  

## Grant Visio Services with Read-Only Operator permissions

In order for Visio Services to refresh the diagrams that are published and connected to Operations Manager data, the Visio Services service application must be configured with credentials that have access to the management server. This is because the Visio Services service application is executing the data provider that is responsible for returning the updated dataset from the management server.  

The easiest way to configure this is to make the account that Visio Services is running as a Read-Only Operator on the management server.  

If you need to determine the account that is configured for Visio Services, use SharePoint's Central Administration.

To use SharePoint's Central Administration, follow these steps:

1.  Open the Central Administration site.  

2.  In the **Security** section, select **Configure Service Accounts**.  

3.  In the list of Service Accounts, select Service Application Pool - SharePoint Web Services Default.  

    The account is listed in the **Select an account for this component** field.  

## Grant the Visio Services account Read-Only Operator access to the management server  

To grant access to the management server, follow these steps:

1.  In the Operations console, select **Administration**.  

2.  In the Administration pane, expand **Administration**, expand **Security**, and select **User Roles**.  

3.  In the User Roles pane, right-click **Read-Only Operator**, and select **Properties**.  

4.  In the **Operations Manager Read-Only Operators - User Role Properties** dialog, on the **General Properties** page, select **Add**.  

5.  On the **Select User or Groups** page, enter the account that is configured for Service Application Pool, and select **OK**.  

6.  Select **Apply**, and select **OK** to close the **Operations Manager Read-Only Operators - User Role Properties** dialog.
