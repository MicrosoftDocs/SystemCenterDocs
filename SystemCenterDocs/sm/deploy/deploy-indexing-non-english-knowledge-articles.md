---
title: Indexing Non-English Knowledge Articles
manager:  cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a0d866d-40b8-4f40-a175-3c5b563bbf83
---

# Indexing Non-English Knowledge Articles

>Applies To: System Center 2016 - Service Manager

If you have existing knowledge articles or are planning to create knowledge articles in any language other than English, use the following procedure to resolve an indexing issue in Microsoft SQL&nbsp;Server&nbsp;2016. This issue deals with non\-English characters that are used in only the Analyst Content and the Internal Content fields in a knowledge article. You must perform this procedure on the computer that hosts the System Center - Service Manager database. You have two tasks to perform. The first is to edit the registry, and the second is to run a series of SQL&nbsp;Server query commands on the Service Manager database.  

> [!CAUTION]  
>  Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.  

 You need three pieces of information for this procedure:  

-   This globally unique identifier \(GUID\): E2403E98\-663B\-4DF6\-B234\-687789DB8560  

-   The GUID of the .rtf file that you will discover in the following procedure  

-   The location of the file rtffil.dll, typically, C:\\Windows\\System32  

 For this procedure, it is assumed that the file rtffil.dll is located in the C:\\Windows\\System32 folder.  

### To edit the registry  

1.  On the computer hosting the Service Manager database, log on to the computer as a user with administrative credentials.  

2.  On the Windows desktop, click **Start**, and then click **Run**.  

3.  In the **Run** dialog box, in the **Open** box, type **regedit**, and then click **OK**.  

4.  If the default instance was selected during Setup, in the **Registry Editor** window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\MSSearch\\Filters\\.rtf**.  

    > [!NOTE]  
    >  If the default instance was not selected during setup, the **MSSQL13.MSSQLSERVER** node will be different.  

5.  In the right pane, double\-click **Default**.  

6.  In the **Edit String** dialog box, in the **Value data** box, make note of the GUID that you find here. This is the GUID of the rtf. file that you will use in step 8. Replace this value with the provided GUID, E2403E98\-663B\-4DF6\-B234\-687789DB8560. Make sure that open and close brackets surround this GUID. Click **OK**.  

7.  In the registry tree, above the **Filters** node that you are currently in, is the **CLSID** node. Expand **CLSID**.  

8.  In the left pane of the registry editor, locate the GUID that you saved from step 6. Right\-click this node, and then click **Rename**.  

9. Rename this node by using the provided GUID, E2403E98\-663B\-4DF6\-B234\-687789DB8560. Make sure that open and close brackets surround the GUID.  

10. In the right pane, double\-click the **Default** key.  

11. In the **Edit String** dialog box, in the **Value data** box, type the path of the file rtffilt.dll. For example, type **c:\\windows\\system32\\rtffilt.dll**, and then click **OK**.  

12. Verify that the data entry for the **ThreadingModel** key is set to **Both**.  

13. Close the Registry Editor.  

### To run the SQL Server commands  

1.  On the computer hosting the Service Manager database, on the Windows desktop, click **Start**, click **All Programs**, click **Microsoft SQL&nbsp;Server&nbsp;2016**, and then click **SQL Server Management Studio**.  

2.  In the **Connect to Server** dialog box, perform the following:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the **Server Name** list, select the server and instance for your Service Manager database.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.  

4.  In the toolbar, click **New Query**.  

5.  In the center pane, type the following commands, and then click **Execute**.  

    ```  
    exec sp_fulltext_service 'verify_signature', 0  
    go  
    exec sp_fulltext_service 'update_languages'  
    go  
    exec sp_fulltext_service 'restart_all_fdhosts'  
    go  

    ```  

6.  In the **Messages** tab, verify that the message "Command\(s\) completed successfully" appears.  

### To verify changing the .rtf filter  

1.  On the computer hosting the Service Manager database, on the Windows desktop, click **Start**, click **All Programs**, click **Microsoft SQL Server&nbsp;2016**, and then click **SQL Server Management Studio**.  

2.  In the **Connect to Server** dialog box, perform the following:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the **Server Name** list, select the server and instance for your Service Manager database.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.  

4.  In the toolbar, click **New Query**.  

5.  In the center pane, type the following, and then click **Execute**:  

    ```  
    select * from sys.fulltext_document_types where document_type = '.rtf'  
    ```  

6.  The results pane shows the following results:  

| result | value |
|---|---|
|document\_type|.rtf|  
|class\_id|E2403E98\-663B\-4DF6\-B234\-687789DB8560|  
|path|C:\\Windows\\System32\\Rtffilt.dll|
