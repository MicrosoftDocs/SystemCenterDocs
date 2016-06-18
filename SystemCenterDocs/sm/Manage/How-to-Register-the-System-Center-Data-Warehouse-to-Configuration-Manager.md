---
title: How to Register the System Center Data Warehouse to Configuration Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b53c170-36ff-4d31-b6a2-2095177cd71c
---
# How to Register the System Center Data Warehouse to Configuration Manager
You can use the following steps in Service Manager to register Configuration Manager with the System Center Data Warehouse and then validate the registration.

### To register Configuration Manager with the data warehouse

1.  By using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.

2.  In the Service Manager console, select **Data Warehouse**.

3.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

4.  In the **Tasks** list, click **Register data source**.

5.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

6.  On the **Data Source Type**  page, select **Configuration Manager**.

7.  Under **Specify a Central Site Server**, type the following information:

    1.  For **Central Site server name**, type the site server name.

    2.  For **Database name**, type the name of the database.

8.  Click **Next**.

9. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when you are registering with the data warehouse.

10. On the **Data Selection** page, choose the domains to extract, and then click **Next**. For example, select **System Center Configuration Manager Connector Configuration** and **System Center Configuration Manager Power Management Connector**.

11. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

12. On the **Result** page, when **Data source registration complete** appears, click **Finish**.

### To validate the Configuration Manager registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Configuration Manager**. You might have to refresh your view to see the new data source.


