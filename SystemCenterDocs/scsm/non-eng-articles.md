---
title: Index non-English knowledge articles
description: This article helps you resolve issues when you want to index non-English knowledge articles.
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a0d866d-40b8-4f40-a175-3c5b563bbf83
---

# Index non-English Service Manager knowledge articles



If you've existing knowledge articles or are planning to create knowledge articles in any language other than English, use the following procedure to resolve an indexing issue in Microsoft SQL Server 2016. This issue deals with non-English characters that are used in only the Analyst Content and the Internal Content fields in a knowledge article. You must perform this procedure on the computer that hosts the System Center - Service Manager database. You have two tasks to perform. The first is to edit the registry, and the second is to run a series of SQL Server query commands on the Service Manager database.  

> [!NOTE]
> The indexing issue has been resolved in the later versions of Microsoft SQL Server 2016. However, if the issue persists, resolve it by using the same procedure outlined for Microsoft SQL Server 2016.

> [!CAUTION]  
> Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.  

 You need three pieces of information for this procedure:  

- This globally unique identifier \(GUID\): E2403E98\-663B\-4DF6\-B234\-687789DB8560  

- The GUID of the .rtf file that you'll discover in the following procedure  

- The location of the file rtffil.dll, typically, C:\\Windows\\System32  

For this procedure, it's assumed that the file rtffil.dll is located in the C:\\Windows\\System32 folder.  

## Edit the registry  

1. On the computer hosting the Service Manager database, sign in to the computer as a user with administrative credentials.  

2. On the Windows desktop, select **Start**, and select **Run**.  

3. In the **Run** dialog, in the **Open** box, enter **regedit**, and select **OK**.  

4. If the default instance was selected during Setup, in the **Registry Editor** window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\MSSearch\\Filters\\.rtf**.  

    > [!NOTE]  
    > If the default instance wasn't selected during setup, the **MSSQL13.MSSQLSERVER** node will be different.  

5. In the right pane, double-click **Default**.  

6. In the **Edit String** dialog, in the **Value data** box, make note of the GUID that you find here. This is the GUID of the rtf. file that you'll use in step 8. Replace this value with the provided GUID, E2403E98\-663B\-4DF6\-B234\-687789DB8560. Ensure that open and close brackets surround this GUID. Select **OK**.  

7. In the registry tree, above the **Filters** node that you're currently in, is the **CLSID** node. Expand **CLSID**.  

8. In the left pane of the registry editor, locate the GUID that you saved from step 6. Right-click this node, and select **Rename**.  

9. Rename this node by using the provided GUID, E2403E98\-663B\-4DF6\-B234\-687789DB8560. Ensure that open and close brackets surround the GUID.  

10. In the right pane, double-click the **Default** key.  

11. In the **Edit String** dialog, in the **Value data** box, enter the path of the file rtffilt.dll. For example, enter **c:\\windows\\system32\\rtffilt.dll**, and select **OK**.  

12. Verify that the data entry for the **ThreadingModel** key is set to **Both**.  

13. Close the Registry Editor.  

### Run the SQL Server commands  

1. On the computer hosting the Service Manager database, on the Windows desktop, select **Start**, select **All Programs**, select **Microsoft SQL&nbsp;Server&nbsp;2016**, and select **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, perform the following:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the server and instance for your Service Manager database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, expand **Databases**, and select **ServiceManager**.  

4. In the toolbar, select **New Query**.  

5. In the center pane, enter the following commands, and select **Execute**.  

    ```  
    exec sp_fulltext_service 'verify_signature', 0  
    go  
    exec sp_fulltext_service 'update_languages'  
    go  
    exec sp_fulltext_service 'restart_all_fdhosts'  
    go  

    ```  

6. In the **Messages** tab, verify that the message **Command(s) completed successfully** appears.  

### Verify changing the .rtf filter  

1. On the computer hosting the Service Manager database, on the Windows desktop, select **Start**, select **All Programs**, select **Microsoft SQL Server&nbsp;2016**, and select **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, perform the following:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the server and instance for your Service Manager database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, expand **Databases**, and select **ServiceManager**.  

4. In the toolbar, select **New Query**.  

5. In the center pane, enter the following, and select **Execute**:  

    ```  
    select * from sys.fulltext_document_types where document_type = '.rtf'  
    ```  

6. The results pane shows the following results:  

| result | value |
|---|---|
|document\_type|.rtf|  
|class\_id|E2403E98\-663B\-4DF6\-B234\-687789DB8560|  
|path|C:\\Windows\\System32\\Rtffilt.dll|

## Next steps

- To review logs files that are created when you install Service Manager and how you can use these logs to troubleshoot deployment issues, see [Troubleshoot deployment issues to resolve problems](troubleshoot-deployment.md).
