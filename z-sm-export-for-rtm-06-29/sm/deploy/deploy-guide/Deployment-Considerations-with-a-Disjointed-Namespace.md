---
title: Deployment Considerations with a Disjointed Namespace
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11c62b07-e735-415a-a632-df1589b53874
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Deployment Considerations with a Disjointed Namespace
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], Setup might fail when you deploy either an additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or an additional [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] in an environment where a disjoint namespace exists. This problem can occur if the Setup program is unable to resolve the principal name of the computer that is hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. For more information, see the Microsoft TechNet article [Disjoint Namespace](http://go.microsoft.com/fwlink/p/?LinkID=187367).  
  
 We recommend that you complete the following procedures before installing either an additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or an additional [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] in an environment where a disjoint namespace exists. The first procedure shows you how to determine the principal name of your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. The second procedure guides you in editing the hosts file on the computer that hosts either the additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or the additional [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)].  
  
### To determine the principal name of the Service Manager management server  
  
1.  Start a [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
2.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Configuration Items**.  
  
3.  In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and then click **All Windows Computers**.  
  
4.  In the **All Windows Computers** pane, click the computer that hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
5.  In the **Tasks** pane, under the name of the computer, click **Edit**.  
  
6.  In the **Computer \- \<computer name\>** window, observe that there is an **Extensions** tab at the top of the form. The **Extensions** tab appears only when you view a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
7.  In the **General** tab in the form, in the **Computer Identity** area, the **Principal name** box shows the principal name that you will use in the following procedure.  
  
8.  Click **Close** to close the form.  
  
9. At a command prompt, ping the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server. You must have the IP address of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server for the following procedure.  
  
### To edit the hosts file  
  
1.  On the computer that hosts either the additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or the additional [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], start Windows Explorer, and then locate the %Systemroot%\\System32\\Drivers\\Etc folder.  
  
2.  Open the hosts file with Notepad by typing **notepad hosts**, and then press ENTER.  
  
3.  At the end of the hosts file, add an entry starting with the IP address of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server followed by its principal name.  
  
4.  Save and close the hosts file.  
  
5.  You can now start the setup procedure for either an additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or an additional [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)].