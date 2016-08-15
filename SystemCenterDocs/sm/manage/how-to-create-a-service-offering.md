---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Create a Service Offering
ms.technology:  service-manager
ms.assetid:  86b13898-ecdf-430a-90b7-67c66fc956c0
---

# How to Create a Service Offering

>Applies To: System Center 2016 Technical Preview - Service Manager

Service offerings are logical groups of request offerings. Both service offerings and their request offerings are available to Self-Service Portal users, when their status is set to Published and if end users have been assigned a corresponding Service Manager user role. Only users who have been assigned a user role that is associated with a catalog group that contains catalog items can use the Self-Service Portal to access the service catalog.

### To create a service offering

1.  In the Service Manager console, select **Library**.

2.  In the **Library** pane, expand **Service Catalog**, and then select **Service Offerings**.

3.  In the **Tasks** pane under **Service Offerings**, click **Create Service Offering** to open the Create Service Offering Wizard.

4.  On the **Before You Begin** page, read the instructions, and then click **Next**.

5.  On the **General** page, complete these steps:

    1.  In the **Title** box, type a title for the service offering. For example, type **Access Services**.

    2.  Optionally, next to **Image**, you can either **Browse** to an image file or leave the default selection.

    3.  In the **Category** list, select a category that this service offering will be a part of. For example, select **Access and Security**.

    4.  In the **Language** list, either leave the default selection or select a language.

    5.  In the **Overview** text box, type a short overview to describe the service offering that will be shown on the Self-Service Portal home page. For example, type **Access to AD Group, Access to Labs**.

    6.  In the description box, type a description that will appear on the service offering page in the Self-Service Portal.

    7.  Next to **Management pack**, select an unsealed management pack of your choice, and then click **Next**. For example, if you previously created the Sample Management Pack, select it.

6.  On the **Detailed Information** page, complete these steps:

    1.  In the **Service level agreement information** box, type a summary of the service level agreement (SLA) information. For example, type **The SLAs for these requests, depending on the criticality of the requests, range from 1-2 business days. For more information, click the link below.**

    2.  In the first **Link for additional information** box, type a hyperlink that users can click to view additional information about the SLA for this service offering.

    3.  In the **Cost information** box, type a summary of any costs associated with requests that will be grouped in this service offering.

    4.  In the second **Link for additional information** box, type a hyperlink that users can click to view additional information about any costs associated with requests that will be grouped in this service offering.

    5.  Click **Next**.

7.  Optionally, on the **Related Services** page, add related business services associated with the service offering, and then click **Next**.

8.  Optionally, on the **Knowledge Articles** page, add related knowledge articles associated with the service offering, and then click **Next**.

9. Optionally, on the **Request Offering** page, add related request offerings associated with the service offering, and then click **Next**.

10. On **the Publish** page, in the **Offering status** list, select **Published** and set the **Offering owner** to yourself, and then click **Next**.

11. On the **Summary** page, review the information, and then click **Create**.

12. On the **Completion** page, click **Close**.



