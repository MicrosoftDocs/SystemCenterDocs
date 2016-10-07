---
title: Step 9 - Create a New Change Request Template
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
ms.assetid: 280de374-7d73-4dbb-95f5-1ed407a9ed88
---

# Step 9 - Create a New Change Request Template

>Applies To: System Center 2016 - Service Manager

In this step of the Woodgrove Bank customization scenario, Ken creates a template for the new compliance change request type; the template is named **Apply AppLocker Software Policy to Computer**. The new template helps ensure consistency among all the change requests of this type, and it helps ensure the correct workflow behavior.  

 The following procedure provides only the high\-level steps for creating a new template in the Service Manager console. For the complete procedure for creating a new template, see [How to Create Change Request Templates](admin-how-to-create-change-request-templates.md).  

### To create a new template  

1.  In the Service Manager console, specify the following as the name of the template: **Apply AppLocker Software Policy to Computer**.  

2.  Set the class to **Change Request**.  

3.  Set the management pack to **WoodGrove Automated Activity: Add Computer to AD Group**.  

4.  When the change request form is displayed, note the customizations in the form, such as the image that was previously added and the new layout of the fields.  

5.  On the **General** tab on the form, set **Area** to **Compliance**.  

6.  On the **Activities** tab, add a review activity named **Review and Approve Adding Computer to Group**, and then set the reviewer to an appropriate user.  

7.  Add the new activity **Automated Activity: Add Computer AD Group**.  

8.  Set **Group** to **GP\_AUTHAPPS**.  

9. Save the template.  
