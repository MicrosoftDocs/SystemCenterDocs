---
title: How to Register the System Center Data Warehouse to Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc5b518f-97c4-4a2d-a1b2-3ece9e7e603e
---
# How to Register the System Center Data Warehouse to Operations Manager
You can use the following procedures in Service Manager to register the System Center Data Warehouse to [!INCLUDE[om12short](./Token/om12short_md.md)] and then validate the registration.

### To register the data warehouse to [!INCLUDE[om12short](./Token/om12short_md.md)]

1.  Register System Center Data Warehouse to Service Manager Source.

2.  Wait for the MPSync job to complete.

3.  Using an account that is a member of the Service Manager and data warehouse management administrators group, log on to the computer that hosts the Service Manager console.

4.  In the Service Manager console, select **Data Warehouse**.

5.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

6.  In the **Tasks** list, click **Register data source**.

7.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

8.  On the **Data Source Type**  page, select **Operations Manager**.

9. Under **Specify a Root Management Server** area, type the following information:

    1.  For **Root Management server name**, type the server name.

    2.  For **Operational database server**, type the database server name.

    3.  For **Database name**, type the name of the database.

10. Click **Next**.

11. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the [!INCLUDE[smshort](./Token/smshort_md.md)] management server and granted Read permission on the [!INCLUDE[smshort](./Token/smshort_md.md)] database. You can specify different credentials from other [!INCLUDE[smshort](./Token/smshort_md.md)] management groups when you are registering with the data warehouse.

12. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

13. On the **Result** page, when **Data source registration complete.** appears, click **Finish**.

### To validate the [!INCLUDE[om12short](./Token/om12short_md.md)] registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Operations Manager**. You might have to refresh your view to see the new data source.


