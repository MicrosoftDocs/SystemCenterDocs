---
title: About Data Warehouse Dimensional Modeling Using a Star Schema
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6dc86af-1505-407a-ad5f-f076e4a38d35
 

















---
# About Data Warehouse Dimensional Modeling Using a Star Schema
The data warehouse in System Center 2012 - Service Manager is a set of databases and processes. The processes add information to the databases automatically. In short, the purpose of the data warehouse is to add information to the data mart where you and other users run reports and perform analyses to help manage your business. System Center 2012 - Service Manager stores data warehouse data longer in the warehouse than in the Service Manager database because of the usefulness of the data for trending and analysis. Also, data warehouse data often outlives its usefulness for normal transactional processing needs.  
  
 The data warehouse is optimized for aggregating and analyzing a lot of data at once in many seemly unpredictable ways. This behavior differs from transactional processing systems, which are optimized for write access on few records in any given transaction, making the behavior of those transactions more predictable.  
  
 To optimize the data warehouse for performance and ease of use, Service Manager uses the Kimball approach to dimensional modeling. \(For more information about the Kimball approach, see [Dimensional modeling](http://go.microsoft.com/fwlink/p/?LinkId=246459).\) This means that tables in the DWDataMart database are grouped logically into subject matter areas that resemble a star when they are laid out in a diagram. Therefore, these groupings are often called star schemas, and they include the following:  
  
-   In the center of the star is a fact table. Fact tables represent relationships, measures, and key performance indicators \(KPIs\). Fact tables are normally long and have relatively few columns, but they contain a large number of transactions.  
  
-   The fact table joins to dimension tables, which represent classes, properties, and enumerations. Dimension tables usually contain far fewer rows than fact tables, but they are wider because they have attributes by which report users slice and dice reports. These attributes can include status, classifications, and date attributes \(such as Created Date or Resolved Date\) of a class.  
  
-   An outrigger is a special kind of dimension table that hangs off another dimension table for performance and usability reasons.  
  
 When you think about a star schema, consider what a star schema for a coffee shop might resemble. If the transactions represent coffee purchases, the dimensions might include the following:  
  
-   A date dimension to consolidate the transaction by both Gregorian and fiscal calendars  
  
-   A customer dimension that indicates who bought the coffee  
  
-   An employee dimension that indicates who made the coffee  
  
-   A product dimension that indicates the coffee type, such as espresso, drip coffee, latte, or breve  
  
-   A store dimension  
  
 When you consider the measures that the fact table might include, the list might include the following:  
  
-   Quantity sold  
  
-   Price per unit  
  
-   Total sales  
  
-   Total discounts  
  
 Information technology \(IT\) processes are not very different from the coffee shop example when you are designing a dimensional model. There are transactions that occur, such as incident creation, resolution, and closure, that can produce interesting and useful metrics, such as time to resolution, resolution target adherence, billable time incurred by analysts, and duration in status.  
  
 When you think about extending and customizing your data warehouse, consider the business questions that you want to answer, and investigate dimensional modeling for useful information and best practices. For additional information about customizing the data warehouse, see the other topics in this section.  
  
## See Also  
 [Customizing the Data Warehouse](../../../sm/manage/operate/Customizing-the-Data-Warehouse.md)
