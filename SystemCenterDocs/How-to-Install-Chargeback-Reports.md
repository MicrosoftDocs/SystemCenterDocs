---
title: How to Install Chargeback Reports
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac53c27a-94b7-4ceb-9162-3fc82d933840
---
# How to Install Chargeback Reports
Chargeback reports in Service Manager consist of various files such as management pack files, Windows PowerShell scripts to import the management pack files, and a Microsoft Excel sample report. The first of the following procedures imports [!INCLUDE[smshort](./Token/smshort_md.md)] management pack files and the second procedure imports management pack files on the Operations Manager management server.

All files that comprise chargeback reports are located in the [!INCLUDE[smshort](./Token/smshort_md.md)] installation folder in the Chargeback subfolder. For example, if you installed [!INCLUDE[smshort](./Token/smshort_md.md)] in C:\\Program Files, then all chargeback report files will be located in C:\\Program Files\\Microsoft System Center 2016\\Service Manager\\Chargeback

You must have Service Manager installed and have administrative credentials on the server hosting the [!INCLUDE[smshort](./Token/smshort_md.md)] and Operations Manager management servers in order to install chargeback report files. Additionally, Operations Manager must monitor Virtual Machine Manager  servers.

The installation procedure below uses the ImportToSM.ps1 PowerShell script that uses parameters described in the following table. If you run the script without specifying any parameters, you are prompted for them.

|Parameter|Description|
|-------------|---------------|
|**omServer**|Name of the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] server|
|**omUsername**|User name of the account that has administrative access to the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] management server|
|**omPassword**|Password of the account that has administrative access to the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] management server|
|**smUsername**|User name of the account that has administrative access to the [!INCLUDE[smblue_2](./Token/smblue_2_md.md)] management server|
|**smPassword**|Password of the account that has administrative access to the [!INCLUDE[smblue_2](./Token/smblue_2_md.md)] management server|


After you have installed chargeback report files on the Operations Manager and Service Manager management servers and configured the Operations Manager CI connector, you are ready to use chargeback report features.

### To install chargeback report files on the Operations Manager management server

1.  Log on to the Operations Manager management server.

2.  In the Chargeback folder, copy the subfolder named Dependencies from the [!INCLUDE[smshort](./Token/smshort_md.md)] management server to the Operations Manager management server.

3.  On the Operations Manager management server, start Windows PowerShell and then navigate to the Dependencies folder. For example, type **cd Dependencies**.

4.  If you have not already set execution policy to remotesigned, then type the following command, and then press ENTER:

    ```
    Set-ExecutionPolicy –force RemoteSigned
    ```

5.  Type the following command, and then press ENTER to run the PowerShell script that imports chargeback management packs and that add chargeback functionality to Operations Mananger:

    ```
    .\ImportToOM.ps1
    ```

6.  After the script has completed running, type **exit**, and then press ENTER to close the **Administrator: Windows PowerShell** window.

7.  Ensure that [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] is connected to [!INCLUDE[vmmblue_2](./Token/vmmblue_2_md.md)], as described at [How to Connect VMM with Operations Manager](http://technet.microsoft.com/library/hh882396.aspx).

8.  Ensure that Operations Manager has discovered information from virtual machine manager such as virtual network interface cards, virtual hard disks, clouds, and virtual machines.

### To install chargeback reports on the Service Manager management server

1.  Log on to the Service Manager management server.

2.  On the computer where you want to run Windows PowerShell, click **Start**, click **All Programs**, click **Microsoft System Center 2016**, click **Service Manager**, and then click **Service Manager Shell**.

3.  If you have not already set execution policy to remotesigned, then type the following command, and then press ENTER:

    ```
    Set-ExecutionPolicy –force RemoteSigned
    ```

4.  Navigate to the Chargeback folder. For example, type **cd chargeback**.

5.  Type the following command, and then press ENTER to run the PowerShell script that imports chargeback management packs and that add chargeback functionality to [!INCLUDE[smshort](./Token/smshort_md.md)]:

    ```
    .\ImportToSM.ps1
    ```

6.  After the script has completed running, type **exit**, and then press ENTER to close the **Administrator: Windows PowerShell** window.

7.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Data Warehouse Jobs**.

8.  In the list of data warehouse jobs, select **MPSyncJob** and then in the Task list, click **Resume**.

9. Configure the Operations Manager CI connector and ensure that [!INCLUDE[smshort](./Token/smshort_md.md)] has discovered the virtual machine information from Operations Manager.


