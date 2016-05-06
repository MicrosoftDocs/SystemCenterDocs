---
title: How to Register the System Center Data Warehouse to a Service Manager Source
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30b83b58-d257-43ae-997b-2514231f5059
---
# How to Register the System Center Data Warehouse to a Service Manager Source
You can use the following procedures in Service Manager to register the System Center Data Warehouse with a Service Manager management group and then validate the registration. This makes it possible to host multiple [!INCLUDE[smshort](./Token/smshort_md.md)] management groups in a single data warehouse.

### To register the data warehouse with another Service Manager management group

1.  By using an account that is a member of the [!INCLUDE[smshort](./Token/smshort_md.md)] and data warehouse management administrators group, log on to the computer that hosts the [!INCLUDE[smcons](./Token/smcons_md.md)].

2.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], select **Data Warehouse**.

3.  In the **Administration** pane, expand **Data Warehouse**, and then select **Data Sources**.

4.  In the **Tasks** list, click **Register data source**.

5.  In the Register Data Source Wizard, on the **Before You Begin** page, click **Next**.

6.  On the **Data Source Type**  page, select **Service Manager**.

7.  Under **Specify a Service Manager Server**, type the following information:

    1.  For **Service Manager server name**, type the server name.

8.  Click **Next**.

9. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and then click **Next**, or you can enter credentials from a user or group of your choice.

    > [!IMPORTANT]
    > The account that you specify will be assigned administrative credentials on the [!INCLUDE[smshort](./Token/smshort_md.md)] management server and granted Read permission on the [!INCLUDE[smshort](./Token/smshort_md.md)] database. You can specify different credentials from other [!INCLUDE[smshort](./Token/smshort_md.md)] management groups when registering with the data warehouse.

10. On the **Summary** page, you can review the settings that you have chosen. Click **Finish**.

11. On the **Result** page, when **Data source registration complete.** appears, click **Finish**.

### To validate the  [!INCLUDE[smshort](./Token/smshort_md.md)] registration process

-   In the **Data Sources** view, the new data source appears in the list of data sources, with the data source type of **Service Manager**. You might have to refresh your view to see the new data source.



