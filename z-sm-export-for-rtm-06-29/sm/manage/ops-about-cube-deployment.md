---
title: About Cube Deployment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58a90410-a4df-4bf1-b21c-6335b90b317e
 

















---
# About Cube Deployment
Online analytical processing \(OLAP\) cube deployment uses the Service Manager deployment infrastructure to create OLAP cubes in the SQL&nbsp;Server Analysis Services \(SSAS\) database.  
  
 To summarize, a deployable element returns a deployer with a collection of resources that are serialized and that are used to create the OLAP cube in the SSAS database. For OLAP cubes, the name of the deployable object is CubeDeployable for the SystemCenterCube element and CubeExtensionDeployable for the CubeExtension element. The deployer for both elements is CubeDeployer.  
  
 The dbo.Selector table in the DWStagingAndConfig database contains an entry for both the SystemCenterCube and CubeExtension management pack elements. The deployment engine uses this metadata if additional deployment processing is necessary for a management pack element when the management pack is imported into the data warehouse using the MPSync job.  
  
 Deployments use the Analysis Management Objects \(AMO\) application programming interface \(API\) to create and modify all the cube components in the SSAS database. Specifically, AMO in disconnected mode is used because the CubeDeployable element will not have a connection to the SSAS database. Working with AMO in disconnected mode makes it possible for you to create the entire tree of AMO objects without establishing a connection to the server. Service Manager then serializes the hierarchy of objects as stream resources and attaches them to the deployer object that is passed back to the deployment infrastructure. The deployer object is then deserialized, establishes a connection to the SSAD database, and creates the objects by sending the appropriate requests to the server.  
  
 Only major objects can be serialized. In AMO, major objects are considered classes that represent a complete object as a complete entity and not as part of another object. For example, major objects include Server, Cube, and Dimension, which are all stand\-alone entities. The DimensionAttribute, however, is not a major object because it can only be created as part of a parent major object of Dimension. DimensionAttribute, therefore, is a minor object. The OLAP cube design focuses on creating all the major objects that are needed for cubes, along with any dependent minor objects. These major objects are the objects that will be serialized-and, eventually, deserialized-before the objects are created in the SSAS database.  
  
 Resources that wrap major objects must be created in a specific order for deployment to complete successfully and satisfy the dependency requirements of the OLAP cube elements. The following two lists illustrate the deployment sequence for the SystemCenterCube and CubeExtension elements, respectively:  
  
1.  DataSourceView elements  
  
2.  dimension elements  
  
3.  date dimension element  
  
4.  cube element  
  
1.  DataSourceView elements  
  
2.  cube element  
  
## See Also  
 [Understanding OLAP Cubes](../../../sm/manage/operate/Understanding-OLAP-Cubes.md)
