---
title: How to Import Configuration Items from a CSV File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b4d69a52-baed-4c59-8052-6b012ce25632
---
# How to Import Configuration Items from a CSV File
Before you can import data from a comma\-separated value \(CSV\) file, you have to create two files: a data file and a format file. For more information about how to create these files, see [About Importing Data From Comma\-Separated Files into Service Manager](About-Importing-Data-from-Comma-Separated-Files-into-Service-Manager.md). You can use the following procedure to import the Newcomputers.csv file by using the Newcomputers.xml format file.

### To import configuration items from a CSV file

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Tasks** pane, click **Import from CSV file**.

4.  In the **Import Instances from CSV File** dialog box, do the following:

    1.  Next to the **XML format file** box, click **Browse**, and then select the format file. For example, select **Newcomputers.xml**, and then click **Open**.

    2.  Next to the **Data file** box, click **Browse**, and then select the data file. For example, select **Newcomputers.csv**, and then click **Open**.

5.  In the **Import Instances from CSV File** dialog box, click **Import**.

6.  In the **Import Instances from CSV File** dialog box, verify that the numbers next to **Items saved**, **Instances created in memory**, and **Instances committed to database** are equal to the number of rows in the data file, and then click **Close**.

![](../Image/PSSymbol.gif)You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to import configuration items from a CSV file, see [Import\-SCSMInstance](http://go.microsoft.com/fwlink/p/?LinkId=225348).

### To validate the import of configuration items from a CSV file

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.

3.  In the **All Windows Computers** pane, verify that the computers in the CSV file are listed.

