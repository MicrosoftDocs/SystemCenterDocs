---
ms.assetid: f27d87a8-d387-4648-a0b9-848a74429538
title: Automatic monitoring template in Management Pack for Azure SQL Managed Instance
description: This article explains how to configure automatic monitoring template in Management Pack for Azure SQL Managed Instance
author: TDzakhov
manager: vvithal
ms.author: jsuri
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Automatic Monitoring Template

Automatic monitoring template allows you to configure monitoring by discovering all managed instances in the specified Azure subscription automatically.

To configure monitoring using the automatic monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Automatic**, and select **Add Monitoring Wizard…**.

    ![Run Add Monitoring Wizard](./media/managed-instance-management-pack/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Automatic**, and click **Next**.

    ![Select monitoring type](./media/managed-instance-management-pack/selecting-monitoring-type.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** drop-down list, select a management pack that you want to use to store the template.

    ![Select destination management pack](./media/managed-instance-management-pack/destination-management-pack.png)

4. At the **Azure Endpoints** step, select the **Enable checkbox if you want to change default Azure Endpoints** checkbox, and modify the default Azure endpoints if required. The default endpoints for creating Azure Service Principal Name are as follows:

   - Authority URI: <https://login.windows.net>
   - Management Service URI: <https://management.azure.com>
   - Database Resource URI: `https://database.windows.net`  
   - Graph API Resource URI: <https://graph.windows.net>

   ![Configure Azure endpoints](./media/managed-instance-management-pack/configuring-azure-endpoints.png)

5. At the **SPN Configuration** step, select any of the following options:

   - **Auto-Create SPN**

       Select this option If you want your Azure Service Principal Name to be created automatically by the Azure SQL MI MP library using the Azure REST API. 
       
       Mind that the account that you use must have either the **Owner** role (or higher), or any of the following roles:

       - **Active Directory Administrator**
       
       - **Service Administrator** or C**o-Administrator**

       For more information, see [How to - Use the portal to create an Azure AD application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal).

   - **Use Existing Run As Profile**

       Select this option if you want to use your own Azure Service Principal Name.

    ![Configure SPN](./media/managed-instance-management-pack/spn-configuration.png)

     If you select the **Auto-Create SPN** option, the **Microsoft Azure sign-in** window will be displayed. In this window, enter your work, school, or personal Microsoft account credentials, click **Next**, and complete the form.

    ![Auto-create SPN](./media/managed-instance-management-pack/auto-create-spn.jpg)

    Upon successful creation of the Azure AD application, at the **Auto-Create SPN Status** step, authentication data will be displayed. Click **Next**.

    ![SPN status](./media/managed-instance-management-pack/auto-create-spn-status.png)

    If you want to use an existing Run As Profile, at the **SPN Configuration** step, select the **Use Existing Run As Profile** option, click **Next**, and select an existing Run As Account associated with the Azure service principal name. This Run As Account will be used for authentication in Azure Cloud.

    ![Use existing Run As profile](./media/managed-instance-management-pack/existing-run-as-profile.png)

6. At the **Subscription Permissions** step, select Azure subscriptions that you want to monitor.

    ![Configure subscription permissions](./media/managed-instance-management-pack/subscription-permissions.png)

7. At the **SQL Connection Settings** step, select an authentication method that you want to use to connect to your managed instances. 

    Regardless of the selected option, make sure to grant required permissions to the selected monitoring account for all managed instances. For more information, see [Security Configuration](managed-instance-management-pack-security-configuration.md).

    ![Configure SQL connection settings](./media/managed-instance-management-pack/sql-connection-settings.png)

8. At the **Configure Instances Filtering** step, you can configure filtering options:

   - Exclude

      Select this option to specify instances that should not be discovered.

   - Include

      Select this option to specify only those instances that you want to be discovered.

    Use an asterisk to replace any symbol/symbols.

    ![Configure instance filtering](./media/managed-instance-management-pack/instance-filtering.png)

9. At the **Summary** step, review connection settings and click **Create**.

    ![Review connection settings](./media/managed-instance-management-pack/review-connection-settings.png)
