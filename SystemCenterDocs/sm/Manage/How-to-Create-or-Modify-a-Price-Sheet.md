---
title: How to Create or Modify a Price Sheet
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8deef26a-3835-4cd8-98e0-7bffeb6ea7eb
---
# How to Create or Modify a Price Sheet

>Applies To: System Center 2016 Technical Preview - Service Manager

Price sheets in Service Manager allow you to define price policies on existing private cloud objects that are discovered from the Operations Manager CI connector. You can associate one or more private clouds to a price sheet. After association, price information contained in the price sheet is shown in OLAP cubes and in a sample Excel report. You can use the OLAP cube data to create your own customized reports using various reporting solutions such as SQL Server Reporting Services, SQL Server Analysis Services tools, and Microsoft Excel. Additionally, you can modify the sample Excel report for your organization’s needs.

Although you can create multiple price sheets without publishing them, you must publish a price sheet before you can associate cloud objects to the price sheet.

### To create a price sheet

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Chargeback**, expand **Infrastructure**, expand **Price Sheets**, and then select **All Price Sheets**.

3.  In the **Tasks** pane under **All Price Sheets**, click **Create Price Sheet**.

4.  On the **General** tab, complete these steps:

    1.  In the **Name** box, type a title for the price sheet. For example, type **Gold Price Sheet**.

    2.  Optionally, in the **Description** box, you can type a description of the price sheet. For example, type **The gold price sheet describes our highest level of service available and is more costly than others offered.**

    3.  You can optionally publish the price sheet using the **Publish** task in the Tasks list of the form. Publishing the price list enables you to assign cloud objects to the price list.

5.  On the **Price** tab, complete these steps:

    1.  In the **VM Base Price per day** box, type the daily base price value of the virtual machine. For example, type **22.55**.

    2.  In the **Cloud Membership Price per day** box, type the base price value for membership in the cloud. For example, type **10.20**.

    3.  In the **VM CPU Price per Core/day** box, type the price value of the CPU core in the virtual machine that is included in the virtual machine. For example, type **1.20**.

    4.  In the **VM Memory Price per GB/day** box, type the price value of each GB of memory in the virtual machine that is included in the associated cloud. For example, type **.30**.

    5.  In the **VM Storage Price per GB/day** box, type the base value of each GB of storage space in the virtual machine that is included in the associated cloud. For example, type **.10**.

    6.  In the **Highly Available VM Price per day** box, type the price value for each virtual machine that is highly available. For example, type **1.10**.

    7.  In the **Static IP Price per day** box, type the price value for each static IP address for virtual machines. For example, type **.05**.

    8.  In the **Expanding VHD Price per day** box, type the price value expanding VHDs. For example, type **.55**.

    9. You can optionally publish the price sheet using the **Publish** task in the Tasks list of the form. Publishing the price list enables you to assign cloud objects to the price list.

6.  If you have published the price sheet, you can optionally assign clouds to the price list using the Assigned Clouds **Price** tab by completing these steps:

    1.  Click **Add**, to open the **Select objects** dialog box.

    2.  In the list of **Private Cloud** objects, select one or more private cloud objects and then click **Add** to add them to the **Selected objects** list.

    3.  Click **OK** to close the **Select objects** dialog box and assign the cloud objects to the price sheet.

    4.  Click **OK** to close the price sheet form.

### To modify a price sheet

1.  In the Service Manager console, select **Administration**.

2.  In the **Administration** pane, expand **Price Sheets**, and then select a view that contains a price sheet that you want to modify.

3.  In the list of price sheets, select the one you want to modify and then in the **Tasks** pane under **Tasks**, click **Edit**.

4.  On the **General** tab, complete any of the following steps that you want to in order to update the price sheet:

    1.  In the **Name** box, update the title for the price sheet. For example, type **Silver Price Sheet**.

    2.  In the **Description** box, you can update the description of the price sheet. For example, type **The sliver price sheet describes our highest level of service available and is more costly than others offered.**

    3.  You can optionally publish the price sheet using the **Publish** task in the Tasks list of the form. Publishing the price list enables you to assign cloud objects to the price list.

5.  On the **Price** tab, complete any of the following steps that you want to in order to update the price sheet:

    1.  In the **VM Base Price per day** box, update the daily base price value of the virtual machine. For example, type **11.44**

    2.  In the **Cloud Membership Price per day** box, update the base price value for membership in the cloud. For example, type **9.10**

    3.  In the **VM CPU Price per Core/day** box, update the price value of the CPU core in the virtual machine. For example, type **0.60**

    4.  In the **VM Memory Price per GB/day** box, update the price value of each GB of memory in the virtual machine. For example, type **.15**

    5.  In the **VM Storage Price per GB/day** box, update the base value of each GB of storage space in the virtual machine. For example, type **.05**

    6.  In the **Highly Available VM Price per day** box, update the price value for each virtual machine that is highly available. For example, type **.90**.

    7.  In the **Static IP Price per day** box, update the price value for each static IP address for virtual machines. For example, type **.03**.

    8.  In the **Expanding VHD Price per day** box, update the price value for expanding VHDs. For example, type **.80**.

    9. You can optionally publish the price sheet using the **Publish** task in the Tasks list of the form. Publishing the price list enables you to assign cloud objects to the price list.

6.  If you have published the price list, you can optionally assign or remove clouds to the price list using the Assigned Clouds **Price** tab by completing these steps:

    1.  Click **Add**, to open the **Select objects** dialog box.

    2.  If you want to add private cloud objects, in the list of **Private Cloud** objects, select one or more private cloud objects and then click **Add** to add them to the **Selected objects** list.

    3.  Click **OK** to close the **Select objects** dialog box and assign the cloud objects to the price sheet.

    4.  If you want to remove private cloud objects, in the list of **Private Cloud** objects, select one or more private cloud objects and then click **Remove**.

    5.  Click **OK** to close the price sheet form.




