---
title: How to Create an Active Directory Connector_2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1468921-5bd4-4287-aa26-7f24084a54ac
---
# How to Create an Active Directory Connector_2
You can use the following procedures in Service Manager to create,  validate, and confirm the status of an Active Directory connector to import objects from Active Directory Domain Services \(AD DS\).

### To create an Active Directory connector and to import objects from AD DS

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Active Directory Connector**.

4.  Complete these steps in the Active Directory Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that the **Enable this connector** check box is selected, and then click **Next**.

    3.  On the **Domain or organizational unit** page, select **Use the domain: \<domain name\>**. Or, select **Let me choose the domain or OU**, and then click **Browse** to choose a domain or an organizational unit \(OU\) in your environment.

    4.  In the **Credentials** area, click **New**.

    5.  In the **Run As Account** dialog box, in the **Display name** box, enter a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to read from AD DS, and then click **OK**. On the **Domain or organizational unit** page, click **Test Connection**.

        > [!NOTE]
        > Special characters \(such as the ampersand \[&\]\) in the **User Name** box are not supported.

    6.  In the **Test Connection** dialog box, make sure that **The connection to the server was successful** is displayed, and then click **OK**. On the **Domain or organizational unit** page, click **Next**.

    7.  On the **Select objects**, do the following:

        1.  Select **All computers, printers, users, and user groups** to import all items or,

        2.  Select **Select individual computers, printers, users or user groups** to import only the selected items or,

        3.  Select **Provide LDAP query filters for computers, printers, users, or user groups** if you want to create your own Lightweight Directory Access Protocol \(LDAP\) query.

        If you want new users that are added to any groups you import to be added automatically to [!INCLUDE[smshort12](../../includes/smshort12_md.md)], select **Automatically add users of AD Groups imported by this connector**, and then click **Next**.

    8.  On the **Schedule** page, in the **Synchronize** list, set the frequency and time of synchronization, and then click **Next**.

    9. On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    10. On the **Completion** page, make sure that you receive the following confirmation message:

        “Active Directory connector successfully created.”

        Then, click **Close**.

        > [!NOTE]
        > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### To validate the creation of an Active Directory connector

1.  In the **Connectors** pane, locate the Active Directory connector that you created. You might have to wait for a minute before the connector appears.

2.  In the **Connectors** pane, review the **Status** column for a status of **Finished Success**.

3.  In the **Configuration Items** pane, expand **Configuration Items**. Expand **Computers** and **All Windows Computers**, and verify that the intended computers from AD DS appear in the **All Windows Computers** pane. Expand **Printers**, expand **All Printers**, and then verify that the intended printers from AD DS appear in the **All Printers** pane.

4.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Configuration Items**. In the **Configuration Items** pane, click **Users**, and then verify that the intended users and user groups from AD DS appear in the **Users** pane.

### To confirm the status of an Active Directory connector

-   View the columns in the **Connector** pane; the columns contain information about the start time, the finish time, the status, and the percentage of imported configuration items.

![](../../media/pssymbol.png)You can use a Windows PowerShell command to create a new [!INCLUDE[smshort12](../../includes/smshort12_md.md)] Active Directory connector. For information about how to use Windows PowerShell to create a new [!INCLUDE[smshort12](../../includes/smshort12_md.md)] Active Directory connector, see [New\-SCADConnector](http://go.microsoft.com/fwlink/?LinkId=225349).


