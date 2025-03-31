---
title: Use a CSV file to import data
description: Describes how you can use a CSV file to import data into Service Manager.
ms.topic: article
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service: system-center
keywords:
ms.date: 03/31/2025
ms.subservice: service-manager
ms.assetid: d968e937-59c1-4a9a-8786-8ff0bbf62db0
ms.custom: UpdateFrequency3, engagement-fy24
---

# Use a CSV file to import data into Service Manager



This article provides an overview and procedures for importing data and configuration items into Service Manager by using comma-separated value (CSV) files.

## Import data from comma-separated files

Configuration items contained in a comma-separated value (.csv) file can be imported into the Service Manager database by using the Import from CSV File feature. This feature lets you bulk-import instances of any class type or projection type that is defined in the Service Manager database. You can use this feature to:

- Create configuration item or work item instances from data stored in a tabular format.

- Bulk-edit existing database instances.

- Populate the Service Manager database by using data exported from an external database.

- Circumvent data entry through forms when many class instances must be created at the same time.

> [!NOTE]
> Importing many complex items-for example, 5,000 computer projections-could take an hour or more. During this time, Service Manager continues to function.

Two files are required to import a set of instances by using the Import from CSV File feature:

1. A data file that consists of a series of comma-delimited object instances. The data file must end with the .csv file name extension.

2. A format file that specifies the class type or projection type of the instances present in the data file. Every instance in the data file is assumed to be of this kind. The format file also specifies (1) the subset of properties and, for projections, specifies components. They're being imported for the indicated type, and (2) the order in which those properties appear as columns in the associated data file. The format file must have the same file name as the csv file that it describes, and it must end with the .xml file name extension.

## Create the data file

For example, you receive a spreadsheet that contains information about computers that you want to import into the Service Manager database. The following is a sample of the first 10 computers in the spreadsheet.

|Computer Name|IP Address|Domain Name|
|-----------------|--------------|---------------|
|WG-Det-1|172.30.14.21|DETROIT|
|WG-Det-2|172.30.14.22|DETROIT|
|WG-Det-3|172.30.14.23|DETROIT|
|WG-Dal-1|172.30.14.24|DALLAS|
|WG-Dal-2|172.30.14.25|DALLAS|
|WG-Chi-1|172.30.14.26|CHICAGO|
|WG-Chi-2|172.30.14.27|CHICAGO|
|WG-Chi-3|172.30.14.28|CHICAGO|
|WG-Chi-4|172.30.14.29|CHICAGO|
|WG-Chi-5|172.30.14.30|CHICAGO|

The first step is to convert the data in the table into a .csv file format. In the .csv file, you make the assumption that the first row is data, and not a header. Therefore, you remove the header line from the spreadsheet and save the results as **newcomputers.csv** as in the following example.

```
WG-Det-1, 172.30.14.21, DETROIT
WG-Det-2, 172.30.14.22, DETROIT
WG-Det-3, 172.30.14.23, DETROIT
WG-Dal-1, 172.30.14.24, DALLAS
WG-Dal-2, 172.30.14.25, DALLAS
WG-Chi-1, 172.30.14.26, CHICAGO
WG-Chi-2, 172.30.14.27, CHICAGO
WG-Chi-3, 172.30.14.28, CHICAGO
WG-Chi-4, 172.30.14.29, CHICAGO
WG-Chi-5, 172.30.14.30, CHICAGO
```

## Create the format file

A format file is now created that is suited to import the rows that are contained in the **newcomputers.csv** file. The first step in writing the format file is identifying the class type or projection type that must be used for the instances in the .csv file. For more information about class type or projection types, see the blog post [Using the CSV import feature](https://techcommunity.microsoft.com/t5/system-center-blog/using-the-csv-import-feature/ba-p/340736) and download the file CSVImport.docx.

For the type of data being imported, you find that the **Microsoft.Windows.Computer** class is the best suited for the object type and property set. Start by declaring the class of the object that is being imported:

```
<CSVImportFormat>
   <Class Type="Microsoft.Windows.Computer">
      ...
   </Class>
</CSVImportFormat>
```

After scanning the list of available properties of the **Microsoft.Windows.Computer** class, select the following properties for each column in the .csv file.

| column | property |
|---|---|
|Column 1|Principal Name|
|Column 2|IPAddress|
|Column 3|DomainDnsName|

By using these properties, you construct the following format file. The properties are listed in the order in which they appear in the .csv file. You must save this file that has the same file name for the .csv file, but with an .xml file name extension.

```
<CSVImportFormat>
   <Class Type="Microsoft.Windows.Computer">
      <Property ID="PrincipalName"/>
      <Property ID="IPAddress"/>
      <Property ID="DomainDnsName"/>
   </Class>
</CSVImportFormat>
```

Save this file as **newcomputers.xml**.

## Import configuration items from a CSV file

Before you can import data from a comma-separated value (CSV) file, you've to create two files: a data file and a format file. You can use the following procedure to import the Newcomputers.csv file by using the Newcomputers.xml format file.

To import configuration items from a CSV file, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Connectors**.

3. In the **Tasks** pane, select **Import from CSV file**.

4. In the **Import Instances from CSV File** dialog, do the following:

    1. Next to the **XML format file** box, select **Browse**, and then select the format file. For example, select **Newcomputers.xml**, and select **Open**.

    2. Next to the **Data file** box, select **Browse**, and then select the data file. For example, select **Newcomputers.csv**, and select **Open**.

5. In the **Import Instances from CSV File** dialog, select **Import**.

6. In the **Import Instances from CSV File** dialog, verify that the numbers next to **Items saved**, **Instances created in memory**, and **Instances committed to database** are equal to the number of rows in the data file, and select **Close**.

![Screenshot of the PowerShell symbol.](./media/import-data-csv/pssymbol.png) You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to import configuration items from a CSV file, see [Import-SCSMInstance](/previous-versions/system-center/powershell/system-center-2012-r2/hh316249(v=sc.20)).

### Validate the import of configuration items from a CSV file

To validate the import of configuration items from a CSV file, follow these steps:

1. In the Service Manager console, select **Configuration Items**.

2. In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and select **All Windows Computers**.

3. In the **All Windows Computers** pane, verify that the computers in the CSV file are listed.

## Next steps

- [Optionally disable ECL logging for faster connector synchronization](disable-ecl-logging.md).
