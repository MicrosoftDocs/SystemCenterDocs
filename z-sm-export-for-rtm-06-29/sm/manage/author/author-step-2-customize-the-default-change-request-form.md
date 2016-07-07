---
title: Step 2: Customize the Default Change Request Form
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d746f1c0-8746-426b-8422-fc25fb844ceb
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
# Step 2: Customize the Default Change Request Form
The second step in the Woodgrove Bank customization scenario is to customize the default Change Request form, which is Microsoft.EnterpriseManagement.ServiceManager.ChangeManagement.Forms.ChangeRequestForm. Ken wants to rearrange some fields on the form and then add the Woodgrove Bank logo. Before Ken starts, he views the fields in the form to see how the values change according to the properties that are selected.  
  
 Next, Ken opens the **ServiceManager.ChangeManagement.Library.mp** management pack file in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)], he customizes the form, and then saves the management pack file. Later, he must import the customized management pack into the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
### To view the System.AddComputerForm form  
  
1.  In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], expand **Forms** in the **Management Pack Explorer** pane. Right\-click the **System.AddComputerForm** form, and then click **Customize** to open the form in the authoring pane.  
  
2.  In the authoring pane, ensure that the **Details** pane is visible. If it is not visible, click **View**, and then click **Details Window**.  
  
3.  Select a field on the form. Note that the properties in the **Details** pane are updated according to the class property that is bound to the field that you selected. Note the **Binding Path** entry in the **Details** pane. This entry indicates the property that the field in the form represents.  
  
### To customize the default Change Request form  
  
1.  In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **File**, point to **Open**, and then click **File**. In the **Open File** dialog box, locate the **ServiceManager.ChangeManagement.Library.mp** management pack. For example, the path to the management pack might be as follows:  
  
     D:\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2012 Authoring\\Library\\ServiceManager.ChangeManagement.Library.mp.  
  
     Select the management pack, and then click **Open**.  
  
2.  In the **Management Pack Explorer**, click the **Service Manager Change Management Library \(sealed\)** management pack, and then expand **Forms**. Right\-click the form that ends with **ChangeRequestForm**, and then click **Customize**.  
  
3.  In the **Target Management Pack** dialog box, select the **WoodGrove Automated Activity \- Add Computer To AD Group** management pack, and then click **OK**.  
  
     A new form item now appears in the **Automated Activity \- Add Computer To AD Group** management pack. The name of the new form is **Microsoft.EnterpriseManagement.ServiceManager.ChangeManagement.Forms.ChangeRequestForm \(Customized\)**.  
  
4.  Right\-click the new form item, and then click **Customize** to open it in the authoring pane.  
  
5.  In the authoring pane, customize the look of the form by dragging fields and rearranging their location on the form.  
  
6.  Click **View**, and then click **Form Customization Toolbox**.  
  
7.  Drag the **Image** icon from the **Form Customization Toolbox** to the form.  
  
8.  In the **Insert Image** dialog box, specify the path of the **Woodgrovebank.jpg** file.  
  
9. Click **File**, and then click **Save All** to save the custom management pack.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)