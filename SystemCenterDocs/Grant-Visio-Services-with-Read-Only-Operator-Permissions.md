---
title: Grant Visio Services with Read-Only Operator Permissions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46d707f5-7500-4a87-8e35-ed24f8b33ae5
---
# Grant Visio Services with Read-Only Operator Permissions
In order for Visio Services to refresh the diagrams that are published and connected to [!INCLUDE[om12short](./Token/om12short_md.md)] data, the Visio Services service application must be configured with credentials that have access to the management server. This is because the Visio Services service application is executing the data provider that is responsible for returning the updated dataset from the management server.

The easiest way to configure this is to make the account that Visio Services is running as a Read\-Only Operator on the management server.

If you need to determine the account that is configured for Visio Services, use SharePoint’s Central Administration:

1.  Open the Central Administration site.

2.  In the **Security** section, click **Configure Service Accounts**.

3.  In the list of Service Accounts, select Service Application Pool – SharePoint Web Services Default.

    The account is listed in the **Select an account for this component** field.

### To grant the Visio Services account Read\-Only Operator access to the management server

1.  In the Operations console, open the Administration view.

2.  In the Administration pane, expand **Administration**, expand **Security**, and then click **User Roles**.

3.  In the User Roles pane, right\-click **Read\-Only Operator**, and then click **Properties**.

4.  In the **Operations Manager Read\-Only Operators – User Role Properties** dialog box, on the **General Properties** page, click **Add**.

5.  On the **Select User or Groups** page, enter the account that is configured for Service Application Pool, and then click **OK**.

6.  Click **Apply**, and then click **OK** to close the **Operations Manager Read\-Only Operators \-User Role Properties** dialog box.


