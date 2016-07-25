---
title: Delay Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18da38ac-7045-4554-982f-e05a1763e8cb


















---
# Delay Activity
This activity introduces a delay between activities in a workflow in System Center 2012 - Service Manager. The **Delay** activity is derived from the Microsoft .NET&nbsp;Framework **DelayActivity** class.  
  
## Design Time Prerequisites  
 None.  
  
## Run Time Prerequisites  
 None.  
  
## Properties  
 The **Delay** activity uses the input properties that are listed in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Initialize TimeoutDuration|InitializeTimeoutDuration||Internal|Specifies a handler to initialize the **TimeoutDuration** property.|  
|TimeoutDuration|TimeoutDuration|Timespan|Yes|Duration of the delay.|  
  
 The **Delay** activity does not produce an output property.  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 For more information about this activity, see [DelayActivity Class](http://go.microsoft.com/fwlink/p/?LinkID=186252) in the .NET&nbsp;Framework Class Library.  
  
## Example  
 None.  
  
## See Also  
 [Delete Control Flow Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///7643bc64-8f70-4215-8cad-e2e7901cbfad)
