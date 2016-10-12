---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Installing and Configuring Chargeback Reports in System Center 2016   Service Manager
ms.technology:  service-manager
ms.assetid:  d803af83-e809-4633-a0b5-ccfc3b593138
---

# Installing and Configuring Chargeback Reports in System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This section provides an overview of key concepts for chargeback reports in Service Manager. This section also contains procedures that you can use to install and configure chargeback reports.

## About Chargeback Reports

As traditional IT transitions into a cloud-optimized IT, service providers are facing a new set of challenges that places a high demand on them. One of the goals of System Center 2016 is to enable and help you, the service provider, to manage the transition, and to help you succeed in your offerings.

In traditional IT, infrastructure was largely physical, service level agreements (SLAs) were typically periods of weeks and months, and capacity was owned and managed by the consumers. However, this is no longer true. With the arrival of centrally pooled resources, on-demand self-service, and short SLAs, service consumers can continue their old habits, which are to over-subscribe and underutilize, without having to carry the burden of managing the acquired capacity. If not managed properly, the ability of the service provider can be compromised in these situations.

In System Center, chargeback is one of the tools that help you communicate with business units about how they consume capacity. This helps you by utilize existing investments, proportionate to your customer's requests. System Center components help you manage the following processes:

-   Quotas
-   Leases
-   Approvals
-   Chargeback or showback

The theme of chargeback is cloud based pricing, where each cloud has its own price, based on SLA. Most often, you'll have many clouds with various SLAs for the clouds for different business units or organizations. Chargeback uses a price sheet, or rate card, for each cloud. This means you can have one price represented in a price sheet that contains various clouds addressing one SLA, and you can have another price sheet for a different SLA.

Specifically, Chargeback in Service Manager uses information discovered from the Operations Manager CI connector about the Virtual Machine Manager fabric that you manage. The private cloud information from Virtual Machine Manager, such as clouds and virtual machines, is what helps define a successful private cloud by offering centrally pooled resources that are metered and charged based on consumption.

Price sheets, or rate cards, are created in Service Manager for Virtual Machine Manager clouds. The clouds are then assigned to prices sheets. For example, you might have price sheets that are associated to silver and bronze clouds in order to differentiate levels of service.

Service Manager comes with a sample report, but its reporting infrastructure is OLAP cube-based, so you can easily create your own reports. You can easily customize the sample report with colors, logos, or whatever you can think of that will best suit your needs. You can use the OLAP cube information presented in the Data Warehouse workspace to easily create a simple pivot table in Microsoft Excel. After you select fields you like, you can format the data any way you like just like you would any other information in Excel.

It's important to let customers know that IT resources are limited in their capacity. You can use chargeback or showback reports to show resource utilization and the associated costs to influence consumption behaviors.

### Operations Manager Requirements
Before you can use chargeback reports, you must create and synchronize an Operations Manager CI connector so that Operations Manager discovers virtual machine resources from Virtual Machine Manager. Earlier versions of Virtual Machine Manager are not supported with Chargeback. During this process, you must synchronize the VMM.2016.Discovery management pack. For more information about creating and synchronizing an Operations Manager CI connector, see [How to Create a System Center Operations Manager Connector](admin-importing-data-and-alerts-from-system-center-operations-manager.md). The following object properties are imported into Service Manager using the connector:

-   virtual machine CPU count

-   virtual machine memory

-   virtual machine storage

-   virtual network interface cards

-   virtual disks

-   virtual machines - this is used to collect a fixed price for virtual machines other than for virtual machine components

-   clouds - used to collect cloud membership price for clouds other than virtual machine or virtual machine component costs

## How to Install Chargeback Reports

Chargeback reports in Service Manager consist of various files such as management pack files, Windows PowerShell scripts to import the management pack files, and a Microsoft Excel sample report. The first of the following procedures imports Service Manager management pack files and the second procedure imports management pack files on the Operations Manager management server.

All files that comprise chargeback reports are located in the Service Manager installation folder in the Chargeback subfolder. For example, if you installed Service Manager in C:\Program Files, then all chargeback report files will be located in C:\Program Files\Microsoft System Center 2016\Service Manager\Chargeback

You must have Service Manager installed and have administrative credentials on the server hosting the Service Manager and Operations Manager management servers in order to install chargeback report files. Additionally, Operations Manager must monitor Virtual Machine Manager  servers.

The installation procedure below uses the ImportToSM.ps1 PowerShell script that uses parameters described in the following table. If you run the script without specifying any parameters, you are prompted for them.

|Parameter|Description|
|-------------|---------------|
|**omServer**|Name of the Operations Manager server|
|**omUsername**|User name of the account that has administrative access to the Operations Manager management server|
|**omPassword**|Password of the account that has administrative access to the Operations Manager management server|
|**smUsername**|User name of the account that has administrative access to the Service Manager management server|
|**smPassword**|Password of the account that has administrative access to the Service Manager management server|


After you have installed chargeback report files on the Operations Manager and Service Manager management servers and configured the Operations Manager CI connector, you are ready to use chargeback report features.

### To install chargeback report files on the Operations Manager management server

1.  Log on to the Operations Manager management server.

2.  In the Chargeback folder, copy the subfolder named Dependencies from the Service Manager management server to the Operations Manager management server.

3.  On the Operations Manager management server, start Windows PowerShell and then navigate to the Dependencies folder. For example, type **cd Dependencies**.

4.  If you have not already set execution policy to remotesigned, then type the following command, and then press ENTER:

    ```
    Set-ExecutionPolicy -force RemoteSigned
    ```

5.  Type the following command, and then press ENTER to run the PowerShell script that imports chargeback management packs and that add chargeback functionality to Operations Mananger:

    ```
    .\ImportToOM.ps1
    ```

6.  After the script has completed running, type **exit**, and then press ENTER to close the **Administrator: Windows PowerShell** window.

7.  Ensure that Operations Manager is connected to Virtual Machine Manager, as described at [How to Connect VMM with Operations Manager](http://technet.microsoft.com/library/hh882396.aspx).

8.  Ensure that Operations Manager has discovered information from virtual machine manager such as virtual network interface cards, virtual hard disks, clouds, and virtual machines.

### To install chargeback reports on the Service Manager management server

1.  Log on to the Service Manager management server.

2.  On the computer where you want to run Windows PowerShell, click **Start**, click **All Programs**, click **Microsoft System Center 2016**, click **Service Manager**, and then click **Service Manager Shell**.

3.  If you have not already set execution policy to remotesigned, then type the following command, and then press ENTER:

    ```
    Set-ExecutionPolicy -force RemoteSigned
    ```

4.  Navigate to the Chargeback folder. For example, type **cd chargeback**.

5.  Type the following command, and then press ENTER to run the PowerShell script that imports chargeback management packs and that add chargeback functionality to Service Manager:

    ```
    .\ImportToSM.ps1
    ```

6.  After the script has completed running, type **exit**, and then press ENTER to close the **Administrator: Windows PowerShell** window.

7.  In the Service Manager console, click **Data Warehouse**, expand the **Data Warehouse** node, and then click **Data Warehouse Jobs**.

8.  In the list of data warehouse jobs, select **MPSyncJob** and then in the Task list, click **Resume**.

9. Configure the Operations Manager CI connector and ensure that Service Manager has discovered the virtual machine information from Operations Manager.
