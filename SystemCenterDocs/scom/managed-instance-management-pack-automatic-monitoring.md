---
ms.assetid: f27d87a8-d387-4648-a0b9-848a74429538
title: Automatic monitoring template in Management Pack for Azure SQL Managed Instance
description: This article explains how to configure automatic monitoring template in Management Pack for Azure SQL Managed Instance
author: Anastas1ya
ms.author: v-ekaterinap
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Automatic Monitoring Template

Automatic monitoring template allows you to configure monitoring by discovering all managed instances in the specified Azure subscription automatically.

To configure monitoring using the automatic monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Automatic**, and select **Add Monitoring Wizard…**.

    ![Screenshot showing the Run Add Monitoring Wizard.](./media/managed-instance-management-pack/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Automatic**, and select **Next**.

    ![Screenshot showing the Select monitoring type.](./media/managed-instance-management-pack/selecting-monitoring-type.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** dropdown list, select a management pack that you want to use to store the template.

    ![Screenshot showing the Select destination management pack.](./media/managed-instance-management-pack/destination-management-pack.png)

4. At the **Azure Endpoints** step, select the **Enable checkbox if you want to change default Azure Endpoints** checkbox, and modify the default Azure endpoints, if necessary. The default endpoints for creating Azure Service Principal Name are as follows:

   - Authority URI: `https://login.windows.net`
   - Management Service URI: `https://management.azure.com`
   - Database Resource URI: `https://database.windows.net`  
   - Graph API Resource URI: `https://graph.windows.net`

   ![Screenshot showing the Configure Azure endpoints.](./media/managed-instance-management-pack/configuring-azure-endpoints.png)

5. At the **SPN Configuration** step, select any of the following options:

   - **Auto-Create SPN**

       Select this option if you want your Azure Service Principal Name to be created automatically by the Azure SQL MI MP library using the Azure REST API.
       
       Ensure that the account that you use must have either the **Owner** role (or higher), or any of the following roles:

       - **Active Directory Administrator**
       
       - **Service Administrator** or C**o-Administrator**

       For more information, see [How to - Use the portal to create an Azure AD application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal).

   - **Use Existing Run As Profile**

       Select this option if you want to use your own Azure Service Principal Name.

    ![Screenshot showing the Configure SPN.](./media/managed-instance-management-pack/spn-configuration.png)

     If you select the **Auto-Create SPN** option, the **Microsoft Azure sign-in** window will be displayed. In this window, enter your work, school, or personal Microsoft account credentials, select **Next**, and complete the form.

    ![Screenshot showing the Auto-create SPN.](./media/managed-instance-management-pack/auto-create-spn.jpg)

    Upon the successful creation of the Azure AD application, at the **Auto-Create SPN Status** step, authentication data will be displayed. Select **Next**.

    ![Screenshot showing the SPN status.](./media/managed-instance-management-pack/auto-create-spn-status.png)

    If you want to use an existing Run As Profile, at the **SPN Configuration** step, select the **Use Existing Run As Profile** option, select **Next**, and select an existing Run As Account associated with the Azure service principal name. This Run As Account will be used for authentication in Azure Cloud.

    ![Screenshot showing the Use existing Run As profile.](./media/managed-instance-management-pack/existing-run-as-profile.png)

6. At the **Subscription Permissions** step, select the Azure subscriptions that you want to monitor.

    ![Screenshot showing the Configure subscription permissions.](./media/managed-instance-management-pack/subscription-permissions.png)

7. At the **SQL Connection Settings** step, select an authentication method that you want to use to connect to your managed instances.

    Regardless of the selected option, ensure to grant required permissions to the selected monitoring account for all the managed instances. For more information, see [Security Configuration](managed-instance-management-pack-security-configuration.md).

    ![Screenshot showing the Configure SQL connection settings.](./media/managed-instance-management-pack/sql-connection-settings.png)

8. At the **Configure Instances Filtering** step, you can configure the filtering options:

   - Exclude

      Select this option to specify instances that shouldn't be discovered.

   - Include

      Select this option to specify only those instances that you want to be discovered.

    Use an asterisk to replace any symbol/symbols.

    ![Screenshot showing the Configure instance filtering.](./media/managed-instance-management-pack/instance-filtering.png)

9. At the **Summary** step, review the connection settings and select **Create**.

    ![Screenshot showing the Review connection settings.](./media/managed-instance-management-pack/review-connection-settings.png)
