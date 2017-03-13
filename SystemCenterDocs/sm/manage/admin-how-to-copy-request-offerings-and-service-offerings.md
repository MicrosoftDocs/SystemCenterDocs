---
title: Copy request offerings and service offerings
description: Learn about how you can copy Service Manager request offerings and service offerings.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: ee6ee7cf-23ea-4241-a58f-b6bfba8d2534
---

# Copy Service Manager request offerings and service offerings

>Applies To: System Center 2016 - Service Manager

After you create a request offering or a service offering, you can copy the offering so that you can easily modify the copied offering.

You can use the following procedures to copy a request offering and a service offering. Keep in mind that if you copy a published catalog item, the published status of the copy is set to Draft.

### To copy a request offering

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, expand **Request Offerings**, and then select **All Request Offerings**.

3.  In the **All Request Offerings** list, select the request offering that you want to copy, and then in the **Tasks** pane under *RequestOfferingName*, click **Create a Copy** to open the **Copy Request Offering** dialog box.

4.  In the dialog box, you can optionally select **Also create a copy of the template referred to in this Request Offering** to create a copy of the template.

5.  Optionally, you can change the management pack where information about the copied request offering is stored or you can create a new management pack.

6.  Click **OK** to close the dialog box and create the copy.

7.  The copied item appears in the list, with a prefix of **Copy of**. For example, your copy might have the name **Copy of Access to Active Directory Group**.

### To copy a service offering

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, expand **Service Offerings**, and then select **All Service Offerings**.

3.  In the **All Service Offerings** list, select the service offering that you want to copy, and then in the **Tasks** pane under *ServiceOfferingName*, click **Create a Copy** to open the **Copy Service Offering** dialog box.

4.  Optionally, you can change the management pack where information about the copied service offering is stored or you can create a new management pack.

5.  Click **OK** to close the dialog box and create the copy.

6.  The copied item appears in the list, with a prefix of **Copy of**. For example, your copy might have the name **Copy of Access Services**.
