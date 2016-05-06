---
title: About Importing Data from Comma-Separated Files into Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: db239f58-9852-4fb9-a7fd-251103a70dba
---
# About Importing Data from Comma-Separated Files into Service Manager
Configuration items contained in a comma\-separated value \(.csv\) file can be imported into the [!INCLUDE[smshort]./Token/smshort_md.md)] database by using the Import from CSV File feature. This feature lets you to bulk\-import instances of any class type or projection type that is defined in the [!INCLUDE[smshort]./Token/smshort_md.md)] database. You can use this feature to:

-   Create configuration item or work item instances from data stored in a tabular format.

-   Bulk\-edit existing database instances.

-   Populate the [!INCLUDE[smshort]./Token/smshort_md.md)] database by using data exported from an external database.

-   Circumvent data entry through forms when many class instances must be created at the same time.

> [!NOTE]
> Importing many complex items—for example, 5,000 computer projections—could take an hour or more. During this time, [!INCLUDE[smshort]./Token/smshort_md.md)] continues to function.

Two files are required to import a set of instances by using the Import from CSV File feature:

1.  A data file that consists of a series of comma\-delimited object instances. The data file must end with the .csv file name extension.

2.  A format file that specifies the class type or projection type of the instances present in the data file. Every instance in the data file is assumed to be of this kind. The format file also specifies \(1\) the subset of properties and, for projections, specifies components. They are being imported for the indicated type, and \(2\) the order in which those properties appear as columns in the associated data file. The format file must have the same file name as the csv file that it describes, and it must end with the .xml file name extension.

## Creating the Data File
For example, you receive a spreadsheet that contains information about computers that you want to import into the [!INCLUDE[smshort]./Token/smshort_md.md)] database. The following is a sample of the first 10 computers in the spreadsheet.

|Computer Name|IP Address|Domain Name|
|-----------------|--------------|---------------|
|WG\-Det\-1|172.30.14.21|DETROIT|
|WG\-Det\-2|172.30.14.22|DETROIT|
|WG\-Det\-3|172.30.14.23|DETROIT|
|WG\-Dal\-1|172.30.14.24|DALLAS|
|WG\-Dal\-2|172.30.14.25|DALLAS|
|WG\-Chi\-1|172.30.14.26|CHICAGO|
|WG\-Chi\-2|172.30.14.27|CHICAGO|
|WG\-Chi\-3|172.30.14.28|CHICAGO|
|WG\-Chi\-4|172.30.14.29|CHICAGO|
|WG\-Chi\-5|172.30.14.30|CHICAGO|

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

## Creating the Format File
A format file is now created that is suited to import the rows that are contained in the **newcomputers.csv** file. The first step in writing the format file is identifying the class type or projection type that must be used for the instances in the .csv file. For more information about class type or projection types, see the blog post [Using the CSV import feature](http://go.microsoft.com/fwlink/p/?LinkID=159957) and download the file CSVImport.docx.

For the type of data being imported, you find that the **Microsoft.Windows.Computer** class is the best suited for the object type and property set. Start by declaring the class of the object that is being imported:

```
<CSVImportFormat>
   <Class Type=”Microsoft.Windows.Computer”>
      …
   </Class>
</CSVImportFormat>
```

After scanning the list of available properties of the **Microsoft.Windows.Computer** class, select the following properties for each column in the .csv file.

|||
|-|-|
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



