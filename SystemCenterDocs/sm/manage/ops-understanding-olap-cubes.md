---
title: Understanding OLAP Cubes
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7506c69-aec8-446e-a59d-dc19917403d5
---

# Understanding OLAP Cubes

>Applies To: System Center 2016 - Service Manager

Online analytical processing \(OLAP\) cubes are a feature in Service Manager that use the existing data warehouse infrastructure to provide self\-service business intelligence capabilities to end users.  

 An OLAP cube is a data structure that overcomes the limitations of relational databases by providing rapid analysis of data. Cubes can display and sum large amounts of data while also providing users with searchable access to any data points. This way, the data can be rolled up, sliced, and diced as needed to handle the widest variety of questions that are relevant to a user's area of interest.  

 Software vendors or information technology \(IT\) developers with a working knowledge of OLAP cubes can create management packs to define their own extensible and customizable OLAP cubes that are built on the data warehouse infrastructure. These cubes are stored in SQL&nbsp;Server&nbsp;Analysis Services \(SSAS\). Self\-service business intelligence tools such as Excel and SQL&nbsp;Server Reporting Services \(SSRS\) can target these cubes in SSAS, and you can use them to analyze the data from multiple perspectives.  

 The databases that a business uses to store all its transactions and records are called online transaction processing \(OLTP\) databases. These databases usually have records that are entered one at a time and that contain a wealth of information that can be used by strategists to make informed decisions about their business. The databases that are used to store the data, however, were not designed for analysis. Therefore, retrieving answers from these databases is costly in terms of time and effort. OLAP databases are specialized databases that are designed to help extract this business intelligence information from the data.  


 OLAP cubes can be considered as the final piece of the puzzle for a data warehousing solution. An OLAP cube, also known as multidimensional cube or hypercube, is a data structure in SQL&nbsp;Server Analysis Services \(SSAS\) that is built, using OLAP databases, to allow near\-instantaneous analysis of data. The topology of this system is shown in the following illustration.  

 ![Diagram of the Service Manager 2016 DW](../media/ops-dw2012.png)  

 The useful feature of an OLAP cube is that the data in the cube can be contained in an aggregated form. To the user, the cube seems to have the answers in advance because assortments of values are already precomputed. Without having to query the source OLAP database, the cube can return answers for a wide range of questions almost instantaneously.  

 The main goal of Service Manager OLAP cubes is to give software vendors or information technology \(IT\) developers the ability to perform near\-instantaneous analysis of data for both historical analysis and trending purposes. Service Manager does this by:  

-   Allowing you to define OLAP cubes in management packs that will be created automatically in SSAS when the management pack is deployed.  

-   Automatically maintaining the cube without user intervention, performing such tasks as processing, partitioning, translations and localization, and schema changes.  

-   Allowing users to use self\-service business intelligence tools, such as Excel, to analyze the data from multiple perspectives.  

-   Saving generated Excel reports for future reference.  

 To see how data warehouse cubes are represented in the Service Manager console, navigate to the **Data Warehouse** workspace, and then click **Cubes**.  
