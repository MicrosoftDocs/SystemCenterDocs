---
title: Deployment considerations with a disjointed namespace
description: This article helps you avoid Service Manager Setup problems with disjointed namespaces.
ms.custom: intro-deployment, UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/22/2025
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 11c62b07-e735-415a-a632-df1589b53874
---

# Deployment considerations with a disjointed namespace


In System Center - Service Manager, Setup might fail when you deploy either an additional Service Manager management server or an additional Self-Service Portal in an environment where a disjointed namespace exists. This problem can occur if the Setup program is unable to resolve the principal name of the computer that is hosting the Service Manager management server. For more information, see the Microsoft TechNet article [Disjointed Namespace](/windows-server/identity/ad-ds/plan/disjoint-namespace).  

We recommend that you complete the following procedures before installing either an additional Service Manager management server or an additional Self-Service Portal in an environment where a disjoint namespace exists. The first procedure shows you how to determine the principal name of your Service Manager management server. The second procedure guides you in editing the hosts file on the computer that hosts either the additional Service Manager management server or the additional Self-Service Portal.  

## Determine the principal name of the Service Manager management server 

To determine the principal name, follow these steps:

1. Start a Service Manager console.  

2. In the Service Manager console, select **Configuration Items**.  

3. In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and select **All Windows Computers**.  

4. In the **All Windows Computers** pane, select the computer that hosts the Service Manager management server.  

5. In the **Tasks** pane, under the name of the computer, select **Edit**.  

6. In the **Computer - *computer name*** window, observe that there's an **Extensions** tab at the top of the form. The **Extensions** tab appears only when you view a Service Manager management server.  

7. In the **General** tab in the form, in the **Computer Identity** area, the **Principal name** box shows the principal name that you'll use in the following procedure.  

8. Select **Close** to close the form.  

9. At a command prompt, ping the Service Manager management server. You must have the IP address of the Service Manager management server for the following procedure.  

## Edit the hosts file  

To edit the hosts file, follow these steps:

1. On the computer that hosts either the additional Service Manager management server or the additional Self-Service Portal, start Windows Explorer and then locate the %Systemroot%\\System32\\Drivers\\Etc folder.  

2. Open the hosts file with Notepad by entering **notepad hosts**, and then press ENTER.  

3. At the end of the hosts file, add an entry starting with the IP address of the Service Manager management server followed by its principal name.  

4. Save and close the hosts file.  

5. You can now start the setup procedure for either an additional Service Manager management server or an additional Self-Service Portal.

## Next steps

Review [Learn about deploying the new Self Service portal and troubleshoot installation issues](learn-self-service-portal.md).
