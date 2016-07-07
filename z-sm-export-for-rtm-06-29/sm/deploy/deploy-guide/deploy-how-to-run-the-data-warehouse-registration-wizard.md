---
title: How to Run the Data Warehouse Registration Wizard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4b1d83f-6a4b-42ab-851b-498f1ff89db2
translation.priority.ht: 
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
# How to Run the Data Warehouse Registration Wizard
You can use the following steps in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to use the Data Warehouse Registration Wizard to register with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse.  
  
### To run the Data Warehouse Registration wizard  
  
1.  By using an account that is a member of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and data warehouse management administrators group, log on to the computer that hosts the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
2.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], select **Administration**.  
  
3.  In the **Administration** pane, expand **Administration**.  
  
4.  In the **Administration** view, in the **Register with Service Manager’s Data Warehouse** area, click **Register with Service Manager Data Warehouse**.  
  
5.  In the Data Warehouse Registration wizard, on the **Before You Begin** page, click **Next**.  
  
6.  On the **Data Warehouse** page, in the **Server name** box, type the *fully qualified domain name* \(FQDN\) of the computer hosting the data warehouse management server, and then click **Test Connection**. If the test is successful, click **Next**.  
  
7.  On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your own choosing.  
  
    > [!IMPORTANT]  
    >  The account that you specify will be assigned administrative credentials on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, and it will be granted Read permission on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database. You can specify different credentials from other [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management groups when you are registering with the data warehouse.  
  
8.  On the **Summary** page, click **Create**.  
  
9. On the **Completion** page, when **The data warehouse registration succeeded** appears, click **Close**.  
  
10. A dialog box states that the report deployment process is not finished. This is to be expected. On the **System Center Service Manager** dialog box, click **OK**.  
  
11. In a few minutes, after you close the Data Warehouse Registration Wizard, the **Data Warehouse** button will be added to the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click the arrow at the lower right corner of the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] buttons, and then click **Show More Buttons**.  
  
 ![Windows PowerShell](../../../sm/deploy/deploy-guide/media/PSSymbol.gif "PSSymbol") You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to register [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management groups with the data warehouse, see [Add\-SCDWMgmtGroup](http://go.microsoft.com/fwlink/p/?LinkId=203096).