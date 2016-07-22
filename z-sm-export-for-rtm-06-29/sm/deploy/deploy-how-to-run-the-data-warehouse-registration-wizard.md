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
---

# How to Run the Data Warehouse Registration Wizard

You can use the following steps in System Center 2012 - Service Manager to use the Data Warehouse Registration Wizard to register with the Service Manager data warehouse.  

### To run the Data Warehouse Registration wizard  

1.  By using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.  

2.  In the Service Manager console, select **Administration**.  

3.  In the **Administration** pane, expand **Administration**.  

4.  In the **Administration** view, in the **Register with Service Manager's Data Warehouse** area, click **Register with Service Manager Data Warehouse**.  

5.  In the Data Warehouse Registration wizard, on the **Before You Begin** page, click **Next**.  

6.  On the **Data Warehouse** page, in the **Server name** box, type the *fully qualified domain name* \(FQDN\) of the computer hosting the data warehouse management server, and then click **Test Connection**. If the test is successful, click **Next**.  

7.  On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your own choosing.  

    > [!IMPORTANT]  
    >  The account that you specify will be assigned administrative credentials on the Service Manager management server, and it will be granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when you are registering with the data warehouse.  

8.  On the **Summary** page, click **Create**.  

9. On the **Completion** page, when **The data warehouse registration succeeded** appears, click **Close**.  

10. A dialog box states that the report deployment process is not finished. This is to be expected. On the **System Center Service Manager** dialog box, click **OK**.  

11. In a few minutes, after you close the Data Warehouse Registration Wizard, the **Data Warehouse** button will be added to the Service Manager console. In the Service Manager console, click the arrow at the lower right corner of the Service Manager console buttons, and then click **Show More Buttons**.  

 ![Windows PowerShell](../media/pssymbol.png) You can use a Windows&nbsp;PowerShell command to complete this task. For information about how to use Windows&nbsp;PowerShell to register Service Manager management groups with the data warehouse, see [Add\-SCDWMgmtGroup](http://go.microsoft.com/fwlink/p/?LinkId=203096).
