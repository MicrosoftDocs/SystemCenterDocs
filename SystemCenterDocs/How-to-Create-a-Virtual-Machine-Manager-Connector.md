---
title: How to Create a Virtual Machine Manager Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b407c1e7-0d9b-44b6-bcfe-8ef701054d75
robots: noindex,nofollow
---
# How to Create a Virtual Machine Manager Connector
Use the following procedures in [!INCLUDE[smlong12](Token/smlong12_md.md)] to create a System Center Virtual Machine Manager connector and validate the creation of the connector.

### To create a System Center Virtual Machine Manager connector

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, under **Connectors**, click **Create Connector**, and then click **Virtual Machine Manager connector**.

4.  Complete these steps to complete the Virtual Machine Manager Connector Wizard:

    1.  On the **Before You Begin** page, click **Next**.

    2.  On the **General** page, in the **Name** box, type a name for the new connector. Make sure that **Enable this connector** is selected, and then click **Next**.

    3.  On the **Connection** page, in the **Server Information** area, type the same of the computer hosting Virtual Machine Manager \(VMM\).

    4.  On the **Connection** page, in the **Credentials** area, either select an existing account or click **New**, and then do the following:

        1.  In the **Run As Account** dialog box, in the **Display name** box, type a name for the Run As account. In the **Account** list, select **Windows Account**. Enter the credentials for an account that has rights to connect [!INCLUDE[vmm12short](Token/vmm12short_md.md)], and then click **OK**. On the **Connection** page, click **Test Connection**.

            > [!NOTE]
            > Special characters \(such as the ampersand \[&\]\) in the **User Name** box are not supported.

        2.  In the **Test Connection** dialog box, make sure that **The connection to the server was successful** appears, and then click **OK**. On the **Connection** page, click **Next**.

    5.  On the **Summary** page, make sure that the settings are correct, and then click **Create**.

    6.  On the **Completion** page, make sure that you receive a “Virtual Machine Manager connector successfully created” message, and then click **Close**.

### To validate the creation of a System Center Virtual Machine Manager connector

1.  In the **Connectors** pane, locate the System Center Virtual Machine Manager connector that you created.

2.  Review the **Status** column for a status of **Running**.

    > [!NOTE]
    > Allow sufficient time for the import process to finish if you are importing a large number of virtual machines or clouds.

3.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Configuration Items**.

4.  In the **Tasks** pane, click **Create Folder**.

5.  In the Create New Folder Wizard, do the following:

    1.  In the **Folder name** box, type a name for the folder. For example, type **Test**.

    2.  In the **Management pack** area, make sure that an unsealed management pack of your choice is selected, and then click **OK**. For example, select **Service Catalog Generic Incident Request**.

6.  In the **Configuration Items** pane, click the folder you just created. For example, click **Test**.

7.  In the **Tasks** pane, click **Create View**.

8.  In the Create View Wizard, do the following:

    1.  On the **General** page, in the **Name** area, type a name for this view. For example, type **VMMTemplates**.

    2.  In the **Management pack** area, make sure that an unsealed management pack of your choice is selected. For example, select **Service Catalog Generic Incident Request**.

    3.  In the navigation pane of the wizard, click **Criteria**.

    4.  In the **Advanced Search** area, click **Browse**.

    5.  In the drop\-down list \(located to the right of the **Type to filter** box\), select **All basic classes**.

    6.  In the **Type to filter** box, type **virtual machine template**, click **Virtual Machine Template**, click **OK**, and then click **OK** to save and close the form.

9. In the **Configuration Items** pane, expand the folder you created, and then click the view you created. For example, expand **Test**, and then click **VMMTemplates**

10. In the **VMMTemplates** pane, you will see the Virtual Machine Manager templates that have been created.


