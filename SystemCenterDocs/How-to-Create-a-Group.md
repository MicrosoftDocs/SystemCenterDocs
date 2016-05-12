---
title: How to Create a Group
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0410edc-b59a-48dd-b68e-7ee969b83894
robots: noindex,nofollow
---
# How to Create a Group
Use the following procedures in [!INCLUDE[smlong12](Token/smlong12_md.md)] to create a new group \(such as the **Exchange Servers** group\) that includes the servers in your environment that are running Microsoft Exchange Server.

> [!NOTE]
> We recommend that you create a Configuration Manager 2007 connector before you run this procedure. For more information, see [Importing Data from Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkID=232312).

### To create a new group

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Library**.

2.  In the **Library** pane, expand **Library**, and then click **Groups**.

3.  In the **Tasks** pane, under **Groups**, click **Create Group**. The Create Group Wizard starts.

4.  On the **Before You Begin** page, click **Next**.

5.  On the **General** page, do the following:

    1.  Provide a name for the group, such as **Exchange Servers**.

    2.  In the **Description** text box, type a description for the group. For example, type **All Exchange servers that require an update.**

    3.  Under **Management pack**, make sure that an unsealed management pack is selected. For example, select **Service Catalog Generic Incident Request**. Then, click **Next**.

6.  On the **Included Members** page, click **Add**.

7.  In the **Select Objects** dialog box, in the **Filter by class** list, select a class, such as **Windows Computer**.

8.  In the **Search by name** box, type the search criteria that you want to use to locate an object, and then click the filter \(magnifying glass\) button.

9. Select one or more items in the **Available Objects** list, and then click **Add**. For example, select all the Exchange servers in your organization.

10. Verify that the objects that you selected in the **Available Objects** list appear in the **Selected objects** list, and then click **OK**.

11. On the **Included Members** page, click **Next**.

12. Optionally, on the **Dynamic members** page, click the ellipsis \(…\) button to specify a type, such as **Windows Computer**, to build the dynamic members. Choose any property you want to build your criteria. For example, after you specify the **Windows Computer** type, select the **Principal Name** property, and then click **Add**. In the related text box, enter **woodgrove** so that all the computers whose principal name contains this text are included, and then click **Next**.

13. Optionally, on the **Subgroups** page, click **Add**, and then select the specific groups that you want as subgroups of this group. If any group that you want to select as a subgroup is from an unsealed management pack, that subgroup must be from the same management pack as the group that you are creating. Click **OK**, and then click **Next**.

14. Optionally, on the **Excluded Members** page, click **Add**, and then select the specific configuration items that you want to exclude from this group. Click **OK**, and then click **Next**.

15. On the **Summary** page, confirm the group settings that you made, and then click **Create**.

16. On the **Completion** page, make sure that you receive the following confirmation message, and then click **Close**:

    “The new group was created successfully.”

### To validate the creating of a new group

-   Make sure that **Exchange Servers** appears in the **Groups** pane. If necessary, press the F5 key to refresh the [!INCLUDE[smcons](Token/smcons_md.md)] view.

    In the **Tasks** pane, under the name of the group, click **View Group Members** to make sure that the Exchange servers appear in the **Group Members** window.

![](Image/PSSymbol.gif)You can use a Windows PowerShell command to retrieve groups from Operations Manager and from Service Manager. For more information, see [Get\-SCSMGroup](http://go.microsoft.com/fwlink/p/?LinkID=225402).


