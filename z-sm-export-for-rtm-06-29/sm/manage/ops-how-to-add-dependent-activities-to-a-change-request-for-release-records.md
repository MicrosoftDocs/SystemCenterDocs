---
title: How to Add Dependent Activities to a Change Request for Release Records
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2fc25f5-8af2-47ca-b8e9-aba8029bdccc


















---
# How to Add Dependent Activities to a Change Request for Release Records
In System Center 2012 - Service Manager, you can use the following procedures to add a dependent activity to an existing change request, which is used as part of the release management process. Although you can add dependent activities to work items, such as release records and service requests, the primary purpose of a dependent activity is for use as a mechanism to associate a change request with a release record. Specifically, a manual activity in a release record is linked to the dependent activity in a change request. When it is completed, the dependent activity indicates that the release management process is complete for the change request.  
  
 If you intend to use release management as part of the standard processes in your organization, consider adding dependent activities to change request templates. For more information about creating change request templates, see [How to Create Change Request Templates](http://go.microsoft.com/fwlink/p/?LinkId=229752).  
  
### To add a dependent activity to a change request  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Change Management**, and then click **All Change Requests**.  
  
3.  Double\-click the change request to which you want to add a dependent activity. For example, double\-click **Apply Exchange Server 2010 Service Pack 1**.  
  
4.  Click the **Activities** tab, and then click **Add**. In the **Select Template** dialog box, click **Default Dependent Activity**, and then click **OK**.  
  
5.  In the **Title** box, type a name that describes the dependent activity. For example, type **Exchange Server 2010 SP1 \- Deploy, Test, and Verify** .  
  
6.  In the **Description** box, type a description of the dependent activity. For example, type **Verify that the service pack is deployed, tested, and verified successful**.  
  
7.  Under **Owner**, click the ellipsis button \(...\).  
  
8.  In the **Select User** dialog box, select the name of the person who has overall responsibility for the dependent activity, and then click **OK**.  
  
9. Under **Assigned To**, click the ellipsis button \(...\).  
  
10. In the **Select User** dialog box, select the name of the person who will perform the dependent activity, and then click **OK**. For example, select **Aaron Lee**.  
  
11. As an option, specify scheduling information on the **Scheduling** tab.  
  
12. Click **OK** to update the changes to the dependent activity.  
  
13. Click **OK** to update the change request and to close the form.  
  
### To validate that the dependent activity was added  
  
-   Reopen the change request, and then click the **Activities** tab to view the dependent activity that you added.  
  
## See Also  
 [How to Create Change Request Templates](http://go.microsoft.com/fwlink/p/?LinkId=229752)   
 [How to Choose Changes to Deploy](../../../sm/manage/operate/How-to-Choose-Changes-to-Deploy.md)
