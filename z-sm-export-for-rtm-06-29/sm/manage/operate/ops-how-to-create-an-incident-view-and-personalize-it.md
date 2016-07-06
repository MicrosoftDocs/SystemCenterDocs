---
title: How to Create an Incident View and Personalize It
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd7fbb82-98d5-433e-91df-7c721d03608b
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Create an Incident View and Personalize It
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you can use the following procedures to create and personalize an incident view and then validate it.  
  
 Views let you group incidents that share certain criteria. For example, the following procedure helps you create a view that lists all the incidents in which the classification has been set to **E\-mail Problems** or to some other classification. When you create a new view, it is saved and becomes available for later use.  
  
 You can also personalize a view. However, when you personalize changes to a view, those changes are not saved. For example, you can personalize the **All Incidents** view, but if you change column widths, column sorting, or grouping or if you remove columns, the next time you return to the view it displays information in the same manner as it did before you personalized it.  
  
### To create an incident view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**.  
  
3.  In the **Tasks** pane, click **Create View**.  
  
4.  In the **General** section of the **Create View** dialog box, type a name for the view in the **Name** box. For example, type **E\-mail Incidents**.  
  
5.  In the **Description** box, type a description. For example, type **All incidents in which the classification is E\-Mail Problem**.  
  
6.  Click **Criteria**.  
  
7.  Next to the **Search for objects of a specific class** list, click **Browse**.  
  
8.  In the **Select a Class** list, under **View**, select **Combination classes**, select **Incident \(Typical\)**, and then click **OK**.  
  
9. In the **Related classes** box, ensure that **Incident** is selected. In the **Available properties** list, select **Classification Category**, and then click **Add**. You might need to scroll to see the **Add** button.  
  
10. At the end of the **Criteria** section, in the **Criteria** definition area, select **E\-mail problems**. When the criterion is complete, it resembles **\[Incident\] Classification Category equals E\-Mail Problems**.  
  
11. Click **Display**, and in the **Columns to display** list, select **Status**, **Classification Category**, and **Description**. Next, under **Assigned To User**, select **Display Name**. Then, click **OK**.  
  
### To personalize an incident view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then select an incident view. For example, select **All Incidents**.  
  
3.  Right\-click any view column heading to resize the columns, to remove items from the results, or to change column sorting and grouping. Repeat this step until you are satisfied with the results.  
  
### To validate the incident view creation  
  
-   In the **Work Items** pane, ensure that an **E\-Mail Incidents** view exists under **Incident Management**. Ensure that the view displays all the incidents in the **E\-Mail Problems** category.  
  
    > [!NOTE]  
    >  It might take a few seconds for the new incident view to appear.  
  
## See Also  
 [Managing Incidents](../../../sm/manage/operate/Managing-Incidents.md)