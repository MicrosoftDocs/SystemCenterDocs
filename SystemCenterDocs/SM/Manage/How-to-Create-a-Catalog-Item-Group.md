---
title: How to Create a Catalog Item Group
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c11d1e8-d320-4760-a462-0e31e8124492
---
# How to Create a Catalog Item Group
Catalog item groups are lists of catalog items that are used to secure the service catalog and provide access to users, based on membership in a corresponding [!INCLUDE[smshort](../../Token/smshort_md.md)] user role. In the following procedure, you create a simple catalog item group. After you create the group, use an existing user role, or create a new user role, to provide access to catalog items that have been associated with the group.

### To create a catalog item group

1.  In the [!INCLUDE[smcons](../../Token/smcons_md.md)], select **Library**, and then click **Groups**.

2.  In the **Tasks** pane under **Groups**, click **Create Catalog Group** to open the Create Group Wizard.

3.  On the **Before You Begin** page, read the instructions, and then click **Next**.

4.  On the **General** page, complete these steps:

    1.  In the **Group name** box, type a name for the catalog group. For example, type **Access Request Offering Group**.

    2.  In the **Group description** box, type a description for the catalog group. For example, type **This group is used to consolidate and provide security to Access Request Offering catalog items**.

    3.  Next to **Management pack**, select an unsealed management pack of your choice, and then click **Next**. For example, if you previously created the Sample Management Pack, select it.

5.  On the **Included Members** page, complete these steps to select catalog items and associate them with the catalog group:

    1.  Click **Add** to open the **Select objects** dialog box, select one or more catalog items that you created previously, click **Add**, and then click **OK** to close the dialog box.

    2.  Click **Next**.

6.  Optionally, on the **Dynamic Members** page, you can select a class and specific objects, based on the criteria that you choose, to add as members of the group, and then click **Next**.

7.  Optionally, on the **Subgroups** page, you can add other groups as members of the new group that you are creating, and then click **Next**.

8.  Optionally, on the **Excluded Members** page, you can select a class and specific objects, based on criteria that you choose, to exclude as members of the group, and then click **Next**.

9. On the **Summary** page, review the information, and then click **Create**.

10. On the **Completion** page, click **Close**.



