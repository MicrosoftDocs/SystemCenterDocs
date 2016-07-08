---
title: How to Refresh OLAP Data Cube Information
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aeb99cdc-6d17-4979-bbf8-76f822e2636b


















---
# How to Refresh OLAP Data Cube Information
You can use the following procedures in System Center 2012 - Service Manager to refresh data in a Microsoft Online Analytical Processing \(OLAP\) data cube and then validate that it was refreshed. By default, most OLAP data cubes are refreshed every 24 hours. However, you can manually refresh the data to ensure that you are accessing the latest information from the data warehouse.  
  
 If necessary, you can also manually process an OLAP data cube outside of the processing job.  
  
### To refresh OLAP data cube information using the Service Manager console  
  
1.  In the Service Manager console, click **Data Warehouse**, expand it, and then click **Cubes**.  
  
2.  In the **Cubes** pane, select a cube name, and then under **Tasks**, click **Process Cube**.  
  
3.  Click **OK** to close the **Process Cube** dialog box.  
  
### To validate that the OLAP data cube was refreshed in the Service Manager console  
  
-   Select an OLAP data cube and verify that the date and time information under **Last Processed Date** has been updated since you processed the cube and that the cube **Status** is listed as **Processed**.  
  
### To manually refresh OLAP data cube information  
  
-   Run the following script for the OLAP data cube of your choice.  
  
    ```  
    Update etl.CubePartition set  
  
    watermarkbatchid = 0  
  
    where cubename = ’ComputerCube’  
    ```  
  
## See Also  
 [Using OLAP Cubes for Advanced Analytics](../../../sm/manage/operate/Using-OLAP-Cubes-for-Advanced-Analytics.md)
