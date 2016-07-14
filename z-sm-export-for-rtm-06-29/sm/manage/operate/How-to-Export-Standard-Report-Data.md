---
title: How to Export Standard Report Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47355db0-4d3f-42a1-81df-4721e6fce723
translation.priority.mt: 
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
# How to Export Standard Report Data
You can use the following procedure in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to export a report into several different types of files so that you can use the data from the reports in different tools. For example, you can export the report data into a comma\-separated value \(CSV\) file and then import it into Microsoft Office Excel.  
  
### To open the report and then export the report data  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Reporting**.  
  
2.  Expand **Reports**, and then click any view. For example, click **Incident Management**.  
  
3.  In the **Incident Management** view, select the **List of Incidents** report, and then in the **Tasks** list, click **Run Report**.  
  
4.  Click **Parameter Control Header** to display the parameter controls for the report. Use these parameters to customize the report.  
  
5.  In the **Start Date** list, select the date one week before the current date \(today\), and then click anywhere in the form.  
  
6.  Optionally, specify other criteria that you want to filter.  
  
7.  In the **Tasks** list, click **Run Report**.  
  
8.  In the **List of Incidents** report, review the data to ensure the incident information that you want to view is displayed. If you do not see the information you expect, revise the criteria, and then run the report again by clicking **Run Report**.  
  
9. Click the **Export** icon, and then select the format in which you want to save the report. In the list, select one of the following:  
  
    -   **XML file with report data**  
  
    -   **CSV \(comma delimited\)**  
  
    -   **Acrobat \(PDF\) file**  
  
    -   **MHTML \(web archive\)**  
  
    -   **Excel**  
  
    -   **TIFF file**  
  
    -   **Word**  
  
10. Save the file to the desktop with a file name of your choice, and then close the report form.  
  
## See Also  
 [Using and Managing Standard Reports](../../../sm/manage/operate/Using-and-Managing-Standard-Reports.md)